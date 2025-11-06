# Windows-11-Tweaks
Kleine Sammlung von Kommandos für jeden Tag, die man immer wieder sucht, vor allem jetzt in der Umstellungsphase.

# Inhaltsverzeichnis

- [Upgrade](https://github.com/OnaldUck/Windows-11-Tweaks.git#Upgrade)
- [Windows 11 ohne Microsoft-Konto einzurichten](https://github.com/OnaldUck/Windows-11-Tweaks.git#Windows-11-ohne-Microsoft-Konto-einzurichten)
- [klassisches Kontextmenu](https://github.com/OnaldUck/Windows-11-Tweaks.git#klassisches-Kontextmenu)
- [klassisches Druckdialog](https://github.com/OnaldUck/Windows-11-Tweaks.git#klassisches-Druckdialog)
- [Reservierten Speicher deaktivieren](https://github.com/OnaldUck/Windows-11-Tweaks.git#Reservierten-Speicher-deaktivieren)
- [Empfohlen im Startmenü entfernen](https://github.com/OnaldUck/Windows-11-Tweaks.git#Empfohlen-im-Startmenü-entfernen)
- [XBox Apps deinstallieren](https://github.com/OnaldUck/Windows-11-Tweaks.git#XBox-Apps-deinstallieren)

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
Erlaube InplaceUpgrade ohne alle Voraussetzungen zu erfüllen.

AllowInplace.reg
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup]
"AllowUpgradesWithUnsupportedTPMOrCPU"=dword:00000001
```

## Inplace von Windows 10 zum Windows 11 LTSC
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
## klassisches Kontextmenu
```
reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```

## klassisches Druckdialog
```
reg add "HKCU\Software\Microsoft\Print\UnifiedPrintDialog" /v "PreferLegacyPrintDialog" /d 1 /t REG_DWORD /f
```

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

# XBox Apps deinstallieren #
In der Powershell aknn den XBox Apps Systemweit deinstallieren

```
PS1:
Get-AppxPackage -AllUsers *Microsoft.Xbox* | Remove-AppxPackage
Get-AppxPackage -AllUsers *Microsoft.XboxIdentityProvider* | Remove-AppxPackage
Get-AppxPackage -AllUsers *Microsoft.YourPhone* | Remove-AppxPackage
```
