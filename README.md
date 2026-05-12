# 📦 Linux File Permissions, Ownership & Users Management Cheat Sheet

---

# 📖 Introduction to Linux Permission Model

Linux uses a permission-based security model to control access to:

* Files
* Directories
* Applications
* Scripts
* Services

Every file and directory in Linux has:

* Owner (User)
* Group
* Others

Permissions define who can:

* Read
* Modify
* Execute

View permissions:

```bash id="x9c7fr"
ls -l
```

---

# 📑 1️⃣ Linux Users & Groups

## 🔹 View Existing Users

```bash id="j0xl9q"
cat /etc/passwd
```

---

## 🔹 View Existing Groups

```bash id="m4x1ub"
cat /etc/group
```

---

# 📑 2️⃣ Create Users and Groups

## 🔸 Create a Group

```bash id="g70djr"
sudo groupadd developers
```

---

## 🔸 Create User and Assign Group

```bash id="2sm77t"
sudo useradd -m -s /bin/bash -g developers atul
```

### 🔹 Important Options

| Option | Meaning               |
| ------ | --------------------- |
| -m     | Create home directory |
| -s     | Default shell         |
| -g     | Primary group         |

---

## 🔸 Set Password for User

```bash id="8d7yqr"
sudo passwd atul
```

---

## 🔸 Add Existing User to Group

```bash id="6a11bx"
sudo usermod -aG developers atul
```

---

## 🔸 Check Groups of User

```bash id="fqvnsj"
groups atul
```

---

# 📖 Understanding Permission Types (Read, Write, Execute)

| Permission | Symbol | Meaning            |
| ---------- | ------ | ------------------ |
| Read       | r      | View file contents |
| Write      | w      | Modify file        |
| Execute    | x      | Run file/script    |

---

# 📖 Symbolic (Character) Representation of Permissions

Example:

```bash id="5ld73m"
-rw-r--r--
```

Breakdown:

| Symbol | Meaning            |
| ------ | ------------------ |
| -      | File               |
| rw-    | Owner permissions  |
| r--    | Group permissions  |
| r--    | Others permissions |

---

# 📖 Numeric (Octal) Representation of Permissions

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

---

## 🔹 Common Numeric Permissions

| Numeric | Symbolic  | Usage               |
| ------- | --------- | ------------------- |
| 777     | rwxrwxrwx | Full access         |
| 755     | rwxr-xr-x | Scripts/directories |
| 644     | rw-r--r-- | Standard files      |
| 700     | rwx------ | Private scripts     |
| 600     | rw------- | Sensitive files     |
| 400     | r-------- | SSH private keys    |

---

# 📑 3️⃣ Manage Permissions Like a Pro

## 🔸 View File Permissions

```bash id="czsj5g"
ls -l file.txt
```

---

## 🔸 Output Example

```bash id="j2m46x"
-rw-r--r-- 1 atul developers 1024 Jul 10 file.txt
```

---

# 📑 4️⃣ Modify File Permissions (chmod)

## 🔸 Symbolic Mode

```bash id="9w6krn"
chmod u+x script.sh
```

Add execute permission for owner.

---

```bash id="egmczh"
chmod g-w file.txt
```

Remove write permission for group.

---

```bash id="5y4x5s"
chmod o+r file.txt
```

Add read permission for others.

---

# 📖 Numeric Mode

```bash id="gf3yxt"
chmod 755 file.sh
```

---

## 🔹 Permission Calculation

| Number | Meaning     |
| ------ | ----------- |
| 7      | rwx = 4+2+1 |
| 5      | r-x = 4+0+1 |
| 4      | r-- = 4+0+0 |

---

## 🔸 Recursive Permission Change

```bash id="tl23dn"
chmod -R 755 project/
```

---

# 📑 5️⃣ Change File Ownership

## 🔸 Change Owner

```bash id="8r12mn"
sudo chown atul file.txt
```

---

## 🔸 Change Owner and Group

```bash id="u26h4n"
sudo chown atul:developers file.txt
```

---

## 🔸 Change Group Ownership

```bash id="06vq4s"
sudo chgrp developers file.txt
```

---

## 🔸 Recursive Ownership Change

```bash id="n5vqt8"
sudo chown -R atul:developers project/
```

---

# 📑 6️⃣ Special Permissions: SUID, SGID, Sticky Bit

