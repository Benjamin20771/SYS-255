# ADDS Lab - Step-by-Step Completion Guide

## Prerequisites
- Lab 4 must be complete and functional
- Access to Active Directory Users and Computers
- Domain controller with ADDS role installed

## Part 1: OU Structure Creation

### Step 1: Open Active Directory Users and Computers
1. On your domain controller, open **Active Directory Users and Computers**
2. Navigate to your domain (yourname.local)

### Step 2: Create Main OU
1. Right-click on your domain name
2. Select **New** → **Organizational Unit**
3. Name it **"SYS255"**
4. Uncheck "Protect container from accidental deletion" (if desired)
5. Click **OK**

### Step 3: Create Child OUs
1. Right-click on the **SYS255** OU
2. Create three child OUs:
   - **Accounts** (for users)
   - **Computers** (for workstations)
   - **Groups** (for security groups)

## Part 2: Create Users and Groups

### Step 4: Create Users
1. Navigate to **SYS255\Accounts** OU
2. Right-click → **New** → **User**
3. Create three users:
   - **Alice** (First: Alice, Last: [surname], User logon: alice)
   - **Bob** (First: Bob, Last: [surname], User logon: bob)
   - **Charlie** (First: Charlie, Last: [surname], User logon: charlie)
4. Set passwords for each user
5. Uncheck "User must change password at next logon" for lab purposes

### Step 5: Move WKS01 Computer
1. Navigate to **yourname.local\Computers**
2. Find **WKS01**
3. Drag and drop **WKS01** to **SYS255\Computers** OU

### Step 6: Create Security Group
1. Navigate to **SYS255\Groups** OU
2. Right-click → **New** → **Group**
3. Group name: **custom-desktop**
4. Group scope: **Global**
5. Group type: **Security**
6. Click **OK**

### Step 7: Add Members to Group
1. Double-click **custom-desktop** group
2. Go to **Members** tab
3. Click **Add**
4. Add **Alice** and **Bob** (NOT Charlie)
5. Click **OK**

## Part 3: Create User Group Policy

### Step 8: Open Group Policy Management
1. Open **Group Policy Management Console**
2. Navigate to your domain → **SYS255** OU

### Step 9: Create User GPO
1. Right-click **SYS255** OU
2. Select **Create a GPO in this domain, and Link it here**
3. Name: **sys255-desktop**
4. Click **OK**

### Step 10: Configure Security Filtering
1. Click on **sys255-desktop** GPO
2. In **Security Filtering** section:
   - Click **Add** → Add **custom-desktop** group
   - Select **Authenticated Users** → Click **Remove**
   - Click **Add** → Add **Domain Computers**

### Step 11: Configure Advanced Permissions
1. Click **Delegation** tab
2. Click **Advanced**
3. Select **Authenticated Users**
4. Uncheck **Apply group policy**
5. Check **Deny** for **Apply group policy**
6. Click **OK**

### Step 12: Edit User Policy Settings
1. Right-click **sys255-desktop** GPO → **Edit**
2. Navigate to: **User Configuration** → **Administrative Templates** → **Desktop**
3. Find **Remove Recycle Bin icon from desktop**
4. Double-click and set to **Enabled**
5. Click **Apply** → **OK**
6. Close Group Policy Editor

## Part 4: Create Computer Group Policy

### Step 13: Create Computer GPO
1. Navigate to **SYS255\Computers** OU in Group Policy Management
2. Right-click → **Create a GPO in this domain, and Link it here**
3. Name: **DisableLastLogin**

### Step 14: Configure Computer GPO Security
1. Select **DisableLastLogin** GPO
2. In **Security Filtering**:
   - Remove **Authenticated Users**
   - Add **Domain Computers**

### Step 15: Edit Computer Policy
1. Right-click **DisableLastLogin** → **Edit**
2. Navigate to: **Computer Configuration** → **Administrative Templates** → **System** → **Logon**
3. Find **Do not display last user name**
4. Double-click and set to **Enabled**
5. Click **Apply** → **OK**
6. Close Group Policy Editor

## Part 5: Testing and Deliverables

### Step 16: Test User Policy (Deliverable 1)
1. Go to **WKS01**
2. Login as **Alice** (alice@yourname.local)
3. Verify Recycle Bin is NOT on desktop
4. Open Command Prompt
5. Run: `gpresult /r`
6. Take screenshot showing VM name, no Recycle Bin, and gpresult output

### Step 17: Test Computer Policy (Deliverable 2)
1. On **WKS01**, open Command Prompt as Administrator
2. Run: `gpupdate /force`
3. Run: `gpresult /scope computer /r`
4. Take screenshot showing DisableLastLogin policy applied

### Step 18: Verify Login Screen Changes (Deliverable 3)
1. Sign out of **WKS01**
2. Observe login screen - should NOT show last logged-in user
3. Take screenshot of clean login screen

### Step 19: Create Network Diagram (Deliverable 4)
1. Use diagrams.net or similar tool
2. Create network diagram including:
   - Domain Controller (hostname, IP, services)
   - WKS01 (hostname, IP)
   - Network connections
   - Domain structure
   - OU hierarchy
3. Document preparation plan for next week's assessment

## Commands Used in Lab
- `gpupdate /force` - Forces immediate group policy update
- `gpresult /r` - Shows applied group policies for user
- `gpresult /scope computer /r` - Shows applied computer policies

## Troubleshooting Tips
- If policies don't apply immediately, wait 90-120 minutes or use gpupdate /force
- Ensure correct security filtering is applied to GPOs
- Verify computer and user accounts are in correct OUs
- Check Event Viewer for Group Policy errors if issues occur
