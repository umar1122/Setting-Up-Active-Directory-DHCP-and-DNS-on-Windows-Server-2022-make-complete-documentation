# Organizational Units

## Goal

Organize Active Directory objects using Organizational Units (OUs).

## Example structure

```text
corp.example.test
├── IT
│   └── Users
├── Administration
│   └── Users
├── Computers
└── Service Accounts
```

## Step 1: Create an OU

In **Active Directory Users and Computers**, right-click the domain and select **New → Organizational Unit**.

**Screenshot:**  
`![Create OU](../screenshots/19-create-ou.png)`

## Step 2: Create the lab OUs

Create OUs that match the needs of your lab.

**Screenshot:**  
`![OU structure](../screenshots/20-ou-structure.png)`

## Result

Users and computers can now be organized into logical administrative units.
