### Windows Server / Enterprise Guidance
- In an enterprise Windows environment, never disable [Credential Guard](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard-manage).  This feature helps prevent the most common types of attacks against Active Directory.  
- Out of the box, Microsoft Certificate Services computer templates do not utilize client TPM to protect certificate private keys.  If you are using computer certificate authentication to protect your network and not using TPM, an attacker can more easily copy a valid certificate to a machine of their choosing to be granted access. [Here is a quick setup guide I created to make the necessary change.](https://github.com/Xorlent/Cybersec-Links/blob/main/Configuring-TPM-Certs.md)  
- The Active Directory Kerberos ticket granting account (KRBTGT) password should be reset periodically to help prevent golden ticket attacks.  [Further details can be found here](https://github.com/microsoft/New-KrbtgtKeys.ps1/tree/master/v1)
- Ensure you are monitoring/notifying on users added or removed from the following [AD security groups](https://github.com/Xorlent/Cybersec-Links/blob/main/Sensitive-AD-Groups.txt)
### Windows Client Guidance
- Disable the following services that do not have DEP protection on all Windows desktop OS machines
  - "Windows Phone IP over USB Transport (IpOverUsbSvc)"
  - "Intel(R) Management Engine WMI Provider Registration"
- You can check for other running services or applications missing DEP by opening Task Manager, selecting "Details," clicking on the column headers and adding "Data execution prevention" to the column list
### Firewall Deep Packet Inspection
- Many firewalls with DPI only support inspection of certain protocol versions, like TLS 1.2 and 1.3  
  - A common attacker circumvention technique is to force a client to connect on an unsupported protocol, bypassing inspection  
  - Be sure to configure your firewall to block unsupported and insecure protocols, e.g. SSL 1.0, 2.0, 3.0, TLS 1.0, 1.1
### AppLocker Authenticode Hash Generation
- To create AppLocker rules from a list of files, use the PowerShell command, [Get-AppLockerFileInformation](https://learn.microsoft.com/en-us/powershell/module/applocker/get-applockerfileinformation?view=windowsserver2022-ps)
