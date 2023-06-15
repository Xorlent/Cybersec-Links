# Configuring computer certificate template for TPM attestation  
_from (https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)_  
  
*These steps assume a working CA deployment and familiarity with Microsoft Certificate Services.*  
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
6. Re-open the new template - Step is required due to a UI bug  
7. Compatibility  
  a. Upgrade Certificate Authority compatibility to 2012R2  
  b. Upgrade Certificate recipient compatibility to Windows 10/2016  
8. Key Attestation  
  a. Select “Required”  
  b. Select “Perform attestation based on:” Hardware Key  
9. Security  
  a.Ensure security settings are appropriate  
    *Hosts that need to enroll should have only the following rights:*  
      - Enroll  
      - Autoenroll  
10. Request Handling  
  a. Ensure all selectable options are unchecked  
11. If not yet done, the final step needed to configure the CA to issue using TPM key attestation for appropriately configured cert templates (create the C:\CAEndorsementKeyList folder first):  
  a. Grant read-only permissions to the computer account of the Certificate Services server  
  b. From an admin command prompt:  
     ```certutil.exe -setreg CA\EndorsementKeyListDirectories +"C:\CAEndorsementKeyList"```  
  c. Reboot or restart Certificate Services  
13. Issue the following on all machines that will be requesting TPM-endorsed certificates  
  *Script this process for a deployment*  
  a. Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
  b. Copy the hash value and paste as the complete filename of a 0 byte file in C:\CAEndorsementKeyList on the issuing CA server  
14. Publish the template  
