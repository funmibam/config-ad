# Configuring Active Directory with Azure VMs

## Project Overview
This project involved configuring an Active Directory (AD) environment using Azure Virtual Machines (VMs) and Virtual Network (VNet). The project setup included creating a Domain Controller (DC-1) on a Windows Server 2022 machine and a client machine (Client-1) on Windows 10. The domain was configured, and a Domain Admin account was created. 

## Steps Performed

### 1. Setup Domain Controller in Azure

1. **Create a Resource Group**  
   Created a new Resource Group in the Azure portal to organize all resources related to the project.

   ![Screenshot Placeholder: Resource Group Creation](#)

2. **Create a Virtual Network and Subnet**  
   Created a Virtual Network (VNet) and Subnet for communication between DC-1 and Client-1.

   ![Screenshot Placeholder: Virtual Network Configuration](#)

3. **Create the Domain Controller VM**  
   I created a Virtual Machine running **Windows Server 2022**, named **DC-1**.  
   - Username: `labuser`  
   - Password: `Cyberlab123!`

   ![Screenshot Placeholder: DC-1 VM Creation](#)

4. **Set Static Private IP for DC-1**  
   Set the Network Interface (NIC) of DC-1 to have a **static private IP address** for DNS consistency.

   ![Screenshot Placeholder: NIC Settings for Static IP](#)

5. **Disable Windows Firewall on DC-1**  
   Disabled the Windows Firewall on DC-1 for connectivity testing.

### 2. Setup Client-1 in Azure

1. **Create Client-1 VM**  
   Created a Windows 10 VM, **Client-1**, with the same credentials as DC-1.  
   - Username: `labuser`  
   - Password: `Cyberlab123!`

   ![Screenshot Placeholder: Client-1 VM Creation](#)

2. **Configure DNS on Client-1**  
   Set Client-1's DNS to point to DC-1’s static private IP for proper domain resolution.

   ![Screenshot Placeholder: DNS Configuration on Client-1](#)

3. **Restart Client-1 and Test Connectivity**  
   Restarted Client-1 and successfully pinged DC-1’s private IP, confirming connectivity.

   ![Screenshot Placeholder: Ping Test Success](#)

4. **Verify DNS Settings on Client-1**  
   Ran `ipconfig /all` on Client-1 to ensure the DNS was properly configured to DC-1’s IP address.

   ![Screenshot Placeholder: ipconfig /all Output](#)

### 3. Installing and Configuring Active Directory on DC-1

1. **Install Active Directory Domain Services**  
   Logged into **DC-1** and installed the **Active Directory Domain Services (AD DS)** role using Server Manager.

   ![Screenshot Placeholder: AD DS Installation](#)

2. **Promote DC-1 to a Domain Controller**  
   After installing AD DS, promoted **DC-1** to a Domain Controller by creating a new forest named **mydomain.com**.

   ![Screenshot Placeholder: Promote DC-1 to Domain Controller](#)

3. **Restart DC-1 and Login to Domain**  
   After promoting DC-1 to a Domain Controller, restarted DC-1 and logged in using domain credentials:  
   - Username: `mydomain.com\labuser`

   ![Screenshot Placeholder: DC-1 Domain Login](#)

### 4. Creating a Domain Admin User

1. **Create Organizational Units (OUs)**  
   In **Active Directory Users and Computers (ADUC)**, created two Organizational Units (OUs):
   - `_EMPLOYEES`  
   - `_ADMINS`

   ![Screenshot Placeholder: OU Creation](#)

2. **Create a Domain Admin User**  
   Created a new user named **Jane Doe** with the username `jane_admin` and added her to the **Domain Admins** security group:  
   - Username: `jane_admin`  
   - Password: `Cyberlab123!`

   ![Screenshot Placeholder: Creating Domain Admin User](#)

3. **Login as Domain Admin**  
   Logged out of the system and reconnected to DC-1 using the new domain admin credentials:  
   - Username: `mydomain.com\jane_admin`

   ![Screenshot Placeholder: Admin Login](#)

---

## Conclusion
In this project, I successfully set up an Active Directory environment using Azure Virtual Machines. The configuration included creating a Domain Controller (DC-1), setting up a new forest, configuring a client machine (Client-1), and adding a Domain Admin user. This configuration demonstrates the fundamentals of AD setup and user management in a cloud environment.
