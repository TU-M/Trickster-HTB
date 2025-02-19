# Trickster Exploitation Report

## About Trickster
Trickster is a medium-difficulty Linux machine featuring multiple vulnerabilities across different services. This report outlines the process of exploiting these vulnerabilities to achieve full system compromise.

## Exploitation Steps

1. **Exploiting PrestaShop (CVE-2024-34716)**  
   - PrestaShop, an open-source e-commerce platform, is vulnerable to an XSS attack when the customer-thread feature flag is enabled.
   - By exploiting this vulnerability, we inject a malicious script that allows us to extract admin session tokens.
   - Using these credentials, we gain access to the remote server as the `www-data` user.

2. **Extracting Database Credentials**  
   - Further enumeration reveals PrestaShop configuration files containing database credentials.
   - These credentials allow us to dump password hashes.
   - Cracking these hashes provides access to user `james`, enabling SSH access.

3. **Exploiting ChangeDetection.io (CVE-2024-32651)**  
   - A Docker container running ChangeDetection.io is discovered on the system.
   - This application is vulnerable to Server-Side Template Injection (SSTI), allowing Remote Code Execution (RCE).
   - Exploiting this vulnerability provides a root shell within the container.

4. **Extracting User Credentials from Backups**  
   - Inside the container, backup files from ChangeDetection.io reveal the credentials for user `adam`.
   - With these credentials, we SSH into the system as `adam`.

5. **Privilege Escalation via PrusaSlicer (CVE-2023-47268)**  
   - The PrusaSlicer tool on the system is vulnerable to a privilege escalation exploit.
   - By leveraging this vulnerability, we escalate privileges and obtain a root shell on the host system.

## Conclusion
By chaining together multiple vulnerabilities—XSS in PrestaShop, SSTI in ChangeDetection.io, and privilege escalation in PrusaSlicer—we achieve full system control over the Trickster machine.

