# 📂 linux-manage-permissions

## 📖 Introduction

Linux permissions are a fundamental part of system security and administration.
They control who can read, write, and execute files or directories in the system.

Proper permission management helps:

* Protect sensitive files
* Prevent unauthorized access
* Secure applications and services
* Maintain system stability

This project explains Linux permission concepts with practical commands and examples.

---

# 📌 Topics Covered

* Introduction to Linux Permission Model
* Understanding Permission Types (Read, Write, Execute)
* Symbolic (Character) Representation of Permissions
* Numeric (Octal) Representation of Permissions
* Modifying Permissions (`chmod`)
* File Ownership and Group Ownership Concepts
* Changing Ownership (`chown`, `chgrp`)
* Access Control Lists (ACL)
* Real-World Security Best Practices

---

# 🖥️ Prerequisites

* Linux System (Ubuntu, RHEL, CentOS, Amazon Linux, Debian)
* Basic Linux command knowledge
* Terminal access
* Sudo privileges (recommended)

---

# 📌 1️⃣ Introduction to Linux Permission Model

Linux permissions define access control for:

* Files
* Directories
* Scripts
* Applications

Each file/directory has:

* Owner (User)
* Group
* Others

View permissions using:

```bash
ls -l
```

Example:

```bash
-rw-r--r-- 1 ec2-user ec2-user 120 May 10 demo.txt
```

---

# 📌 2️⃣ Understanding Permission Types

## 🔹 Read (r)

Allows viewing file contents.

```bash
cat file.txt
```

---

## 🔹 Write (w)

Allows modifying file contents.

```bash
echo "Hello" >> file.txt
```

---

## 🔹 Execute (x)

Allows executing scripts/programs.

```bash
./script.sh
```

---

# 📌 3️⃣ Symbolic Representation of Permissions

Example:

```bash
-rwxr-xr--
```

Breakdown:

| Symbol | Meaning            |
| ------ | ------------------ |
| rwx    | Owner permissions  |
| r-x    | Group permissions  |
| r--    | Others permissions |

---

## 🔹 Permission Symbols

| Symbol | Meaning       |
| ------ | ------------- |
| r      | Read          |
| w      | Write         |
| x      | Execute       |
| -      | No Permission |

---

# 📌 4️⃣ Numeric (Octal) Representation

## 🔹 Permission Values

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

---

## 🔹 Common Permission Examples

| Numeric | Symbolic  | Meaning                        |
| ------- | --------- | ------------------------------ |
| 777     | rwxrwxrwx | Full access to everyone        |
| 755     | rwxr-xr-x | Common for scripts/directories |
| 644     | rw-r--r-- | Common for files               |
| 600     | rw------- | Private file                   |
| 700     | rwx------ | Private executable             |

---

# 📌 5️⃣ Modifying Permissions Using chmod

## 🔹 Symbolic Method

Add execute permission:

```bash
chmod +x script.sh
```

Remove write permission:

```bash
chmod -w file.txt
```

Grant read permission to group:

```bash
chmod g+r file.txt
```

---

## 🔹 Numeric Method

```bash
chmod 755 script.sh
```

```bash
chmod 644 file.txt
```

---

# 📌 6️⃣ File Ownership and Group Ownership

Check ownership:

```bash
ls -l
```

Example:

```bash
-rw-r--r-- 1 atul devops 200 May 10 notes.txt
```

| Field  | Meaning |
| ------ | ------- |
| atul   | Owner   |
| devops | Group   |

---

# 📌 7️⃣ Changing Ownership

## 🔹 Change File Owner

```bash
sudo chown user1 file.txt
```

---

## 🔹 Change Owner and Group

```bash
sudo chown user1:devops file.txt
```

---

## 🔹 Change Group Ownership

```bash
sudo chgrp developers file.txt
```

---

# 📌 8️⃣ Directory Permissions

## 🔹 Create Directory

```bash
mkdir project
```

---

## 🔹 Assign Permissions

```bash
chmod 755 project
```

---

## 🔹 Recursive Permission Change

```bash
chmod -R 755 project
```

---

# 📌 9️⃣ Access Control Lists (ACL)

ACL provides advanced permission management beyond standard Linux permissions.

---

## 🔹 Install ACL Package

### Ubuntu/Debian

```bash
sudo apt install acl -y
```

### RHEL/CentOS/Amazon Linux

```bash
sudo yum install acl -y
```

---

## 🔹 Set ACL Permission

```bash
setfacl -m u:user1:rwx file.txt
```

---

## 🔹 View ACL

```bash
getfacl file.txt
```

---

## 🔹 Remove ACL

```bash
setfacl -x u:user1 file.txt
```

---

# 📌 🔟 Special Permissions

## 🔹 SUID

Runs file with owner's privileges.

```bash
chmod u+s file.sh
```

---

## 🔹 SGID

```bash
chmod g+s directory/
```

---

## 🔹 Sticky Bit

Commonly used on `/tmp`.

```bash
chmod +t shared/
```

---

# 📌 1️⃣1️⃣ Real-World Security Best Practices

## ✅ Follow Principle of Least Privilege

Grant only required permissions.

---

## ✅ Avoid 777 Permissions

```bash
chmod 777 file.txt
```

Avoid unless absolutely necessary.

---

## ✅ Secure SSH Keys

```bash
chmod 400 key.pem
```

---

## ✅ Protect Sensitive Files

```bash
chmod 600 secrets.txt
```

---

## ✅ Use Groups for Shared Access

Instead of giving permissions to everyone.

---

## ✅ Regularly Audit Permissions

```bash
find / -perm 777
```

---

# 📌 Useful Commands Cheat Sheet

| Command | Description         |
| ------- | ------------------- |
| ls -l   | View permissions    |
| chmod   | Change permissions  |
| chown   | Change owner        |
| chgrp   | Change group        |
| getfacl | View ACL            |
| setfacl | Set ACL             |
| umask   | Default permissions |

---

# 📌 Practice Examples

## 🔹 Create File

```bash
touch demo.txt
```

---

## 🔹 Assign Permissions

```bash
chmod 644 demo.txt
```

---

## 🔹 Create Script

```bash
nano script.sh
```

```bash
#!/bin/bash
echo "Hello Linux"
```

---

## 🔹 Make Script Executable

```bash
chmod +x script.sh
```

Run:

```bash
./script.sh
```

---

# 📌 Common Permission Scenarios

| Scenario         | Recommended Permission |
| ---------------- | ---------------------- |
| Web Files        | 644                    |
| Directories      | 755                    |
| SSH Private Keys | 400                    |
| Backup Files     | 600                    |
| Scripts          | 755                    |

---

# 📌 Conclusion

Linux permission management is essential for:

* System security
* User access control
* Application stability
* Compliance and auditing

Mastering permissions helps Linux administrators and DevOps engineers build secure and reliable environments.

---

# 📌 Author

**Atul Kamble**
Cloud & DevOps Trainer | Cloud Solutions Architect

GitHub: [atulkamble GitHub](https://github.com/atulkamble?utm_source=chatgpt.com)
