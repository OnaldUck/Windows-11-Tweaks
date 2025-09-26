## Windows-11-Tweaks
Kleine Sammlung von Kommandos für jeden Tag, die man immer wieder sucht, vor allem jetzt in der Umstellungsphase.

## Upgrade
Einschränkungen beseitigen

### Bypass TPM usw.

```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\SOFTWARE\Microsoft\PCHC]
"UpgradeEligibility"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig]
"BypassTPMCheck"=dword:00000001
"BypassSecureBootCheck"=dword:00000001
"BypassRAMCheck"=dword:00000001
"BypassStorageCheck"=dword:00000001
"BypassCPUCheck"=dword:00000001
"BypassDiskCheck"=dword:00000001
```
