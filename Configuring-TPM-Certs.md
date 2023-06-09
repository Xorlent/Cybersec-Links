# Configuring a TPM-based computer certificate template  
  
*These steps assume Active Directory functional level is 2012R2 or higher, a working CA is deployed, clients have working TPM, and you are familiar with Microsoft Certificate Services.*  
1. Copy a working computer certificate template  
2. General tab  
  a. Name the certificate template  
3. Compatibility  
  a. Upgrade Certificate Authority compatibility to 2008 R2  
  b. Upgrade Certificate recipient compatibility to Windows 7/2008R2  
4. Cryptography  
  a. Change Provider Category to “Key Storage Provider”  
  b. Algorithm: RSA  
  c. Minimum key size: 2048  
  d. Select, “Requests must use one of the following providers”  
  e. Check only “Microsoft Platform Crypto Provider”  
  f. Thumbprint: SHA256  
5. Click OK  
6. Security  
  a.Ensure security settings are appropriate  
    *Hosts that need to enroll should have only the following rights:*  
      - Enroll  
      - Autoenroll  
7. Request Handling  
  a. Ensure all selectable options are unchecked  
8. Publish the template.  At this step you can publish a group policy object to have the machines auto-enroll.  
