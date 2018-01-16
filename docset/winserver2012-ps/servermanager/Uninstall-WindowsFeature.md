---
external help file: Microsoft.Windows.ServerManager.PowerShell.dll-Help.xml
ms.assetid: FF3743EB-D209-44B9-93EC-7118ABE14EDE
online version: 
schema: 2.0.0
---

# Uninstall-WindowsFeature

## SYNOPSIS
Uninstalls specified Windows Server roles, role services, and features from a computer that is running Windows Server 2012.
By adding the Remove parameter, also deletes feature files, or payload, from a computer.
This cmdlet replaces Remove-WindowsFeature, the cmdlet that was used to uninstall roles, role services, and features in Windows Server 2008 R2.

## SYNTAX

### RunningComputer (Default)
```
Uninstall-WindowsFeature [-Name] <Feature[]> [-Restart] [-IncludeManagementTools] [-Remove]
 [-ComputerName <String>] [-Credential <PSCredential>] [-LogPath <String>] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

### VhdPath
```
Uninstall-WindowsFeature [-Name] <Feature[]> [-Vhd <String>] [-IncludeManagementTools] [-Remove]
 [-ComputerName <String>] [-Credential <PSCredential>] [-LogPath <String>] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION
The `Uninstall-WindowsFeature` cmdlet uninstalls and optionally removes specified roles, role services, and features from a computer that is running Windows Server 2012, or from an offline virtual hard disk (VHD) on which Windows Server 2012 is installed.
This cmdlet works similarly to the Remove Roles and Features Wizard in Server Manager, with an important exception: by default, management tools are not uninstalled when you run the `Uninstall-WindowsFeature` cmdlet; you must add the `IncludeManagementTools` parameter to uninstall associated management tools.

This cmdlet requires elevation; you must be running a Windows PowerShell session as an administrator to use this cmdlet.

## EXAMPLES

### EXAMPLE 1
```
PS C:\> Get-WindowsFeature | Where-Object -FilterScript { $_.Installed -Eq $TRUE } | Uninstall-WindowsFeature
```

This example uninstalls any roles or features that are currently installed on the target server.

### EXAMPLE 2
```
PS C:\> Uninstall-WindowsFeature -Name Web-Server -ComputerName Server1 -Credential contoso\user1
```

This example removes Web Server (IIS) from Server1, including all role services.
The user account specified to perform the operation is contoso\user1.

### EXAMPLE 3
```
PS C:\> Get-WindowsFeature | Where-Object -FilterScript { $_.Installed -Eq $FALSE } | Uninstall-WindowsFeature -Remove
```

This example deletes the feature files for any roles or features that currently are not installed on the local server.

## PARAMETERS

### -ComputerName
Uninstalls and optionally removes one or more rrsandf_plural from a specified remote computer.
This parameter accepts only one computer name.
If this parameter is not added, or no computer name is specified, the default target is the local computer.

Valid values for the parameter include a NetBIOS name, an IP address, or a fully qualified domain name of a remote computer that is running Windows Server 2012.

To use an IP address of a remote computer as the value of this parameter, your command must include the `Credential` parameter.
The computer must either be configured for HTTPS transport, or the IP address of the remote computer must be included in the WinRM TrustedHosts list on the local computer.
For information about adding a computer name to the WinRM TrustedHosts list, see "How to Add a Computer to the Trusted Host List" in about_Remote_Troubleshootinghttp://go.microsoft.com/fwlink/p/?LinkId=135188.

```yaml
Type: String
Parameter Sets: (All)
Aliases: Cn

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a user account that has access rights to perform this action.
If the parameter is not added, or no value is specified, the default value of this parameter is the current user.
Enter a user name in one of the following formats.
Quotation marks are optional.

-- "UserName" 

 

 -- "Domain\User" 

 

 -- "User@Domain.com" 

 

 -- A Credential object returned by the Get-Credentialhttp://go.microsoft.com/fwlink/p/?LinkId=113311 cmdlet.

If a user name is entered, then a prompt for a password is displayed.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IncludeManagementTools
Specifies the uninstallation of all applicable management tools along with the roles, role services, or features that are specified in the `Name` parameter.
Note that by default, management tools are not uninstalled when you run the `Uninstall-WindowsFeature` cmdlet; you must add this parameter to uninstall associated management tools.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LogPath
Specifies a name and path to a log file.
Add this parameter if the results of this cmdlet must be stored in a log.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
Specifies a list of features to uninstall.
This parameter does not support wildcard characters.

```yaml
Type: Feature[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Remove
Deletes feature files for the specified rrsandf_plural from the side-by-side store, located at %SystemDrive%:\Windows\WinSxS.
If the feature is not yet uninstalled, the command uninstalls the feature.

When you delete feature files, features that depend upon the files you remove are also deleted.
When you delete feature files for a subfeature, and no other subfeatures for the parent feature are installed, then files for the entire parent role or feature are deleted.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Restart
Specifies that the target computer is restarted automatically, if a restart is required by the uninstallation process for the specified roles or features.
This parameter cannot be used with the `Vhd` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: RunningComputer
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Vhd
Specifies the path to an offline VHD.
The path can either point to a VHD file, or to a location on which the VHD is already mounted by using Deployment Image Servicing and Management (DISM) tools.

The VHD can be on a local disk on the target computer, or on a network shared folder.
If the VHD is in a network shared folder, then the value of this parameter is a UNC path to the VHD.
In this case, the computer account of the computer that you are using to mount the VHD must have read and write permissions (Read/Write permissions in the File Sharing dialog box, or Full Control on the Security tab of the folder Properties dialog box) on the shared folder, or the VHD will not be accessible.
Local loopback UNC paths are not supported.
Use either of the following formats for the computer account: DOMAIN\SERVERNAME$ or SERVERNAME$.

Add the `ComputerName` parameter to specify the target computer you want to use to mount the VHD.
If the `ComputerName` parameter is not specified, then the local computer is used.
The computer that you are using to mount the VHD must be running Windows Server 2012.
Any local path, such as D:\myFolder, that is specified by using this parameter is always relative to the target computer.

```yaml
Type: String
Parameter Sets: VhdPath
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String[]

### Microsoft.Windows.ServerManager.Commands.Feature[]

## OUTPUTS

### Microsoft.Windows.ServerManager.Commands.FeatureOperationResult

## NOTES

## RELATED LINKS

[Get-WindowsFeature](./Get-WindowsFeature.md)

[Install-WindowsFeature](./Install-WindowsFeature.md)

[Enable-ServerManagerStandardUserRemoting](./Enable-ServerManagerStandardUserRemoting.md)

[Disable-ServerManagerStandardUserRemoting](./Disable-ServerManagerStandardUserRemoting.md)
