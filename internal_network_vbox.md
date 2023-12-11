### Active Directory using VirtualBox

**Prerequisites:**
- Oracle VirtualBox
- ISO Files:
  - Windows 10 or Windows 11
  - Windows Server 2019
  - pfSense

**Initial Setup:**

1. **AD User (Windows 10/Windows 11):**
   - 2+ Cores for CPU
   - 4+ GB of RAM
   - 32+ GB of storage
   - Set up the adapter as Internal Network

2. **Windows Server:**
   - 2+ Cores for CPU
   - 8+ GB of RAM
   - 32+ GB of Storage
   - Set up the adapter as Internal Network

3. **pfSense:**
   - 1 or 2 Cores for CPU
   - 2 GB of RAM
   - 16+ GB of Storage
   - Set up Adapter #2 as Internal Network

**pfSense Configuration:**

- Perform a default installation of pfSense.
- Choose "Set Interface(s) IP Address" and:
  - Choose "LAN (em1 – static)".
  - Configure IPv4 address for LAN interface as "192.168.1.1/24".
  - Configure DHCP for LAN: No.
  - Configure IPv6 for LAN: No.
  - Enable DHCP server on LAN.
  - Set the IPv4 client range: 192.168.1.2 to 192.168.1.254.
- Finish the setup from the web interface on the AD User machine at [https://192.168.1.1/](https://192.168.1.1/).
  - During general setup, add DNS servers 8.8.8.8 and 8.8.4.4.

**Windows Server Configuration:**

- Perform a default Windows Server 2019 installation, choosing Standard with the Desktop Experience.
- Hostname: Windows2019
- Timezone: (UTC-05:00) Eastern Time (US & Canada)
- Network Configuration:
  - Static IP: 192.168.1.2
  - Subnet: 255.255.255.0
  - Gateway: 192.168.1.1
  - DNS: 8.8.8.8, 8.8.4.4
- Install Active Directory and DNS:
  - In Server Manager, add roles: Active Directory Domain Services, DNS Server.
- Promote the Server to a Domain Controller:
  - In Server Manager, click "Promote this server to a domain controller".
  - Choose "Add a new forest" and set the root domain name to "active.directory.local".
  - Set a password and proceed with the default options.

- Create an Active Directory user:
  - In Server Manager, go to "Active Directory Users and Computers".
  - Expand the active.directory.local domain.
  - Right-click on "Users" and click New > User.
  - Create a user named "Test" with the password "P@ssw0rd" or your preferred password.

**AD User Configuration:**

- Perform a default Windows 10 installation.
- Hostname: Windows10
- Timezone: (UTC-05:00) Eastern Time (US & Canada)
- Network Configuration:
  - Static IP: 192.168.1.3
  - Subnet: 255.255.255.0
  - Gateway: 192.168.1.1
  - DNS: 192.168.1.2, 8.8.8.8

- Connect to the Active Directory Domain:
  - Option 1:
    - Go to Settings > Accounts > Access work or school.
    - Click "Join this device to a local Active Directory domain".
    - For the domain name, type "ACTIVE".
    - Enter "Test" for the username and the chosen password.
  - Option 2:
    - Open "Advanced System Settings", go to "Computer Name", and click "Change".
    - Click the "Domain" button and type "ACTIVE".
    - Enter "Test" for the username and the chosen password.
