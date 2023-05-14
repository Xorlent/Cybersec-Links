#### What is NPS?
- Included in your Windows Server licensing is a role called, [Network Policy Server](https://learn.microsoft.com/en-us/windows-server/networking/technologies/nps/nps-top).  NPS is most commonly leveraged for RADIUS authentication of Wi-Fi and Wired network clients (802.1x).  
- Although relatively simplistic and limited in terms of client visibility and reporting, it can help smaller organizations implement better network controls for minimal cost and effort.  
- A properly built NPS deployment with Microsoft Certificate Services can be functionally competitive versus products like Cisco ISE, Aruba Clearpass, FortiNAC/Bradford -- all without the significant cost and operational complexities.  
- Deploying and configuring NPS in a test bed, even before doing research and selection on a 3rd party product will enable your team to design and test a working 802.1x solution in your environment which provides clarity as to the features and functionality that is truly needed.  In fact, NPS can continue to be used as a fail-over RADIUS host should the 3rd party product go offline for any reason.
  
#### If you are thinking about NAC:
- *Prioritize.*  Do you still have Server 2012 or Windows 8.1 and earlier systems in your fleet?  Address this first.  
- I encourage your team to deploy, configure, and audit Microsoft Certificate Services as a first step.  
- Certificate Services is needed for most NAC deployments.  Even if you do not immediately plan to use a PKI, getting a working, tested, and familiar setup running in your environment should be a priority.  
- If you have an older Certificate Services deployment with SHA1-based root CA and/or sub CA certificate signatures, [you need to address this](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/sha1-key-migration-to-sha256-for-a-two-tier-pki-hierarchy/ba-p/400338).  
- Start small and simple.  
  - If you have a Wi-Fi environment that can implement RADIUS authentication for access, do this first.
