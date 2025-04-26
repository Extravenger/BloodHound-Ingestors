# BloodHound-Ingestors

This repository consolidates information on various BloodHound Ingestors. While conducting red team operations, I faced challenges and decided to create a single repository to centralize all of them.

1. [SharpHound](https://github.com/SpecterOps/SharpHound.git)<br>
2. [ADExplorer](https://github.com/c3c/ADExplorerSnapshot.py.git)<br>
3. [RustHound](https://github.com/g0h4n/RustHound-CE)<br>
4. [ShadowHound](https://github.com/Friends-Security/ShadowHound)<br>
5. [bloodhound-ce](https://github.com/dirkjanm/BloodHound.py/tree/bloodhound-ce)

# SharpHound

![image](https://github.com/user-attachments/assets/4d462c57-fbf3-46ff-a55d-5f36884841af)

- `.\SharpHound.exe -c all --domain sevenkingdoms.local --zipfilename sevenkingdoms --zippassword --outputfile C:\Users\Public\Documents\out.zip`

# RustHound

![image](https://github.com/user-attachments/assets/74c10694-0da2-4727-8df0-2cfa37992075)

RustHound-CE is a cross-platform and cross-compiled BloodHound collector tool written in Rust, making it compatible with Linux, Windows, and macOS. It therefore generates all the JSON files that can be analyzed by BloodHound Community Edition.

- `.\rusthound-ce.exe --ldapusername amit --ldappassword "Password123!" --domain sevenkingdoms.local --collectionmethod All --zip output.zip`
