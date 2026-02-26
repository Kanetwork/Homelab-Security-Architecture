# Ubuntu 24.04.3 LTS Security Baseline Audit

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

<!--## Audit Methodology
Explain HOW you performed the audit.

Include:
- Manual configuration review
- Command line enumeration
- Security best practice comparison
- Reference standards (CIS Benchmarks, etc.)
- [Full Audit Here](/03-Security-Control/Security-Audit.md)-->

## Results

<br>

<table border="1" style="width: 100%; border-collapse: collapse;">
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #0228fd;">
      Environment
    </th>
  </tr>

  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Virtualisation Platform</td>
    <td style="text-align: center; padding: 10px;">Ubuntu 24.04.3 LTS</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold; ">Server Configuration</td>
    <td style="text-align: center; padding: 10px;">Ubuntu Server 24.04.3 LTS</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Network Configuration</td>
    <td style="text-align: center; padding: 10px;">Internal NAT network</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Connected Systems</td>
    <td style="text-align: center; padding: 10px;">1. Parrot OS attack VM used for validation testing <br> 2. Administrator workstation VM used for management tasks</td>
  </tr>
</table>

<br>

<table border="1" style="width: 100%; border-collapse: collapse;">
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #025e19;">
     System Information
    </th>
  </tr>

  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">OS</td>
    <td style="text-align: center; padding: 10px;">Oracle VirtualBox</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold; ">Kernel</td>
    <td style="text-align: center; padding: 10px;">Ubuntu Server 24.04.3 LTS</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Host Role</td>
    <td style="text-align: center; padding: 10px;">Internal Server.</td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Installed Packages</td>
    <td style="text-align: center; padding: 10px;">1. SSH <br> 2. Docker</td>
  </tr>
</table>

<br>

<table border="1" style="width: 100%; border-collapse: collapse;">
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #ff0505;">
     Audit
    </th>
  </tr>
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #706f6f;">
    User & Account Auditing
    </th>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">List all users</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold; ">Find accounts with UID 0 (root privileges)</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show usernames + UID</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">List normal users (home directories)</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Check "nobody" account</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #706f6f;">
    Group & Privilege Auditing
    </th>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show sudo group members</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show listening services and ports</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Check what is using port 8080</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Firewall status</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #706f6f;">
    Software & Package Monitoring
    </th>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show all installed packages</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show manually installed packages</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show recent installs</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #706f6f;">
    Process Monitoring
    </th>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show running processes in tree format</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Find SUID/SGID binaries</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <th colspan="2" style="text-align: center; padding: 10px; background-color: #706f6f;">
    Login & Authentication Monitoring
    </th>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show login history</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>
  <tr>
    <td style="text-align: center; padding: 10px; font-weight: bold;">Show failed login attempts</td>
    <td style="text-align: center; padding: 10px;"><!--Result--></td>
  </tr>

</table>