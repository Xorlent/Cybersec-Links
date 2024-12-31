## Recommended EDR alert notification rules

### Exec or script downloaded via browser
#### Process
    w3wp.exe,cmdl32.exe,httpd.exe,tomcat6.exe,tomcat7.exe,tomcat8.exe,tomcat9.exe,tomcat.exe,tomcat10.exe,msedge.exe,firefox.exe,chrome.exe,iexplore.exe,opera.exe,putty.exe,filezilla.exe,brave.exe,chromium.exe

#### File written
    *.exe,*.msi,*.iso,*.img,*.ps1,*.psm,*.zip,*.rar,*.arc,*.7z,*.tar,*.vbs,*.wasm,*.vbe,*.vb,*.wsf,*.jar,*.ps,*.com*.cab,*.cmd,*.bat,*.cpl,*.lnk,*.reg,*.vbscript,*.ws,*.chm,*.py,*.svg

### Executables run
    rclone.exe,msdt.exe
