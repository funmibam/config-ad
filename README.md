# Configuring Active Directory with Azure VMs

## Lab Overview
This lab involved configuring an Active Directory (AD) environment using Azure Virtual Machines (VMs) and Virtual Network (VNet). The project setup included creating a Domain Controller (DC-1) on a Windows Server 2022 machine and a client machine (Client-1) on Windows 10. The domain was configured, and a Domain Admin account was created. 

## Steps Performed

### 1. Setup Domain Controller in Azure

1. **Create a Resource Group**  
   Created a new Resource Group in the Azure portal to organize all resources related to the project.
   

  <img width="727" alt="Screenshot 2024-10-16 130655" src="https://github.com/user-attachments/assets/01830928-7caa-4057-bb17-09199431ff24">
  


2. **Create a Virtual Network and Subnet**  
   Created a Virtual Network (VNet) and Subnet for communication between DC-1 and Client-1.
   

  <img width="720" alt="Screenshot 2024-10-15 102245" src="https://github.com/user-attachments/assets/c9731764-607e-4c63-9299-370655e1ad30">
  


3. **Create the Domain Controller VM**  
   I created a Virtual Machine running **Windows Server 2022**, named **DC-1**.  
   - Username: `labuser`  
   - Password: `Cyberlab123!`


  <img width="727" alt="Screenshot 2024-10-16 133130" src="https://github.com/user-attachments/assets/5bc1aad0-86bf-4b17-84e2-99668b02632d">





4. **Set Static Private IP for DC-1**  
   Set the Network Interface (NIC) of DC-1 to have a **static private IP address** for DNS consistency.

   
   

 <img width="438" alt="Screenshot 2024-10-15 110201" src="https://github.com/user-attachments/assets/c77228e3-1085-4b2a-bd45-009d0351048b">

 


5. **Disable Windows Firewall on DC-1**  
   Disabled the Windows Firewall on DC-1 for connectivity testing.
   

### 2. Setup Client-1 in Azure

1. **Create Client-1 VM**  
   Created a Windows 10 VM, **Client-1**, with the same credentials as DC-1.  
   - Username: `labuser`  
   - Password: `Cyberlab123!`

     
<img width="677" alt="Screenshot 2024-10-16 135030" src="https://github.com/user-attachments/assets/936031ec-ac1a-4c24-b2f2-deb2ca5347e1">

  

2. **Configure DNS on Client-1**  
   Set Client-1's DNS to point to DC-1’s static private IP for proper domain resolution.
   
   
<img width="892" alt="Screenshot 2024-10-15 111632" src="https://github.com/user-attachments/assets/6d955e2d-ebb6-487c-8e05-873014ac748f">



4. **Restart Client-1 and Test Connectivity**  
   Restarted Client-1 and successfully pinged DC-1’s private IP, confirming connectivity.
   

  <img width="576" alt="Screenshot 2024-10-16 133538" src="https://github.com/user-attachments/assets/e0f689c9-e47f-4482-bc49-df9e1f89723d">
  


5. **Verify DNS Settings on Client-1**  
   Ran `ipconfig /all` on Client-1 to ensure the DNS was properly configured to DC-1’s IP address.
   
   
<img width="493" alt="image" src="https://github.com/user-attachments/assets/bba31466-9a64-4d5c-a459-784e6e24f3e3">


### 3. Installing and Configuring Active Directory on DC-1

1. **Install Active Directory Domain Services**  
   Logged into **DC-1** and installed the **Active Directory Domain Services (AD DS)** role using Server Manager.
   

<img width="688" alt="Screenshot 2024-10-16 134821" src="https://github.com/user-attachments/assets/c129e00a-c087-45a3-bf18-c867de039f45">


2. **Promote DC-1 to a Domain Controller**  
   After installing AD DS, promoted **DC-1** to a Domain Controller by creating a new forest named **mydomain.com**.


  <img width="487" alt="Screenshot 2024-10-16 134225" src="https://github.com/user-attachments/assets/b654afa6-5c14-42b4-a89f-c0a1f1bc0e07">


3. **Restart DC-1 and Login to Domain**  
   After promoting DC-1 to a Domain Controller, restarted DC-1 and logged in using domain credentials:  
   - Username: `mydomain.com\labuser`



### 4. Creating a Domain Admin User

1. **Create Organizational Units (OUs)**  
   In **Active Directory Users and Computers (ADUC)**, created two Organizational Units (OUs):
   - `_EMPLOYEES`  
   - `_ADMINS`

2. **Create a Domain Admin User**  
   Created a new user named **Jane Doe** with the username `jane_admin` and added her to the **Domain Admins** security group:  
   - Username: `jane_admin`  
   - Password: `Cyberlab123!`
  
     
   - <img width="597" alt="Screenshot 2024-10-16 134427" src="https://github.com/user-attachments/assets/6c6ef88c-b0f7-498a-bd97-11674932d36d">

  

3. **Login as Domain Admin**  
   Logged out of the system and reconnected to DC-1 using the new domain admin credentials:  
   - Username: `mydomain.com\jane_admin`

   <img width="310" alt="Screenshot 2024-10-16 132456" src="https://github.com/user-attachments/assets/d5aa5453-6d4b-46a2-b49d-7d762c5d4a54">


---

## Conclusion
In this project, I successfully set up an Active Directory environment using Azure Virtual Machines. The configuration included creating a Domain Controller (DC-1), setting up a new forest, configuring a client machine (Client-1), and adding a Domain Admin user. This configuration demonstrates the fundamentals of AD setup and user management in a cloud environment.
