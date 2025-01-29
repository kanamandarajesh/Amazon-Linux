
---

### 1. **What happens when you type www.google.com on your browser?**
When you type "www.google.com" into your browser:
1. **DNS Lookup**: The browser queries a DNS (Domain Name System) server to resolve "www.google.com" into an IP address (e.g., `142.250.190.78`).
2. **Establishing Connection**: The browser establishes a TCP connection with the IP address over port 80 (HTTP) or 443 (HTTPS), depending on whether it's using HTTP or HTTPS.
3. **Request**: The browser sends an HTTP request (GET request) to the server.
4. **Server Response**: The server processes the request and sends back the HTML page, along with additional resources like CSS, JavaScript, and images.
5. **Rendering**: The browser renders the webpage for you to view.

---

### 2. **Explain DNS. How can we check system utilization on a Linux system?**
- **DNS (Domain Name System)**: DNS is a hierarchical system that translates human-readable domain names (like www.google.com) into IP addresses, which computers use to locate each other on the network.
  
- **To check system utilization on a Linux system**: 
  - **`top`**: Displays a real-time summary of system performance, including CPU, memory, and process information.
  - **`htop`**: An enhanced version of `top` with an easier-to-read, interactive interface.
  - **`free -h`**: Displays memory usage (RAM and swap).
  - **`df -h`**: Displays disk space usage.
  - **`iostat`**: Reports CPU statistics and input/output device load.

---

### 3. **Tell me when you solved a complex issue using a simple solution?**
This could be a personal anecdote from your experience. Here's an example:

**Example Answer**:  
I once worked on a project where I needed to troubleshoot a system performance issue. After much analysis, I realized that the issue wasn't with the application code but with the configuration of a log rotation system that was using excessive disk space. The simple solution was adjusting the log retention policy rather than diving deep into complex code optimizations. This solved the problem, and performance improved significantly with minimal effort.

---

### 4. **Tell me about a time when you had to dive deep to solve a problem?**
This should be another personal anecdote. Here's an example:

**Example Answer**:  
I was working on a system where users were experiencing intermittent delays. After checking the usual suspects (CPU usage, memory, network), I had to dive deeper into the system logs and tracing tools. I discovered that a certain database query was being inefficiently executed during peak times, leading to a backlog of requests. I optimized the query and added better indexing, which solved the performance issue.

---

### 5. **I am unable to establish a connection through SSH to a remote EC2 instance and getting permission denied error. How to troubleshoot?**
1. **Check Security Group**: Ensure that the EC2 instance’s security group allows inbound SSH traffic on port 22 from your IP address.
2. **Check Key Pair**: Verify that you're using the correct private key (the one you associated with the EC2 instance) to authenticate.
3. **Check User**: Ensure you're using the correct SSH user (`ec2-user` for Amazon Linux, `ubuntu` for Ubuntu, etc.).
4. **Verify Instance State**: Confirm that the EC2 instance is in the running state.
5. **Verify SSH Agent**: Ensure your SSH agent is running and the private key is loaded (`ssh-add`).

---

### 6. **Not able to modify file permissions using the `chmod` command. What could be the issue?**
1. **Permissions Issue**: You may not have the necessary privileges to change the file permissions. Ensure you're using `sudo` if required.
2. **Filesystem is Read-Only**: Check if the filesystem is mounted as read-only. Use `mount` to check.
3. **Immutable Attribute**: The file might have the immutable attribute set. Use `lsattr` and `chattr` to check/change it.
4. **Filesystem Error**: The file system might be corrupted or in a non-writable state.

---

### 7. **What process happens in the background when an application loads up?**
When an application starts, the operating system performs several steps in the background:
1. **Memory Allocation**: The OS allocates memory for the application.
2. **Process Creation**: The kernel creates a new process for the application and assigns it a process ID (PID).
3. **Page Loading**: The necessary pages of the application are loaded into RAM, either in full or partially (using demand paging).
4. **I/O Setup**: File handles, input/output devices, and network connections are established if needed.
5. **Execution**: The application begins executing instructions from its code.

---

