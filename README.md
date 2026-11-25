# TrimKit

Builds a trimmed Windows installation ISO. `TrimKit.ps1` (internally named GDebloat) debloats a source Windows ISO, rebuilds the WIM and writes a new ISO. The ISO can include extra drivers, GSecurity files and the .NET Framework 3.5 (NetFx3) source.

## Contents

| Path | Purpose |
|------|---------|
| `TrimKit.ps1` | Main script. Removes components from the image, rebuilds the WIM and creates the ISO. |
| `Start.bat` | Elevates, then starts every `.ps1` file in its folder in alphabetical order. |
| `Drivers/` | Network adapter drivers and `SilentInstall.cmd`, which installs them. |
| `GSecurity/` | GSecurity files placed into the ISO (`Iso/sources/$OEM$/...`). |
| `NetFx3/` | .NET Framework 3.5 source. |

## Usage

Requires elevated 64-bit Windows PowerShell 5.1 and `oscdimg` from the Windows ADK.

```powershell
.\TrimKit.ps1 -SourceIso D:\Win11.iso -OutputIso D:\TrimKit.iso
```

| Parameter | Meaning |
|-----------|---------|
| `-SourceIso` | Source Windows ISO. |
| `-ImageIndex` | Image index in the WIM. Default `0`. |
| `-OutputIso` | Output ISO path. Default `GDebloat.iso` next to the script. The script stops if the file already exists. |
| `-WorkDirectory` | Drive used for working files. Default is the system drive. |
| `-OscdimgPath` | Path to `oscdimg.exe`. |
| `-DriverDirectory` | Drivers to add to the image. |
| `-GSecurityDirectory` | GSecurity files to add. |
| `-NetFx3Source` | .NET 3.5 source folder. |
| `-SkipAutoDrivers` | Skip automatic driver handling. |
| `-SkipGSecurity` | Skip adding GSecurity. |

The script removes Windows components and edits the image. Runtime behavior on the resulting Windows install is unverified, so test the ISO in a virtual machine first.
