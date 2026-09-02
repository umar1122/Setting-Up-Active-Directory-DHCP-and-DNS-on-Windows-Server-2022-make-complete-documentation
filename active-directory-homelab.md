# Active Directory Home Lab

A small home lab where I set up my first Active Directory environment from scratch using Hyper-V. This covers installing AD DS, setting up DNS and DHCP, building an OU structure, creating users, and joining a client PC to the domain.

## Goal

I wanted a working domain environment I could keep building on later (more domain controllers, group policy, etc). For this first pass I kept it simple:

- One server acting as the domain controller
- One Windows 10 client that joins the domain
- A basic OU structure to separate IT staff from regular staff

## Lab Setup

| Machine | Role | Notes |
|---|---|---|
| DC01 | Domain Controller | Windows Server 2022, static IP `192.168.0.1`, runs AD DS + DNS + DHCP |
| PC01 | Client | Windows 10, gets its IP from DHCP, joined to the domain |

Both machines run as VMs on Hyper-V, connected on the same private virtual switch.

Domain name: `int.acme.com`
NetBIOS name: `ACME`

## 1. Prep the server

Before touching Active Directory:

- Deployed Windows Server 2022
- Renamed the machine to `DC01`
- Set a static IP (`192.168.0.1`) — a domain controller should never be on DHCP

## 2. Install the AD DS role

From Server Manager → **Add Roles and Features** → picked a role-based install → selected **Active Directory Domain Services**.

A few things worth noting from this step:

- It also pulls in the Group Policy Management tools automatically
- It warned me that DNS isn't installed yet — I let it install DNS at the same time instead of doing it separately
- Installing the role itself doesn't create the domain yet, it just adds the software. The actual domain gets created in the next step (post-deployment configuration)
- This role **does require a restart** later, unlike DHCP/DNS role installs which don't

## 3. Promote the server to a Domain Controller

After the role finished installing, I ran the post-deployment wizard and chose **"Add a new forest"** since this is a brand new environment.

**Domain name:** I went with `int.acme.com` instead of just `acme.com`. The idea is to avoid mixing your internal AD domain name with your public-facing domain name — using the same name for both gets messy (you'd need extra config known as split-brain DNS). Prepending something like `int.` keeps internal and external separate.

Other choices made during the wizard:

- Kept the default forest/domain functional level (didn't downgrade for old Windows Server 2008 compatibility since I don't need it)
- This DC also became the DNS server and holds the Global Catalog
- Set a Directory Services Restore Mode (DSRM) password
- Changed the auto-generated NetBIOS name from `INT` to `ACME` — this is what shows up in the login screen for users, and `INT` alone would've been confusing
- Let it use default file paths for the AD database
- Ran through the prerequisite checks (a couple of yellow warnings, nothing blocking) and hit install

The install finishes with a reboot — this is the restart mentioned earlier.

## 4. Check DNS

Once the server came back up, I confirmed AD had built out DNS automatically:

- Forward lookup zone for `int.acme.com` was already there, including the A record for DC01
- **Reverse lookup zone was missing** — AD doesn't create this for you, so I added it manually:
  - New Zone → Primary zone → Reverse lookup zone
  - Replication scope set to replicate to all DNS servers running on domain controllers in the domain (useful later if I add a second DC)
  - Network: `192.168.0.0/24`
  - Enabled secure dynamic updates so new machines register themselves automatically
- Went back into the forward zone and refreshed the pointer (PTR) record for DC01 to make sure it matched

## 5. Install DHCP

Added the DHCP role the same way as AD DS (Server Manager → Add Roles). After install, DHCP needs to be authorized against Active Directory — it asked to use the domain admin account for this, which I approved.

Created a scope:

- Name: `ACME IPv4`
- Range: `192.168.0.50` – `192.168.0.200` (plenty for a lab)
- Subnet mask: `255.255.255.0`
- Default gateway handed out: `192.168.0.254`
- DNS server handed out: `192.168.0.1` (DC01) — the wizard actually detected the domain and suggested this automatically
- No WINS
- Activated the scope

Tested it from PC01 — it picked up `192.168.0.50` from DHCP right away.

## 6. Build an OU structure

Under Active Directory Users and Computers, I created a small structure to keep things organized:

```
int.acme.com
└── ACME (OU)
    ├── IT (OU)
    └── Staff (OU)
```

When creating each OU, I unchecked **"Protect container from accidental deletion"** — it's easier to work with while you're still shaping the lab. In a real production environment you'd want to leave that protection on.

Also worth noting: the built-in **Computers** container already had `PC01` sitting in it automatically once I joined that machine to the domain (see step 7).

## 7. Create users

Created two test accounts:

- **troy** — placed in the `IT` OU, logon name `tberg`, added to the **Domain Admins** group so this account can be used for admin tasks instead of logging in as the built-in `administrator` account
- **batman** — placed in the `Staff` OU, logon name `bman`, left "user must change password at next logon" checked

## 8. Join the client PC to the domain

On PC01:

1. Confirmed it had picked up a DHCP address
2. System Properties → Change domain/workgroup
3. Joined `int.acme.com`
4. When prompted, authenticated with the domain admin account (not a local PC account — local accounts aren't recognized by AD)
5. Restarted the machine

After the reboot, the login screen let me log in as a domain user instead of just local accounts.

## 9. Test everything

- Logged into PC01 as `tberg` — authenticated successfully against DC01. Ran `query user` to confirm the session was recognized as a domain login.
- Logged in as `bman` — was prompted to change the password on first login as expected, then landed on a fresh profile.

Both logins were authenticated by DC01, confirming AD, DNS, and DHCP were all working together correctly.

## Result

At the end of this, I had:

- A working AD DS domain (`int.acme.com` / NetBIOS `ACME`)
- DNS with both forward and reverse lookup zones
- DHCP handing out addresses and pointing clients to the domain's DNS server
- A basic OU structure separating IT from general staff
- A domain-joined client and two working domain user accounts, one with admin rights

## Next steps

- Add a second domain controller for redundancy
- Set up Group Policy
- Build out more OUs / security groups as the lab grows