### 8. **How to check disk usage?**
You can check disk usage on Linux using the following commands:
- **`df -h`**: Shows the disk space usage in a human-readable format.
- **`du -sh <directory>`**: Shows the disk usage of a specific directory.
- **`lsblk`**: Displays information about block devices and their usage.

---

### 9. **Where is the table restored? Is it stored in RAM memory?**
In a database system, a **table** is typically stored in the **disk** but may be cached in **RAM** for faster access if the database uses memory caching (e.g., buffer pools). The system may restore tables into memory (RAM) for temporary access to improve performance but persists the data in non-volatile storage (disk).

---

### 10. **When a program is started, all pages are not loaded into RAM, and only the necessary pages are loaded as per the program's requirement.**
This is **demand paging**, where only the pages of a program that are needed at the moment are loaded into memory. As the program executes and needs more pages, the operating system loads them from disk into RAM. This method allows efficient memory usage.

---

### 11. **Where do the processes go from RAM? Usually, they go to the CPU where the execution happens?**
Yes, processes are loaded into **RAM** by the operating system, and the **CPU** retrieves instructions from the RAM to execute them. The CPU uses its registers and cache to store and quickly access frequently used data.

---

### 12. **How does the OS achieve running multiple applications and multiprocessing?**
- **Multiprocessing**: The OS achieves multiprocessing by using multiple **CPUs or cores** to run multiple processes in parallel. Each CPU/core executes different processes or threads simultaneously.
- **Multitasking**: On a single core, the OS uses time-sharing to rapidly switch between tasks, giving the illusion of simultaneous execution.

---

### 13. **How does context switching work, and what is a Process Control Block (PCB)?**
- **Context Switching**: This is the process of saving the state of a currently running process (its registers, program counter, etc.) and loading the state of another process. It allows the CPU to switch between processes efficiently.
- **Process Control Block (PCB)**: The PCB is a data structure that stores information about a process, such as its state, program counter, registers, memory management information, and scheduling information.

---

### 14. **What interrupt signal is sent by the CPU when it needs to switch from one process to another?**
When the CPU needs to switch between processes, an **interrupt signal** called a **Timer Interrupt** is used. This interrupts the current process, saving its state, and then the OS scheduler decides which process to execute next.

---

### 15. **My system is running very slow. How will I troubleshoot?**
1. **Check CPU Usage**: Use `top` or `htop` to check if the CPU is overburdened.
2. **Check Memory Usage**: Ensure the system isn’t running out of memory (`free -h`).
3. **Check Disk Usage**: Check if the disk is full or under heavy usage (`df -h` and `iostat`).
4. **Look at Running Processes**: Identify any processes consuming excessive resources and kill them if necessary (`ps aux`).
5. **Check Network Usage**: High network usage could cause slowness (use `iftop` or `netstat`).
6. **Check Logs**: Review system logs for errors or warnings (`/var/log/syslog` or `dmesg`).

---

### 16. **Your hard disk is 600GB, and you want to upload a file which is 65GB but you're getting an error saying the disk is full, even though you have 200GB free. What could be the issue?**
- **Filesystem Limits**: Some filesystems have limitations on file sizes (e.g., FAT32 has a 4GB file size limit). Check if you're using a filesystem that supports large files (like ext4 or NTFS).
- **Inode Limits**: The filesystem may have run out of **inodes**, preventing new files from being created, even if there is free space. Use `df -i` to check inode usage.

---

### 17. **What is the difference between file storage and block storage?**
- **File Storage**: Data is stored in files, and the file system manages the storage. Example: NFS, SMB.
- **Block Storage**: Data is stored in fixed-size blocks, and it's up to the user to manage files. Example: AWS EBS, SAN.

---

### 18. **Why do you want to join Amazon?**
This is a personal question. Here’s an example answer:
**Example Answer**:  
I am interested in joining Amazon because it is known for its innovation, leadership, and cutting-edge technologies. I admire Amazon’s customer-centric approach and its ability to solve complex problems at scale. I believe my skills and passion for technology would make me a valuable contributor to Amazon’s mission of continuous improvement and delivering exceptional service to customers.

---
