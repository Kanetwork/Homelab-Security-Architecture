# Security Audit

## Objective
Establish a security baseline for Ubuntu 24.04.3 LTS to identify vulnerabilities and support threat model analysis, enabling the development of a structured and tested hardening plan.

## Scope
This audit evaluates the security posture of an Ubuntu 24.04.3 LTS server. The assessment focuses on the following security domains:

- Operating system configuration
- Installed services and software exposure
- Network exposure and listening services
- User accounts and privilege configuration
- Logging and monitoring capabilities
- Firewall and network security controls

## Audit Commands Used
### User & Account Auditing

#### <u>List all users </u>

        cut -d: -f1 /etc/passwd
Purpose: Cut isolates the first column (usernames) from the user database.

Rationale: To inventory every account. Many are system services (like bin or sys), not humans.

Expected results: You should recognize all "human" names. Any unexpected name is a red flag.

#### <u>Find accounts with UID 0 (root privileges)</u>
        awk -F: '($3 == "0") {print $1}' /etc/passwd
Purpose: awk filters for users where the 3rd column (UID) is 0.

Rationale: UID 0 is the "root" ID. Only the account named root should typically have this power.

Expected Results: Only root should appear. Multiple UID 0 accounts often indicate a "backdoor."

#### <u>Show usernames + UID</u>     
        awk -F: '{print $1, $3}' /etc/passwd
Purpose: Displays usernames alongside their unique ID numbers

Rationale: To map names to IDs, helping you distinguish between system accounts (usually < 1000) and users.

Expected Results: User IDs for humans usually start at 1000 on modern Ubuntu systems.

#### <u>List normal users (home directories)</u>
        awk -F: '$6 ~ /^\/home/ {print $1, $6}' /etc/passwd
Purpose: Filters for users who have a directory in /home/

Rationale: Identifies "real" users versus background service accounts.

Expected Results: A list of known users who have a home directory.

#### <u>Check "nobody" account</u>
        grep nobody /etc/passwd
Purpose: Searches for the specific nobody user entry.

Rationale: nobody is a low-privilege account used by some services. It should not own files or have a shell.

Expected Result: The entry should usually end in /usr/sbin/nologin or /bin/false.

### Group & Privilege Auditing

#### <u>Show sudo group members</u>
        grep -Po '^sudo.+:\K.*$' /etc/group
Purpose: Extracts the list of members in the sudo group

Rationale: These users can run any command as root. This is the "hit list" for an attacker.

Expected Results: This list should be extremely short. Only trusted administrators belong here.

### Network & Service Monitoring

#### <u>Show listening services and ports</u>
        ss -tulpn
Purpose: Shows tcp/udp listening processes with numbers.

Rationale: To see what services are waiting for a connection

Expected Results: Only essential services (e.g., SSH on 2222). If you see vnc or telnet, close them

#### <u>Check what is using port 8080</u>
        sudo lsof -i :8080
Purpose: List Open Files on port 8080.

Rationale: To identify exactly which application is using a specific port.

Expected Result: Useful for troubleshooting or finding "ghost" web servers.


#### <u>Firewall status</u>
        sudo ufw status verbose
Purpose: Shows the Uncomplicated Firewall rules.

Rationale: To verify if the server's "shield" is actually turned on.

Expected Results: Status should be active. Default should be deny (incoming).

### Software & Package Monitoring

#### <u>Show all installed packages</u>
        apt list --installed
Purpose: Lists every software package on the system

Rationale: To look for "bloatware" or dangerous tools like compilers (gcc) or network sniffers.

Expected Results: A long list, but one you should periodically audit for "software rot."

#### <u>Show manually installed packages</u>
        apt-mark showmanual
Purpose: Shows packages you specifically told Ubuntu to install.

Rationale: To separate your intentional choices from the background dependencies

Expected Results: Items you recognize (e.g., nginx, docker).

#### <u>Show recent installs</u>
        grep " install " /var/log/dpkg.log | tail -25
Purpose: Searches the install logs for the 25 most recent additions.

Rationale: To see if software was installed recently without your knowledge.

Expected Results: Should match your own maintenance history.
### Process Monitoring

#### <u>Show running processes in tree format</u>
        ps auxf
Purpose: Displays all running processes in a "tree" (forest) view.

Rationale: To see if a legitimate process (like apache) has "given birth" to a suspicious one (like sh).

Expected Results: Processes should look organized. A shell (sh) running under a web server is a bad sign.

#### <u>Find SUID/SGID binaries</u>
        find / -perm /6000 -type f 2>/dev/null
Purpose: Finds files with SUID/SGID bits (special permissions).

Rationale: These files run with the power of their owner (root), regardless of who clicks them.

Expected Results: A standard list of binaries like passwd or sudo. New or strange files here are high risk

### Login & Authentication Monitoring

#### <u>Show login history</u>
        last -a
Purpose: Shows a history of who logged in and from where.

Rationale: To check for logins from strange IP addresses or at weird times (e.g., 3:00 AM)

Expected Results: You should see your own IP address and login times.

#### <u>Show failed login attempts</u>
        sudo grep "Failed password" /var/log/auth.log
Purpose: Searches the auth log for failed login attempts.

Rationale: To see if bots are trying to "brute-force" (guess) your passwords.

Expected Results: If the server is public, you will see many attempts. This justifies using SSH keys.