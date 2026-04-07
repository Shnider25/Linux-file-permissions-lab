# 🔐 Linux File Permissions Management

> **Google Cybersecurity Certificate – Portfolio Activity**  
> Course: Tools of the Trade: Linux and SQL

---

## 📋 Project Description

The research team at my organization needed to update file permissions for certain files and directories within the `projects` directory. The existing permissions did not reflect the appropriate level of authorization, creating potential security risks. I audited and updated these permissions using Linux commands to bring the system into compliance and maintain a secure environment.

---

## 🛠️ Skills Demonstrated

- Linux command-line navigation
- Auditing file and directory permissions with `ls -la`
- Modifying permissions using `chmod`
- Understanding of the Linux permissions string (rwx model)
- Applying the principle of least privilege

---

## 📁 Tasks Performed

### 1. Check File and Directory Details

I used the `ls` command with the `-la` flag to display a detailed listing of all contents in the `projects` directory, including hidden files.

```bash
ls -la projects/
```

**Output revealed:**
- 1 directory: `drafts`
- 1 hidden file: `.project_x.txt`
- 5 project files (e.g., `project_k.txt`, `project_t.txt`, etc.)

Each entry includes a **10-character permissions string** in the first column.

---

### 2. Understanding the Permissions String

The 10-character string breaks down as follows:

| Character(s) | Meaning |
|---|---|
| 1st | File type: `d` = directory, `-` = regular file |
| 2nd – 4th | **User** permissions: read (`r`), write (`w`), execute (`x`) |
| 5th – 7th | **Group** permissions: read (`r`), write (`w`), execute (`x`) |
| 8th – 10th | **Other** permissions: read (`r`), write (`w`), execute (`x`) |

A `-` in any position means that permission is **not granted**.

**Example:** `-rw-rw-r--` for `project_t.txt`
- `-` → regular file
- `rw-` → user has read & write
- `rw-` → group has read & write
- `r--` → others have read only

---

### 3. Change File Permissions

The organization determined that **others should not have write access** to any files. I identified `project_k.txt` as having improper write access for others and removed it.

```bash
chmod o-w project_k.txt
ls -la projects/
```

This brought `project_k.txt` into compliance with the organization's authorization policy.

---

### 4. Change Permissions on a Hidden File

The team archived `project_x.txt` and required that:
- **No one** has write access
- **User and group** retain read access

Hidden files in Linux start with a `.` — in this case `.project_x.txt`.

```bash
chmod u-w,g-w,g+r .project_x.txt
ls -la projects/
```

This removed write access from both user and group, and ensured the group had read access.

---

### 5. Change Directory Permissions

Only `researcher2` should have access to the `drafts` directory. This meant removing execute permissions from the group, since `researcher2` already had the necessary permissions.

```bash
chmod g-x drafts/
ls -la projects/
```

After this change, only `researcher2` retained execute permissions on the `drafts` directory.

---

## ✅ Summary

| Task | Command Used | Purpose |
|---|---|---|
| Audit permissions | `ls -la` | View all file/directory permissions |
| Remove others' write access | `chmod o-w project_k.txt` | Principle of least privilege |
| Update hidden file permissions | `chmod u-w,g-w,g+r .project_x.txt` | Restrict archived file access |
| Restrict directory access | `chmod g-x drafts/` | Limit access to authorized user only |

By using `ls -la` to audit and `chmod` to adjust permissions, I successfully aligned the `projects` directory with my organization's security requirements — demonstrating practical application of Linux file permission management in a cybersecurity context.

---

## 📚 Certificate

[Google Cybersecurity Certificate](https://grow.google/certificates/cybersecurity/) – Coursera  

---

*This project is part of my cybersecurity portfolio developed through the Google Cybersecurity Certificate program.*
