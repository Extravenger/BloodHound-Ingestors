# BloodHound-Ingestors

> [!NOTE]
> None of the tools mentioned here were developed by me. This repository was created solely to organize and store them in one place!<br>

1. [SharpHound](#SharpHound)
2. [RustHound](#RustHound)
3. [ShadowHound](#ShadowHound)
4. [SOAPHound](#SOAPHound)
5. [ADExplorer](#ADExplorer)
5. [GPOHound](#GPOHound)
6. [bloodhound-ce](https://github.com/dirkjanm/BloodHound.py/tree/bloodhound-ce) (Remote)
7. [NetExec](#NetExec) (Remote)

# SharpHound

![image](https://github.com/user-attachments/assets/4d462c57-fbf3-46ff-a55d-5f36884841af)

Source: https://github.com/SpecterOps/SharpHound.git

SharpHound is a data collection tool that's part of the BloodHound project, It maps Active Directory (AD) environments by gathering information like user sessions, group memberships, and ACLs.<br>
It uses methods like LDAP queries, SMB sessions, and Windows APIs for collection and it helps identify attack paths, privilege escalation opportunities, and misconfigurations in AD.

- `.\SharpHound.exe -c all --domain sevenkingdoms.local --zipfilename sevenkingdoms --zippassword --outputfile C:\Users\Public\Documents\out.zip`

# RustHound

![image](https://github.com/user-attachments/assets/74c10694-0da2-4727-8df0-2cfa37992075)

Source: https://github.com/g0h4n/RustHound-CE

RustHound-CE is a cross-platform and cross-compiled BloodHound collector tool written in Rust, making it compatible with Linux, Windows, and macOS. It therefore generates all the JSON files that can be analyzed by BloodHound Community Edition.

- `.\rusthound-ce.exe --ldapusername amit --ldappassword "Password123!" --domain sevenkingdoms.local --collectionmethod All --zip`

# ShadowHound

![image](https://github.com/user-attachments/assets/f9d133af-e588-4296-9841-42ada68871c0)

Source: https://github.com/Friends-Security/ShadowHound

ShadowHound is a set of PowerShell scripts for Active Directory enumeration without the need for introducing known-malicious binaries like SharpHound. It leverages native PowerShell capabilities to minimize detection risks and offers two methods for data collection:

1. ShadowHound-ADM.ps1: Uses the Active Directory module (ADWS).
2. ShadowHound-DS.ps1: Utilizes direct LDAP queries via DirectorySearcher.

- Collect: `ShadowHound-ADM -OutputFilePath "C:\Results\ldap_output.txt"`
- Converting Data for BloodHound: `python3 split_output.py -i ldap_output.txt -o pyldapsearch_ldap -n 100`

After collecting data, use BofHound to convert it into BloodHound-compatible JSON files:

- `python3 bofhound.py -i ldap_output.txt -p All --parser ldapsearch`

# SOAPHound

![image](https://github.com/user-attachments/assets/977eeccb-5f3d-425f-a696-c2ad5a57e959)

[SOAPHound](https://github.com/FalconForceTeam/SOAPHound) is a .NET data collector tool, which collects Active Directory data via the Active Directory Web Services (ADWS) protocol.

- `SOAPHound.exe --buildcache -c c:\temp\cache.txt`

This will generate a cache file in the c:\temp folder. The cache file is a JSON formatted mapping of basic information about all domain objects.<br>
After the cache file has been generated, you can use the --bhdump collection method to collect data from the domain that can be imported into BloodHound.

An example command to collect BloodHound data is (note that this references the cache file generated in the previous step):

- `SOAPHound.exe -c c:\temp\cache.txt --bhdump -o c:\temp\bloodhound-output`


# ADExplorer

![image](https://github.com/user-attachments/assets/355c84b0-d3e8-4191-942f-27ce8576a53f)

Source: https://github.com/c3c/ADExplorerSnapshot.py.git

[Download](https://learn.microsoft.com/en-us/sysinternals/downloads/adexplorer) and Execute the binary in the environment you want to collect information from and capture a snapshot.<br>
We can then convert the snapshot into JSON files that BloodHound can ingest!

- `python3 ADExplorerSnapshot.py <FILENAME>.dat`

# GPOHound

Source: https://github.com/cogiceo/GPOHound

GPOHound is a tool for dumping and analysing Group Policy Objects (GPOs) extracted from the SYSVOL share.<br>
It provides a structured, formalized format to help uncover misconfigurations, insecure settings, and privilege escalation paths in Active Directory environments.

# NetExec

![image](https://github.com/user-attachments/assets/73ae2e49-3be5-4d30-9e36-0e7b60474967)

Source: https://github.com/Pennyw0rth/NetExec

NetExec has a build in bloodhound collector. To configure the name server, dns timeout or to use tcp for dns resolution take a look at the NetExec command line options for [dns](https://github.com/Pennyw0rth/NetExec-Wiki/blob/main/getting-started/dns-options.md).

- `nxc ldap <ip> -u user -p pass --bloodhound --collection All`
