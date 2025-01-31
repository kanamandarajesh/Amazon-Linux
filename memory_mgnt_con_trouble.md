### **Memory Management in Linux**

Memory management is a crucial aspect of any Linux system, and it ensures that processes and applications can efficiently utilize available memory resources while preventing memory overload or leaks.

#### **Key Concepts of Memory Management**:
1. **Virtual Memory**:
   - The kernel provides **virtual memory** to each process, which appears as if each process has its own dedicated memory. In reality, the system shares physical memory among all processes, using **paging** to swap data between RAM and swap space (on disk) when necessary.

2. **RAM vs Swap**:
   - **RAM** (Physical memory) is where running processes and data are stored.
   - **Swap** is disk space used when RAM is full. Excess data from RAM is moved to swap space to free up memory for other processes. This is slower than RAM but provides an overflow mechanism to prevent out-of-memory (OOM) conditions.

3. **Memory Allocation**:
   - The **kernel** manages memory through the **buddy system** for allocating chunks of memory.
   - It also uses **slab allocator** for efficiently managing small, frequently allocated memory blocks (e.g., kernel objects).

4. **OOM Killer**:
   - If the system runs out of memory, the **OOM killer** is invoked by the kernel to terminate processes that are using excessive memory to free up resources. It's usually triggered when swap space is also exhausted.

5. **Monitoring Memory Usage**:
   - Use `free`, `top`, `htop`, `vmstat`, `ps`, and `/proc/meminfo` to monitor memory usage and identify potential issues like memory leaks or high memory consumption.

---

### **Connectivity Troubleshooting**

#### **1. SSH (Secure Shell)**

**Common Issues:**
- **Connection Timeout**: The SSH client can't reach the server due to network issues, firewall configurations, or incorrect hostnames.
- **Authentication Failure**: Wrong username/password or SSH keys not set up correctly.
- **Permission Denied**: Incorrect permissions on SSH files (like `~/.ssh/authorized_keys`).
  
**Troubleshooting Steps**:
1. **Check SSH Daemon Status**:
   - Ensure SSH is running on the server:
     ```bash
     systemctl status sshd
     ```
2. **Check Firewall**:
   - Ensure that the firewall allows SSH traffic on port 22 (default):
     ```bash
     firewall-cmd --list-all
     ```
3. **Check Hostname & IP Address**:
   - Verify the correct IP address or hostname is being used:
     ```bash
     ping <hostname/IP>
     ```
4. **Check SSH Configuration**:
   - Review the `/etc/ssh/sshd_config` file for configuration issues (like `PermitRootLogin` or `PasswordAuthentication` settings).
5. **Enable Debug Mode**:
   - Run SSH client in debug mode for more verbose output:
     ```bash
     ssh -v user@hostname
     ```

#### **2. NFS (Network File System)**

**Common Issues**:
- **Mounting Issues**: NFS client cannot mount shared directories.
- **Permission Denied**: The NFS server denies access to clients due to incorrect permissions.

**Troubleshooting Steps**:
1. **Check NFS Service Status**:
   - Ensure the NFS server is running:
     ```bash
     systemctl status nfs-server
     ```
2. **Check /etc/exports**:
   - Review `/etc/exports` on the server to ensure the correct directories are being shared and clients are allowed to mount them.
     Example:
     ```bash
     /shared/dir 192.168.1.0/24(rw,sync)
     ```
3. **Check Mount Command**:
   - Use `mount` on the client side to manually attempt the NFS mount and check for errors:
     ```bash
     mount -t nfs <server-ip>:/shared/dir /mnt
     ```
4. **Firewall Configuration**:
   - Ensure the NFS ports are open on both client and server firewalls.
     ```bash
     firewall-cmd --list-all
     ```

#### **3. SFTP (Secure File Transfer Protocol)**

**Common Issues**:
- **Connection Refused**: The SFTP server is not running, or SSH is not configured to allow SFTP.
- **Authentication Issues**: Incorrect credentials or missing keys.

**Troubleshooting Steps**:
1. **Verify SSH Daemon**:
   - Ensure that the SFTP server (which runs over SSH) is active:
     ```bash
     systemctl status sshd
     ```
2. **Check Permissions**:
   - Ensure the user has correct permissions to access the directories they are trying to SFTP into.
3. **Use Debug Mode**:
   - Run the SFTP client with debug mode:
     ```bash
     sftp -vvv user@hostname
     ```

#### **4. FTP (File Transfer Protocol)**

**Common Issues**:
- **Connection Timeout**: FTP client cannot reach the server.
- **Permission Denied**: Incorrect file or directory permissions.
- **Passive/Active Mode Issues**: Misconfigurations between passive or active modes for FTP data transfer.

**Troubleshooting Steps**:
1. **Check FTP Service**:
   - Verify the FTP server is running:
     ```bash
     systemctl status vsftpd
     ```
2. **Firewall and NAT**:
   - FTP requires additional ports (21 for control, and a range of ports for data). Check if these ports are open on both the client and server.
3. **Check Configuration**:
   - Review `/etc/vsftpd.conf` for any misconfigurations (e.g., `pasv_enable`, `anonymous_enable`).
4. **Use Passive Mode**:
   - If behind a NAT, configure FTP clients to use passive mode.

#### **5. DNS (Domain Name System)**

**Common Issues**:
- **DNS Resolution Failures**: Unable to resolve domain names to IP addresses.
- **Wrong DNS Server Configuration**: Misconfigured DNS servers.

**Troubleshooting Steps**:
1. **Check DNS Resolution**:
   - Use `dig` or `nslookup` to test domain resolution:
     ```bash
     dig example.com
     nslookup example.com
     ```
2. **Check /etc/resolv.conf**:
   - Ensure DNS servers are configured correctly in `/etc/resolv.conf`.
     Example:
     ```bash
     nameserver 8.8.8.8
     ```
3. **Check Network Configuration**:
   - Ensure that the server has correct network configuration and can access DNS servers.

#### **6. Packet Flow Troubleshooting**

**Common Issues**:
- **Network Communication Failure**: Packet drops or slow communication between systems.

**Troubleshooting Steps**:
1. **Ping and Traceroute**:
   - Use `ping` to check connectivity:
     ```bash
     ping <destination-IP>
     ```
   - Use `traceroute` to trace the packet’s path to its destination:
     ```bash
     traceroute <destination-IP>
     ```
2. **Check Routing Table**:
   - Review the system’s routing table:
     ```bash
     route -n
     ```
3. **Check Firewall**:
   - Verify that the firewall is not blocking the required packets:
     ```bash
     firewall-cmd --list-all
     ```
4. **Tcpdump and Wireshark**:
   - Use `tcpdump` or Wireshark to capture and analyze packets in transit:
     ```bash
     tcpdump -i eth0
     ```

---

### **Summary of Key Troubleshooting Steps:**
- **SSH**: Use `-v` for debug output and check the SSH daemon.
- **NFS**: Ensure the NFS server is running and check `/etc/exports`.
- **SFTP**: Check SSH and user permissions.
- **FTP**: Check for correct firewall rules, passive mode, and FTP service status.
- **DNS**: Use `dig`, `nslookup`, and check `/etc/resolv.conf`.
- **Packet Flow**: Use `ping`, `traceroute`, `tcpdump`, and check routing and firewall settings.

By systematically following these steps, you can resolve most connectivity and memory-related issues on Linux systems.
