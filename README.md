# update-openssh-windows
Few command lines to get OpenSSH updated manually.

# Download binary files from latest release
Get the latest release from this repo 
https://github.com/PowerShell/Win32-OpenSSH/releases<br>
Unzip it on a folder.

```$oldAcl = Get-Acl -Path C:\Windows\System32\OpenSSH\```

```$uname = $env:username```

```takeown.exe /a /r /f C:\Windows\System32\OpenSSH\```

```$openSshBins = (Get-ChildItem 'C:\WINDOWS\System32\OpenSSH\').Name```

```$perm = $uname + ":F"```

```$openSshBins | %{ icacls "C:\Windows\System32\OpenSSH\$_" /grant $perm /T }```

Path on this command takes binary downloaded files <br>
```$openSshBins | %{ Copy-Item -Path .\openssh\$_ -Destination C:\Windows\System32\OpenSSH\ }```

```$perm = $uname```

```$openSshBins | %{ icacls "C:\Windows\System32\OpenSSH\$_" /remove $perm /T }```

```Set-Acl -Path C:\Windows\System32\OpenSSH\ -AclObject $oldAcl```

Check OpenSSH version
```ssh -V```

Example output
```
PS C:\ > ssh -V
OpenSSH_for_Windows_8.1p1, LibreSSL 2.6.5
```
