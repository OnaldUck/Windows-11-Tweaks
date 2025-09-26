# Windows-11-Tweaks
Kleine Sammlung von Kommandos für jeden Tag, die man immer wieder sucht, vor allem jetzt in der Umstellungsphase.

## Upgrade
Einschränkungen beseitigen. Am besten die beiden REG-Dateien speichern und in die ISO-Datei integrieren. Dann kann man sie währen des Installationsprozesses aktivieren z.B: `REG IMPORT ByPass.reg` oder `AllowTelemetry.reg`.

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

### AllowInplace
Erlaube InplaceUpgrade ohne alle Voraussetzungen zu erfüllen

AllowInplace.reg
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup]
"AllowUpgradesWithUnsupportedTPMOrCPU"=dword:00000001
```

## Inplace von Win10 zum Windows 11 LTSC
Die Installation starten, dann die REG-Datei ausführen, dann weiter machen.

Inplace-Win10-to-Win11LTSC.reg
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion]
"CurrentBuild"="19044"
"CurrentBuildNumber"="19044"
"EditionID"="enterpriseS"
"ProductName"="Windows 10 Enterprise LTSC 2021"
"ReleaseId"="21H2"
"DisplayVersion"="21H2"
```

### Windows 11 ohne Microsoft-Konto einzurichten
Um Windows 11 ohne Microsoft-Konto einzurichten, drücken Sie während des Einrichtungsprozesses
`SHIFT + F10`, um eine Eingabeaufforderung zu öffnen, und geben Sie dort `start ms-cxh:localonly` ein, gefolgt von der Eingabetaste, um die Option für ein lokales Konto freizuschalten. 

# Nach der Installation
## Reservierten Speicher deaktivieren

```
dism /Online /Get-ReservedStorageState 
dism /Online /Set-ReservedStorageState /State:Disabled
```

## Empfohlen im Startmenü entfernen

Empfohlen entfernen W11.reg
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer]
"HideRecommendedSection"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\current\device\Start]
"HideRecommendedSection"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\current\device\Education]
"IsEducationEnvironment"=dword:00000001
```

# Computerschutz deaktivieren #
`PS1:Disable-ComputerRestore -Drive C:\`
