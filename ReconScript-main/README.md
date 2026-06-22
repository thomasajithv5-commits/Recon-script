# ReconScript

A custom Bash script designed to automate basic infrastructure reconnaissance and vulnerability scanning.

## 🛠️ Features

The script provides an interactive command-line menu with two main automation tracks:

1. **Nmap Scan**
   * Prompts for a target address.
   * Runs an aggressive scan (`-A`) with service version detection (`-sV`) across all 65,535 ports (`-p1-65535`).

2. **OSINT Framework (Subfinder + Httpx + Nuclei)**
   * Prompts for a target domain.
   * **Subfinder:** Passively gathers subdomains and saves them to a temporary file.
   * **Httpx-toolkit:** Validates live HTTP/HTTPS servers, extracting status codes and page titles.
   * **Nuclei:** Automatically checks the validated live hosts for known vulnerabilities.

## 🚀 Usage Guide

1. Make the script executable:
```bash
   chmod +x recon.sh
