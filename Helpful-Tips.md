### Windows Server / Enterprise Guidance
- In an enterprise Windows environment, never disable [Credential Guard](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard-manage).  This feature helps prevent the most common types of attacks against Active Directory.  
- Out of the box, Microsoft Certificate Services computer templates do not utilize client TPM to protect certificate private keys.  If you are using computer certificate authentication to protect your network and not using TPM, an attacker can more easily copy a valid certificate to a machine of their choosing to be granted access. [Here is a quick setup guide I created to make the necessary change.](https://github.com/Xorlent/Cybersec-Links/blob/main/Configuring-TPM-Certs.md)  
- The Active Directory Kerberos ticket granting account (KRBTGT) password should be reset periodically to help prevent golden ticket attacks.  [Further details can be found here](https://github.com/microsoft/New-KrbtgtKeys.ps1/tree/master/v1)
### Windows 10/11 Guidance
- If you have systems in your environment without TPM, you will need to get busy on a hardware refresh project
  - Windows 11 requires TPM 2.0
- Disable the following services that do not have DEP protection on all Windows desktop OS machines
  - "Windows Phone IP over USB Transport (IpOverUsbSvc)"
  - "Intel(R) Management Engine WMI Provider Registation"
- You can check for other running services or applications missing DEP by opening Task Manager, selecting "Details," clicking on the column headers and adding "Data execution prevention" to the column list
