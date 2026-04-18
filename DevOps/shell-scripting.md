### What is automation:

Automation is the process where you try to reduce your manual activities.
manual → automate

Shell scripting is the process where you automate your tasks on Linux.

---

### Create file:

touch first-shell-script.sh

---

### Basic Commands:

ls → list files

ls -ltr → shows when files were created and permissions

ls -ld → shows details of current directory

man ls → gives you details of the command (man = manual, you can use it with any command)

---

### vi / vim:

vi and vim can be used to create or open files in terminal.
vi is already installed in Linux, but vim should be installed using:

sudo apt install vim

Commands:
:wq → save and exit
:q! → quit without saving

vim second.sh → vim directly creates the file (if not exist) and opens it

---

### NOTE:

Sometimes vim asks whether to open an existing file or create a new one.
vim does not always create a new file — it can open an existing file.

vim is basically used to write/edit files.
touch creates a file.

---

### Shebang:

#!/ → shebang

#!/bin/bash

👉 This first line tells the Linux kernel which interpreter to use to execute the script.

bash, dash, sh, ksh → these are different **shell interpreters** used with shebang

👉 You have to tell the Linux kernel which interpreter to use to execute your script

👉 In terms of syntax, they can vary significantly

👉 bash is a shell interpreter and has its own syntax for writing scripts

---

### Linking Concept (Important):

When you use:
#!/bin/sh

👉 `/bin/sh` is a **symbolic link**, not always bash

👉 It can point to different shells

Earlier:
/bin/sh → bash

Now (in many systems like Ubuntu):
/bin/sh → dash

👉 So the request is forwarded to whichever shell `/bin/sh` points to

---

### Important:

👉 If you are using bash scripting, use it explicitly:

#!/bin/bash

👉 Because compatibility issues can occur on different machines

👉 `/bin/sh` is not always linked to bash — it can be linked to dash

👉 Do NOT assume `/bin/sh` = bash

---

### Interview Question:

What is the difference between #!/bin/sh and #!/bin/bash?

Previously both behaved similarly because `/bin/sh` was linked to bash.
Now many systems use dash by default.

👉 If you use bash syntax with `#!/bin/sh`, the script might not run.

---

### Key Understanding:

👉 If I use `#!/bin/sh` and write bash syntax:

* It will run on my system ONLY if `/bin/sh` points to bash
* It will fail on another system where `/bin/sh` points to dash

---

### Printing Output:

echo "hello world"

---

### vim usage:

open file → press Esc + i (insert mode)
closing file → Esc + :wq (save and exit)

:q! → quit without saving

---

### File Content:

cat → prints content of the file

---

### Executing the file:

./filename
sh filename

👉 `./filename` requires execute permission
👉 `sh filename` does NOT require execute permission

---

## Permissions in Linux:

Before executing a script file, Linux checks permissions.

👉 chmod is used to **change permissions**

---

### chmod:

ch → stands for change (changing permissions)

👉 syntax:
chmod <mode> filename

👉 `chmod filename` alone is invalid

---

### Permission Types:

chmod controls permissions for:

1. User (owner)
2. Group
3. Others (all users)

---

### Numeric Values:

4 → read
2 → write
1 → execute

Example:

chmod 777 filename

👉 gives full permissions to user, group, and others

---

## How vim saves a file:

When you save in vim, it often:

* creates a temporary file
* writes changes there
* deletes old file
* renames new file

👉 So it may replace the file instead of editing directly

---

### Important Clarification:

👉 Vim does NOT override permissions

👉 It can overwrite a file only if the **directory has write permission**

---

## Running Scripts:

👉 Running with sh or bash does NOT need execute permission

👉 Running with ./script.sh requires execute permission

---

## Difference: File vs Directory Permissions

### File Permissions:

r (read) → view content
w (write) → modify content
x (execute) → run the file

Example:

chmod 444 file.txt

👉 read only
👉 no editing
👉 no execution

---

### Directory Permissions:

r (read) → list files
w (write) → create/delete/rename files
x (execute) → enter directory

---

### Key Difference:

👉 File w = modify content
👉 Directory w = modify files inside

---

## Why this matters:

You saw:
“Even with 444, file was modified”

👉 Reality:

File permission blocked editing ✔️
Directory permission allowed replacement ✔️

👉 Directory controls file existence, not file content

---

## Changing Permissions:

Numeric:
chmod 755 file.sh

👉 user = 7 (rwx)
👉 group = 5 (r-x)
👉 others = 5 (r-x)

Symbolic:
chmod u+x file.sh
chmod g-w file.txt
chmod o+r file.txt

Directory:
chmod 755 myfolder
chmod 555 .

---

### What does . mean?

. → current directory

Examples:
chmod 555 .
ls .

Related:
. → current directory
.. → parent directory

---

## Final Understanding:

To modify a file, Linux checks:

✅ File permission (write?)
✅ Directory permission (replace/delete?)
✅ Ownership / root

---

## Summary:

👉 File permissions = content control
👉 Directory permissions = structure control

👉 Both together = real security

🔥 One-line takeaway:
A file is protected only when BOTH the file and its directory are properly restricted.

---

## Role of Shell Scripting in DevOps:

As a DevOps engineer:

* you maintain infrastructure
* maintain code using git on Linux
* do configuration management using Ansible

👉 all of these can be done using shell scripting

---

### Example:

John is a DevOps engineer in Amazon.
He manages thousands of Linux VMs.

Instead of manually checking CPU, memory, and processes:

👉 he writes a script that:

* fetches system data
* checks node health
* logs into machines
* returns output

👉 runs automatically daily
👉 sends email reports

---

### Why shell scripting?

👉 Tools provide limited parameters

👉 Shell scripts allow you to get as many parameters as you want

---

## Monitoring Node Health:

CPU → nproc
Memory → free
Processes → top
available disk space -> df
---

## Final Concept:

👉 If I use #!/bin/sh and write bash syntax:

* it will run on my system ONLY if /bin/sh points to bash
* it will fail on another system where /bin/sh points to dash

---

