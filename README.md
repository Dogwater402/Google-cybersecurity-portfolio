# Linux File Permissions Audit and Remediation

## Project Description

As a security professional working with a research team at a large organization, my role involves ensuring precise user authorizations on the file system. This project demonstrates my ability to examine existing Linux file and directory permissions, identify discrepancies with authorized access levels, and precisely modify these permissions to bolster system security and maintain data integrity.

## Scenario Overview

My primary responsibility is to safeguard sensitive research data by implementing the principle of least privilege. This involves regularly auditing file system permissions and making necessary adjustments. For this activity, I investigated and updated permissions on a set of files and a subdirectory within the research team's `projects` directory, ensuring only authorized users have access and removing any unauthorized write capabilities.

---

## Step-by-Step Instructions & Execution

### 1. Check File and Directory Details: Examining Current Permissions

To begin the audit, I needed to inspect the current permissions set on all files and subdirectories within the `projects` directory, including hidden files.

**Command Used:**
The `ls -la` command is used to list the contents of a directory in a long format (`-l`) and include hidden files and directories (`-a`). This provides a detailed output showing permissions, ownership, file size, and modification date.

```bash
ls -la /home/researcher/projects/Current Permissions (from the example ls -la output above, or from the provided Current file permissions document):

project_k.txt: rw-rw-rwx

project_m.txt: rw-r-----

project_r.txt: rw-rw-r--

project_t.txt: rw-rw-r--

.project_x.txt: rwxrwxrwx

drafts/: rwxrwxrwx2. Describe the Permissions String
The 10-character string at the beginning of each line in the ls -l (or ls -la) output represents the file or directory permissions. It's a crucial component for understanding access control in Linux.

Example Explanation (using drwxr-xr-x for a typical directory):

The first character (d) indicates the file type.

d: directory

-: regular file

l: symbolic link

c: character device file

b: block device file

The next nine characters are divided into three sets of three, representing permissions for:

User (Owner): The first set of three characters (rwx).

Group: The second set of three characters (r-x).

Others: The third set of three characters (r-x).

Within each set of three:

r: Read permission. Allows viewing file contents or listing directory contents.

w: Write permission. Allows modifying file contents or creating/deleting files within a directory.

x: Execute permission. Allows running a file (if it's an executable script/program) or entering/traversing a directory.

-: Indicates the absence of that particular permission.

For our specific audit example: Let's take .project_x.txt with initial permissions rwxrwxrwx.

-: It's a regular file.

rwx: The User (owner) has read, write, and execute permissions.

rwx: The Group has read, write, and execute permissions.

rwx: Others (anyone else on the system) have read, write, and execute permissions.

This is a highly insecure permission set, providing full access to anyone.

3. Change File Permissions: Removing Unauthorized Write Access for Others
Requirement: The organization's policy dictates that others should not have write access to any files. Based on the initial ls -la output, project_k.txt currently has rwx (read, write, execute) for "others," which violates this policy.

Command Used to Modify Permissions:
The chmod command is used to change file permissions. We can use either symbolic mode or octal mode. Here, I'll use octal mode for precision.

The current permission for project_k.txt is rw-rw-rwx (octal 667). To remove write access for "others" while retaining read access, the "others" permission needs to change from 7 (rwx) to 4 (r--). This means the target permission will be rw-rw-r-- (octal 664).
