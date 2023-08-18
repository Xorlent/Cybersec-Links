#### What is NPS?
- Included in your Windows Server licensing is a role called, [Network Policy Server](https://learn.microsoft.com/en-us/windows-server/networking/technologies/nps/nps-top).  NPS is most commonly leveraged for RADIUS authentication of Wi-Fi and Wired network clients (802.1x).  
- Although relatively simplistic and limited in terms of client visibility and reporting, it can help smaller organizations implement better network controls for minimal cost and effort.  
- Alongside Microsoft Certificate Services, a properly built NPS deployment can be functionally competitive versus products like Cisco ISE, Aruba Clearpass, FortiNAC/Bradford -- all without the significant cost and operational complexities.  
- Deploying and configuring NPS in a test bed, even before doing research and selection on a 3rd party product will enable your team to design and test a working 802.1x solution in your environment which provides clarity as to the features and functionality that is truly needed.  In fact, NPS can continue to be used as a fail-over RADIUS host should the 3rd party product require maintenance or fail for any reason.
  
#### If you are thinking about NAC:
- *Priorities.*  Do you still have Server 2012 or Windows 8.1 and earlier systems in your fleet?  Address these first.  
  - In-place upgrades can sometimes be an option.  Here is guidance for [Windows Server 2012R2/2016 to 2019](https://github.com/Xorlent/Cybersec-Links/blob/main/Windows-Server-In-Place-Upgrade.md)  
- A Microsoft Certificate Services deployment should be your team's first step towards NAC.  Even if you do not currently plan to use a PKI, getting a working, tested, and documented certificate system setup running in your environment should be a priority.  
- If you have an older Certificate Services deployment with SHA1-based root CA and/or sub CA certificate signatures, [you need to address this](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/sha1-key-migration-to-sha256-for-a-two-tier-pki-hierarchy/ba-p/400338).  
- Start small and simple.  
  - If you have a Wi-Fi deployment that is RADIUS authentication-compatible, migrate your private SSIDs to use Microsoft NPS.  
  - Write down all of the possible failure scenarios and simplify or adjust the design to make these easier (read: quicker) to recover from.  
  - Remember that redundancy and high availability adds complexity; usually you can get more mileage out of proper design.  Most vendors allow you to specify multiple RADIUS servers to provide simple fail-over capability.

#### NPS on Windows Server 2019:
- If, despite all your best efforts, the RADIUS server does not seem to be responding to client requests, it's likely Microsoft's problem.  Fix the IAS/NPS Windows Firewall service access by running the following from an elevated command prompt:  
  ```sc sidtype IAS unrestricted```

#### Other NPS tips:
- Always make logging the first thing you configure.  Log settings can be found under the "Accounting" option in the Network Policy Server management console.
  - If you plan on trying the NPS log parser / visualizer I created, you will want to configure daily logs in the ODBC format.
- If you are setting up 802.1x wired authentication, you will want to configure a test user on the switches so they can detect when a RADIUS host is offline.  These tests will result in a lot of log entries you probably don't want to see.
  - In regedit, navigate to ```HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\IAS\Parameters```
  - Add an REG_SZ key called, "ping user-name"
  - Set the value to the name of your RADIUS test account

