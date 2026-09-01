# Active Directory Domain Setup

## Goal

Install Active Directory Domain Services (AD DS) and create a lab domain.

## Step 1: Install AD DS

Open **Server Manager → Add Roles and Features**.

Select **Active Directory Domain Services**.

**Screenshot:**  
`![AD DS role](../screenshots/10-ad-ds-role.png)`

## Step 2: Promote the server

After the role installation, select **Promote this server to a domain controller**.

**Screenshot:**  
`![Promote server](../screenshots/11-promote-server.png)`

## Step 3: Create a new forest

Select **Add a new forest** and use a lab-only domain name, for example:

`corp.example.test`

Do not use a real public domain that you do not control.

**Screenshot:**  
`![New forest](../screenshots/12-new-forest.png)`

## Step 4: Configure domain controller options

Configure the forest and domain functional levels and set the Directory Services Restore Mode password.

**Screenshot:**  
`![Domain controller options](../screenshots/13-domain-controller-options.png)`

## Step 5: Complete the installation

Review the configuration, install the role and restart the server.

**Screenshot:**  
`![AD DS installation](../screenshots/14-ad-installation.png)`

## Verify

Sign in using the domain administrator account and open **Active Directory Users and Computers**.
