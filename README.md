# Trickster-HTB
This report details exploiting Trickster via an XSS in PrestaShop (CVE-2024-34716) to gain www-data access, extracting database credentials for SSH as james. A root shell in Docker is obtained via ChangeDetection.io (CVE-2024-32651), revealing adam’s credentials, followed by root escalation with CVE-2023-47268 in PrusaSlicer.
