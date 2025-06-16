## Recommended EDR alert notification rules
_Other alerts can be helpful depending on the environment, but the following should work fairly well and not generate too much noise_

### Exec or script downloaded via browser
#### Browser process performing write
    w3wp.exe,cmdl32.exe,httpd.exe,tomcat6.exe,tomcat7.exe,tomcat8.exe,tomcat9.exe,tomcat.exe,tomcat10.exe,msedge.exe,firefox.exe,chrome.exe,iexplore.exe,opera.exe,putty.exe,filezilla.exe,brave.exe,chromium.exe

#### File extensions written by browser process
    *.exe,*.msi,*.iso,*.img,*.ps1,*.psm,*.zip,*.rar,*.arc,*.7z,*.tar,*.vbs,*.wasm,*.vbe,*.vb,*.wsf,*.jar,*.ps,*.com*.cab,*.cmd,*.bat,*.cpl,*.lnk,*.reg,*.vbscript,*.ws,*.chm,*.py,*.svg

### Executables run
#### This is the lite version; for a more complete list, see https://github.com/Xorlent/Risky-EXEs  
    rclone.exe,msdt.exe,wmic.exe,mshta.exe,certutil.exe,bitsadmin.exe,schtasks.exe,sc.exe,csc.exe,cscript.exe,wscript.exe
