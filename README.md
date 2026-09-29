# Linux File Permissions Lab

> Hands-on practice managing Linux file and directory permissions using Bash.

## What I Practiced

- Reading Linux permissions with `ls -l`
- Finding hidden files with `ls -la`
- Understanding user, group, and other permissions
- Changing permissions with `chmod`
- Removing unauthorized access
- Managing permissions on files and directories

---

## Lab Scenario

I was given access to the `/home/researcher2/projects` directory and needed to review the existing permissions.

The `researcher2` user belongs to the `research_team` group.

The goal was to identify permissions that allowed unauthorized access and correct them.

---

## 1. Inspect the Project Directory

### Navigate to the Directory

`cd projects`

### View File Permissions

`ls -l`

The files were owned by:

`User: researcher2`  
`Group: research_team`

### Check for Hidden Files

`ls -la`

I found the hidden file:

`.project_x.txt`

### Understanding Linux Permissions

Linux permissions are divided into three categories:

`User` | `Group` | `Other`

The three basic permissions are:

- `r` = read
- `w` = write
- `x` = execute

For example:

`-rwxr-x---`

This means:

- User: read, write, and execute
- Group: read and execute
- Other: no permissions

---

## 2. Remove Unauthorized Write Access

The requirement was that **other users should not have write access** to the files.

After checking the permissions, I found that `project_k.txt` allowed other users to write to the file.

### Fix

`chmod o-w project_k.txt`

This removes the `write` permission from other users.

---

## 3. Restrict `project_m.txt`

The `project_m.txt` file was supposed to be restricted to the file owner.

The group currently had read access.

### Fix

`chmod g-r project_m.txt`

This removes the group's `read` permission.

---

## 4. Secure the Hidden File

The hidden file `.project_x.txt` was an archived file and should not be writable.

The user and group both had write permissions.

### Fix

`chmod u-w,g-w,g+r .project_x.txt`

This:

- Removes write permission from the user
- Removes write permission from the group
- Gives the group read permission

---

## 5. Restrict the `drafts` Directory

The `drafts` directory should only be accessible by `researcher2`.

I checked the directory permissions with:

`ls -l`

The group had execute permission on the directory.

### Fix

`chmod g-x drafts`

This removes the group's execute permission and prevents group members from accessing the directory.

---

## Commands Used

- `cd projects`
- `ls -l`
- `ls -la`
- `chmod o-w project_k.txt`
- `chmod g-r project_m.txt`
- `chmod u-w,g-w,g+r .project_x.txt`
- `chmod g-x drafts`

---

## What I Learned

This lab gave me practical experience working with Linux permissions.

I learned how to:

- Read Linux permission strings such as `-rw-r--r--`
- Identify file owners and groups
- Find hidden files
- Use `chmod` with symbolic permissions
- Remove specific permissions without changing others
- Control access for users, groups, and other users
- Understand the importance of execute permissions on directories

## Key Takeaway

I learned that properly configuring Linux permissions is an important part of maintaining system security and access control. By assigning users and groups only the permissions they require, administrators can follow the principle of least privilege, reduce unauthorized access, and help protect sensitive files and directories. 
