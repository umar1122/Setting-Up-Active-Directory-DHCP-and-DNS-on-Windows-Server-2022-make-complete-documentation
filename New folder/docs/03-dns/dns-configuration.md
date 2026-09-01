# DNS Configuration

## Goal

Configure and verify DNS for the Active Directory lab.

## Step 1: Open DNS Manager

Open:

**Server Manager → Tools → DNS**

**Screenshot:**  
`![DNS Manager](../screenshots/21-dns-manager.png)`

## Step 2: Check the forward lookup zone

Verify that the Active Directory domain zone exists.

Example:

`corp.example.test`

**Screenshot:**  
`![Forward lookup zone](../screenshots/22-forward-zone.png)`

## Step 3: Verify host records

Check that the domain controller has the expected DNS records.

**Screenshot:**  
`![DNS records](../screenshots/23-dns-records.png)`

## Step 4: Test DNS

From a Windows client:

```powershell
nslookup corp.example.test
```

You can also test the domain controller hostname.

**Screenshot:**  
`![DNS test](../screenshots/24-dns-test.png)`

## Result

DNS is resolving the Active Directory lab domain and controller.
