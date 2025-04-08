---
title: lodctr
description: Reference article for the lodctr command, which allows you to register or save performance counter name and registry settings in a file and designate trusted services.
ms.topic: reference
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
ms.author: jgerend
author: robinharwood
manager: mtillman
ms.date: 10/16/2017
---

# lodctr



Allows you to register or save performance counter name and registry settings in a file and designate trusted services.

## Syntax

```
lodctr <INI-filename>  [/C:<filename>]  [/H:<filename>] [L:<LangID>] [/s:<Backup-filename>] [/R] [/R:<Backup-Filename] [/T:<service-name>] [/Q] [/Q:<Service-Name>] [/E:<Service-Name>] [/D:<Service-Name>] [/M:<Counter-Manifest [<Installation-Path<]] [/?]
 ```

### Parameters

| Parameter | Description |
| --------- | ----------- |
| `<INI-filename>` | Installs counter text strings. INI-filename is the name of theinitialization file that contains the counter name definitions and explain text for an extensible counter DLL. |
| `<filename>` | Specifies the name of the initialization file that registers the performance counter name settings and explanatory text. |
| /C:`<filename>` | Upgrades counter text strings using <filename>. |
| /H:`<filename>` | Upgrades help text strings using <filename>. |
| /L:`<LangID>` | Specifies the language for the /C and /H commands. |
| /S:`<Backup-filename>` | Specifies the name of the file to which the performance counter registry settings and explanatory text are saved. |
| /R | Rebuilds perf registry from scratch based on current registry settings and backup INI files.**Warning:** If you use this command, you'll overwrite all performance counter registry settings and explanatory text, replacing them with the default configuration. 3rd Party counters might require reinstallation. |
| /R:`<filename>` | Restores perf registry strings & info using <filename>.<p>**Warning:** If you use this command, you'll overwrite all performance counter registry settings and explanatory text, replacing them with the configuration defined in the specified file. |
| /t:`<servicename>` | Sets the specified performance counter provider as trusted. |
| /Q | Displays performance counter provider information. |
| /Q:<Service-Name> | Displays performance counter provider information for a specific provider. |
| /E:<service-name> | Enables the performance counter provider. |
| /D:<service-name> | Disables the performance counter provider. |
| /M:<Counter-Manifest> [<Installation-Path>] | Installs a v2.0 performance counter provider using the specified XML manifest. The installation requires a full path to the DLL containing the performance counter resources (localized  strings). The path to the DLL will be determined as follows: If the applicationIdentity attribute in the manifest is a full path, that will be used. Otherwise, if <Installation-Path> is provided and is a full path, that will be used. Otherwise, if <Counter-Manifest> is a full path, the directory from <Counter-Manifest> will be combined with the DLL name from the applicationIdentity attribute in the manifest. Otherwise, the current directory will be combined with the DLL name from the applicationIdentity attribute in the manifest.
| /? | Displays help at the command prompt. |

#### Remarks

- If the information that you supply contains spaces, use quotation marks around the text (for example, "file name 1"). 

### Examples

To save the current performance registry settings and explanatory text to file *"perf backup1.txt"*, type:

```
lodctr /s:"perf backup1.txt"
```

To rebuilt performance counter setting from system backup store type: 

```
lodctr /R
```

To query the current status of the Counter "PerfDisk", type:

```
lodctr /q:PerfDisk
```

If you want to disable the PerfDisk-Counter type:
Note, this will create a registry entry "Disable Performance Counters" with a value of 1 below the Registry-Key related to the PerfDisk Object. This is located in HKLM\SYSTEM\CurrentControlSet\Services\PerfDisk\Performance. Once specific counters are disabled, you will encounter an error when opening Performance Monitor as the default view of Performance Monitor is providing you with a system summary that contain information form Memory, Network, CPU and Disk. 
![image](https://github.com/user-attachments/assets/45652c54-0042-4ad0-b33c-a5a629948a2c)

```
lodctr /d:PerfDisk
```

If you want to enable the PerfDisk-Counter type:
Note, this will delete an existing registry entry "Disable Performance Counters" below the Registry-Key related to the PerfDisk Object. This is located in HKLM\SYSTEM\CurrentControlSet\Services\PerfDisk\Performance.

```
lodctr /e:PerfDisk
```


## Related links

- [Command-Line Syntax Key](command-line-syntax-key.md)
