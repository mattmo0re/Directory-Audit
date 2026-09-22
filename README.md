# Directory-Audit

<img width="862" height="372" alt="Screenshot 2026-09-22 182531" src="https://github.com/user-attachments/assets/9e13227a-3ff1-44c6-9915-374017b5ec78" />

Writable Directory Auditor Scan for world-writable directories (find / -perm -0002 -type d) that standard user profiles can access, tracking down spots where external threat actors could potentially stage drops or execute rootkits.

Highlights of this design:Anti-Crash / Pure Logic: It uses set -euo pipefail to ensure structural errors stop immediately, but safely paths around permissions denials (2>/dev/null).Noise Filtering: In threat engineering, scanning /proc or /sys drops performance to zero and yields hundreds of fake alerts. This programmatically builds arguments to completely bypass them.TTP Execution Risk-Rating: It doesn't just check if a standard user can write to the directory—it actively checks if the world-executable permission bit is set (perms:8:1). Directories with write permissions but without execute rights are harder for automated baseline implants to misuse.
