# BloodHound-Ingestors

This repository consolidates information on various BloodHound Ingestors. While conducting red team operations, I faced challenges and decided to create a single repository to centralize all of them.

1. [SharpHound](https://github.com/SpecterOps/SharpHound.git)<br>
2. [RustHound](https://github.com/g0h4n/RustHound-CE)<br>
3. [ShadowHound](https://github.com/Friends-Security/ShadowHound)<br>
4. [bloodhound-ce](https://github.com/dirkjanm/BloodHound.py/tree/bloodhound-ce) (Remote)
5. [ADExplorer](https://github.com/c3c/ADExplorerSnapshot.py.git)<br>

# SharpHound

![image](https://github.com/user-attachments/assets/4d462c57-fbf3-46ff-a55d-5f36884841af)

SharpHound is a data collection tool that's part of the BloodHound project, It maps Active Directory (AD) environments by gathering information like user sessions, group memberships, and ACLs.<br>
It uses methods like LDAP queries, SMB sessions, and Windows APIs for collection and it helps identify attack paths, privilege escalation opportunities, and misconfigurations in AD.

- `.\SharpHound.exe -c all --domain sevenkingdoms.local --zipfilename sevenkingdoms --zippassword --outputfile C:\Users\Public\Documents\out.zip`

# RustHound

![image](https://github.com/user-attachments/assets/74c10694-0da2-4727-8df0-2cfa37992075)

RustHound-CE is a cross-platform and cross-compiled BloodHound collector tool written in Rust, making it compatible with Linux, Windows, and macOS. It therefore generates all the JSON files that can be analyzed by BloodHound Community Edition.

- `.\rusthound-ce.exe --ldapusername amit --ldappassword "Password123!" --domain sevenkingdoms.local --collectionmethod All --zip output.zip`

# ShadowHound

![image](https://github.com/user-attachments/assets/f9d133af-e588-4296-9841-42ada68871c0)

ShadowHound is a set of PowerShell scripts for Active Directory enumeration without the need for introducing known-malicious binaries like SharpHound. It leverages native PowerShell capabilities to minimize detection risks and offers two methods for data collection:

1. ShadowHound-ADM.ps1: Uses the Active Directory module (ADWS).
2. ShadowHound-DS.ps1: Utilizes direct LDAP queries via DirectorySearcher.

- Collect: `ShadowHound-ADM -OutputFilePath "C:\Results\ldap_output.txt"`
- Converting Data for BloodHound: `python3 split_output.py -i ldap_output.txt -o pyldapsearch_ldap -n 100`

After collecting data, use BofHound to convert it into BloodHound-compatible JSON files:

- `python3 bofhound.py -i ldap_output.txt -p All --parser ldapsearch`
