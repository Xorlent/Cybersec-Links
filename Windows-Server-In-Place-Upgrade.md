## Windows Server 2012R2/2016 to 2019 In-Place Upgrade Procedure  
*Your mileage may vary!*  
  
1.	Prepare your change management request.  
    a.	The upgrade maintenance window should be at least 3 hours.  
    b.	This process is not valid or recommended for domain controllers, ADFS, Exchange, or Microsoft NPS  
2.	Check OS drive available space.  Extend volume to ensure at least 45GB free.  
3.	Ensure host has latest updates:  
    a.	At a minimum, it should be patched to March 2023 with the latest Servicing Stack update.  
    b.	Upgrade any MSSQL instances to a current supported version and apply the latest cumulative update.  
4.	Remove or upgrade any outdated or unused software and reboot.  
5.	Running as a VMWare guest?  Ensure VMWare Tools is updated to version 11.3.0 at a minimum, 11.3.5 recommended.  
6.	Take a full backup and then a VM snapshot.  
7.	At this point, it is recommended to run dism in an elevated command prompt. Reboot if issues were resolved.  
    dsim /online /cleanup-image /restorehealth  
8.	Stop all non-essential services and disable any scheduled tasks that may interfere with the maintenance window.  
9.	Copy the Windows Server 2019 Standard ISO to the host’s D or C drive.  
10.	Right-click the copied ISO file, select “Properties” and click “Unblock”  
11.	Click “Ok”  
12.	Launch task manager and ensure no other users are logged in.  
13.	Right-click the copied ISO file and select, “Mount.”  
14.	Double-click setup.exe.  
15.	Allow the welcome screen default (Download Updates) and click, “Next.”  
16.	IMPORTANT: Select “Windows Server 2019 Standard (Desktop Experience)” and click “Next.”  
17.	Accept license terms and click “Next.”  
18.	Select “Keep personal files and apps” and click “Next.”  
19.	If a warning appears about VMWare Tools components/drivers, they are safe to ignore (confirm) if you have the latest 11.3 release installed per step 6.  Any other driver or application warnings should be researched fully before continuing.  
20.	Click, “Install” when prompted.  It can take up to 75 minutes for this process to complete.  
21.	If the install errors at 21%, it is possible you have OS volume corruption.  Verify security is correct first:  
    a.	From an admin command prompt at C:\>  
        i.	sfc /scannow  
        ii.	secedit /configure /cfg %windir%\inf\defltbase.inf /db defltbase.sdb /verbose  
        iii.	Reboot  
        iv.	Delete C:\$WINDOWS.~BT  
        v.	Begin again at step 14 of this document.  If it still fails, continue to vi.  
        vi.	Backup any user profile data that needs to be preserved, as this process is destructive to these folders.  
        vii.	From C:\> icacls * /q /c /t /reset  
        viii.	Open File Explorer and browse into all root folders.  If prompted that the Recycle Bin is corrupt, select, “Empty”  
        ix.	Reboot  
        x.	Open Control Panel -> System -> Advanced System Settings -> User Profiles Settings  
            1.	Delete all except the Default Profile so they can be recreated with default permissions.  
        xi.	Reboot  
        xii.	Delete C:\$WINDOWS.~BT  
        xiii.	Begin again at step 14 of this document.  If it fails at this point, you may need to perform a fresh install of 2019 and migrate to the new server.  
22.	Connect (console or RDP) to the server after waiting 40-75 minutes  
23.	With Server Manager open, click “Local Server” and ensure Operating System Version is “Microsoft Windows Server 2019 Standard.”  
24.	Open Windows Updates and apply the latest available updates and reboot if necessary.  
25.	Open Control Panel – System – Activate Windows.  
26.	Select “Change Product Key.”  
27.	Enter a valid MAK and activate Windows.  
28.	Review Event Viewer and assess any recent error logs.  
29.	Re-enable any services and scheduled tasks that were disabled prior to the upgrade.  
30.	Adjust Windows Firewall inbound rules as necessary.  
    a.	Inbound ping requests (File and Printer Sharing (Echo Request - ICMPv4-In) will be disabled by default; you may want to enable this.  
31.	Ensure all applications are working as expected.  
32.	Remove the Windows Server 2019 ISO.  
33.	Complete.  Take another backup and delete any VM shapshots.
