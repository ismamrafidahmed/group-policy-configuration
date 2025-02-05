<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in Windows Server 2022 Virtual Machine </h1>
This tutorial outlines the implementation of on-premises Active Directory within Windows Server 2022 using VirtualBox<br />

<h2>Environments and Technologies Used</h2>

- VirtualBox
- Active Directory Domain Services
- Group Policy Management 

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro

<h2>Deployment and Configuration Steps Covered in This Section</h2>

- Configuring Group Policy
- Implementing a Strong Password Policy
- Implementing Account Lockout Policy
- Implementing a Custom Login Message Policy
- Enforcing Group Policy Updates on Domain Users
- Checking if Policies Have Been Applied to Domain Accounts
- Results of Enforced Group Policies

<h2>Deployment and Configuration Steps</h2>

Open the server manager, access tools, and group policy manager to view the group policy window. 

To view default policies, right-click the default domain policy, then click edit

![image](https://github.com/user-attachments/assets/e356d4d0-76df-4fdb-8f4a-22d90c52f4ac)

Implementing a Strong Password Policy

Path: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy

Settings to Modify:

Minimum Password Length → Set to at least 10-12 characters.
Password Complexity → Enable (requires uppercase, lowercase, numbers, special characters).
Maximum Password Age → Set to 60 days (forces password change).

Effect: Improves security by ensuring users have strong passwords.

![image](https://github.com/user-attachments/assets/7fc60643-9714-4249-99cf-41051ffb5571)

Implementing Account Lockout Policy

This policy locks user accounts after multiple failed login attempts, preventing unauthorized access.

Steps to Configure:

Open Group Policy Management Editor in your Windows Server 2022 VM.
Navigate to: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy
Configure the following settings:
Account lockout threshold → Set to 5 (locks account after 5 failed attempts).
Account lockout duration → Set to 15 minutes (locked accounts remain locked for 15 minutes).
Reset account lockout counter after → Set to 10 minutes (failed attempts reset after 10 minutes).

Effect:

If a user enters the wrong password 5 times, their account is locked for 15 minutes.
After 10 minutes, the failed login count resets.

![image](https://github.com/user-attachments/assets/1c16ae67-19d7-4db2-82d0-db811020dcb8)

Implementing a Custom Login Message Policy

This policy displays a message before the login screen, useful for setting rules, and warnings, or just adding a personal touch.

Steps to Configure:

Open Group Policy Management Editor on your Windows Server 2022 VM.
Navigate to: Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options
Interactive logon: Message title for users attempting to log on → Set to: “Welcome to Rafid’s Homelab Server"
Interactive logon: Message text for users attempting to log on → Set to: ”This is a private server for testing, learning, and experimenting with IT systems. Unauthorized access is not allowed. 

Effect:

Before logging in, users (including you) will see this message.
It adds a layer of security and a personal touch to your home lab setup.

![image](https://github.com/user-attachments/assets/795acb6b-0f27-47b5-b781-381cd5f67c6b)

Enforcing Group Policy Updates on Domain Users

Open Command Prompt as administrator on the Windows Server 2022 VM.
Run the following command to force update the Group Policy: gpupdate /force
If you made security-related changes (like password policies), reboot the server: shutdown /r /t 0

![image](https://github.com/user-attachments/assets/83533866-24ee-4144-a4e6-cfd2d1a6b80d)

Checking if Policies Have Been Applied to Domain Accounts

Since password and account lockout policies apply at the domain level, they will automatically affect all users. 

However, ensure that domain users are receiving these policies correctly.

Open Command Prompt (Admin), run gpresult /r
Look under Applied Group Policy Objects (GPOs) and verify your policies appear.

Results of Enforced Group Policies

Custom Login Message Policy

![image](https://github.com/user-attachments/assets/4f1a1398-ada7-402a-9097-67fbcd50dfb3)

Account Lockout Policy 

Input incorrect password 6 times to get locked out. 

![image](https://github.com/user-attachments/assets/31936add-3940-45fc-abda-b0d4033b4a53)

Now that this account is locked out, go to ADUC, reset the password for the user and create a temporary new password. 

![image](https://github.com/user-attachments/assets/134259a2-8eb9-4e9f-b0af-3bf0cfd7c8e6)

Strong Password Policy 

Reset client-1 and log in using the temporary password created in ADUC. Next, you will be prompted to create a new password. Try inserting a new password that does not fit the 12-character minimum limit and you will see an error message pop up, this indicates that the strong password policy we implemented earlier has been forced. 

![image](https://github.com/user-attachments/assets/b8a79d6e-608f-4b7e-93a7-4c20126c5ec7)

![image](https://github.com/user-attachments/assets/3359f084-9348-43cd-9500-bedef4740486)










