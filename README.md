## Windows-11-Tweaks
Kleine Sammlung von Kommandos für jeden Tag, die man immer wieder sucht, vor allem jetzt in der Umstellungsphase.

## Upgrade
Einschränkungen beseitigen. Am besten die beiden REG-Dateien speichern und in die ISO-Datei integrieren. Dann kann man sie währen des Installationsprozesses aktivieren z.B: `REG IMPORT ByPass.reg` `oder AllowTelemetry.reg`.

### Bypass TPM, CPU, SecureBoot usw.
ByPass.reg
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
AllowInplace.reg
### AllowInplace
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup]
"AllowUpgradesWithUnsupportedTPMOrCPU"=dword:00000001
