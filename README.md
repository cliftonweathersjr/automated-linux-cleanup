# Automated File Creation and Cleanup with Bash and Cron

This project demonstrates a basic but practical example of automation on a Linux system using Bash scripting and `cron`. The goal was to create a file automatically, then delete it shortly after using scheduled tasks.

---

## 🛠 File Creation Script

I began by creating a simple script to generate a test file. Here's the content of `file_creation.sh`:

```bash
#!/bin/bash
echo "Hello World! I was created to be deleted." >> ~/projects/automated-linux-cleanup/documents/test.txt
```

After saving the script using the Vim editor, I made it executable with:

```bash
chmod +x file_creation.sh
```

Initially, I encountered the following error:

```
./file_creation.sh: line 2: /projects/automated-linux-cleanup/documents/test.txt: No such file or directory
```

This was due to using an incorrect absolute path. Updating the path to use the `$HOME` shortcut (`~/`) resolved the issue.

Once corrected, I ran the script again and confirmed that the file was created successfully in the `documents/` folder. After verifying that everything worked as intended, I committed and pushed the script to my GitHub repository.

---

## 🧹 File Cleanup Script

Next, I wrote a cleanup script to delete any files in the same folder. Here's the content of `file_cleanup.sh`:

```bash
#!/bin/bash
find ~/projects/automated-linux-cleanup/documents/ -type f -exec rm {} \;
```

In a real-world scenario, especially in production or enterprise environments, you'd likely use the `-mtime` flag to target files older than a certain age (e.g., delete files older than 7 days).

After testing, I confirmed that the file created by the earlier script was successfully deleted. I then committed and pushed this script to GitHub as well.

---

## ⏰ Automating with Cron

To automate the file creation and deletion, I edited the crontab using:

```bash
crontab -e
```

Since I had no existing crontab entries, I selected Vim as my editor.

Initially, I scheduled the tasks like this:

```cron
# m h  dom mon dow   command
51 9 * * * /~/projects/automated-linux-cleanup/file_creation.sh
53 9 * * * /~/projects/automated-linux-cleanup/file_cleanup.sh
```

However, this didn’t work as expected. I discovered that `~` doesn’t expand in cron, so I updated the paths using my full home directory (`/home/clifton/`):

```cron
51 9 * * * /home/clifton/projects/automated-linux-cleanup/file_creation.sh
53 9 * * * /home/clifton/projects/automated-linux-cleanup/file_cleanup.sh
```

With the corrected paths, the cron jobs ran successfully — first creating the file, then deleting it two minutes later.

---

## 🎯 Purpose

This was a simple exercise to strengthen my familiarity with Bash scripting, file management, and Linux automation using `cron`. While straightforward, it was a productive and insightful 30–45-minute task that helped reinforce important concepts in automation and scripting.


Signed,
*Clifton*
