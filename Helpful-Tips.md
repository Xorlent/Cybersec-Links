- In an enterprise Windows environment, never disable [Credential Guard](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard-manage).  This feature helps prevent the most common types of attacks against Active Directory.  
- Out of the box, Microsoft Certificate Services computer templates do not utilize client TPM to protect certificates.  If you are using computer certificate authentication to protect your network and not using TPM, an attacker can simply copy a valid certificate to a machine of their choosing to be granted access.  
- 