## 🔸 SUID (Execute as File Owner)

```bash id="9pc6wi"
sudo chmod u+s file.sh
```

Check:

```bash id="wl5o4j"
ls -l file.sh
```

Output:

```bash id="qqm0uv"
-rwsr-xr-x
```

---

## 🔸 SGID (Execute as Group Owner)

```bash id="j8j6nx"
sudo chmod g+s /opt/mydir
```

Check:

```bash id="6vbmz7"
ls -ld /opt/mydir
```

Output:

```bash id="r04yz4"
drwxr-sr-x
```

---

## 🔸 Sticky Bit (Restrict Delete Access)

```bash id="b7yk9x"
sudo chmod +t /tmp/mydir
```

Check:

```bash id="j0c1xm"
ls -ld /tmp/mydir
```

Output:

```bash id="xhl3iq"
drwxrwxrwt
```

---

# 📑 7️⃣ Access Control Lists (ACL) – Advanced Permission Management

ACL provides fine-grained permission management for multiple users.

---

## 🔸 Install ACL Tools

### Ubuntu/Debian

```bash id="uw6nq7"
sudo apt-get install acl -y
```

### RHEL/CentOS/Amazon Linux

```bash id="6v4vl6"
sudo yum install acl -y
```

---

## 🔸 Assign ACL Permission

```bash id="xmygwb"
sudo setfacl -m u:atul:rwx file.txt
```

Meaning:

* User `atul`
* Gets `rwx`
* On `file.txt`

---

## 🔸 View ACL

```bash id="vmgr2w"
getfacl file.txt
```

---

## 🔸 Remove ACL

```bash id="z9wzlf"
setfacl -x u:atul file.txt
```

---

## 🔸 Set Default ACL

```bash id="9fv1sd"
setfacl -d -m u:atul:rw /opt/mydir
```

---

# 📦 Suggested Repository Names

* linux-manage-permissions
* linux-permissions-management
* linux-users-groups-permissions
* linux-security-permissions

---

# 📜 Bonus: View Effective Permissions for User

```bash id="pdxj3v"
sudo -u atul ls -l file.txt
```

---

# 📌 Real-World Security Best Practices for Permissions

## ✅ Follow Least Privilege Principle

Give only required permissions.

---

## ✅ Avoid 777 Permissions

```bash id="9q1o3d"
chmod 777 file.txt
```

Avoid unless absolutely necessary.

---

## ✅ Secure SSH Private Keys

```bash id="d4klcb"
chmod 400 key.pem
```

---

## ✅ Protect Sensitive Files

```bash id="qz1b0m"
chmod 600 secrets.txt
```

---

## ✅ Use Groups Instead of Public Access

Improves security management.

---

## ✅ Regularly Audit Permissions

```bash id="ccj7yf"
find / -perm 777
```

---

# 📌 Important Points to Remember

* Read = 4
* Write = 2
* Execute = 1
* 755 = rwxr-xr-x
* 644 = rw-r--r--
* Root user bypasses most permissions
* Directories require execute permission for access
* Sticky bit is commonly used on `/tmp`
* ACL provides advanced permission control

---

# 📌 Recommended GitHub Repository Structure

```bash id="m9ol6q"
linux-permissions-management/
│
├── README.md
├── examples/
│   ├── chmod-examples.sh
│   ├── chown-examples.sh
│   ├── acl-examples.sh
│   └── users-groups.sh
│
├── notes/
│   └── permissions-cheatsheet.md
│
└── images/
    └── linux-permissions-diagram.png
```

---

# 📌 Conclusion

Linux permissions and ownership management are essential for:

* Linux Administration
* DevOps
* Cloud Security
* Infrastructure Management
* System Hardening

Mastering permissions helps secure Linux environments effectively.

---

# 👨‍💻 Author

**Atul Kamble**

* [LinkedIn - Atul Kamble](https://www.linkedin.com/in/atuljkamble?utm_source=chatgpt.com)
* [GitHub - atulkamble](https://github.com/atulkamble?utm_source=chatgpt.com)
* [X - @Atul_Kamble](https://x.com/Atul_Kamble?utm_source=chatgpt.com)
* [Instagram - atuljkamble](https://www.instagram.com/atuljkamble?utm_source=chatgpt.com)
* [Website - atulkamble.in](https://www.atulkamble.in?utm_source=chatgpt.com)
