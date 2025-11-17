# Penetration Testing Tool (Mini-Nmap + Mini-SQLMap)

This project is a Python-based vulnerability scanner created as part of a cybersecurity curriculum. It integrates several modules to perform an end-to-end penetration test workflow: Reconnaissance, Scanning, Detection, optional Proof-of-Concept, and Reporting.

The tool crawls a target web application, enumerates endpoints, performs network discovery, and tests for common web vulnerabilities like SQL Injection and Cross-Site Scripting.

> **Ethical Hacking Disclaimer**
> This tool is intended strictly for educational purposes and for use in isolated, controlled lab environments (such as DVWA, OWASP Juice Shop, or Metasploitable2). Running this tool against any system without explicit prior authorization is illegal and unethical. The authors are not responsible for any misuse.

---

## 🚀 Key Features

* **Web Crawler:** Discovers pages, links, and forms on the target site.
* **Port Scanner:** A multi-threaded TCP scanner to find open ports and grab service banners.
* **Passive Analyzer:** Checks for missing security headers, insecure cookie configurations, and exposed sensitive paths (like `.git` or `/admin`).
* **Active Vulnerability Scanner:**
    * **SQLi Detector:** Tests for both Error-Based and Boolean-Based SQL Injection.
    * **XSS Detector:** Uses unique tokens to test for Reflected Cross-Site Scripting.
* **Safe PoC Module:** (Optional) Safely demonstrates the impact of found vulnerabilities using non-destructive payloads (e.g., time-based SQLi, `alert()` for XSS).
* **HTML Report Generator:** Produces a single, comprehensive HTML file detailing all findings, their severity, and clear remediation advice.

---

## 🛠️ Project Structure

The tool is organized into a main controller and a `modules` directory, where each file represents a different phase of the project.
 
 ## ⚙️ Installation

1.  Clone or download this repository to your local machine.
2.  Navigate to the project directory:
    ```bash
    cd pentest_project
    ```
3.  Install the required Python libraries using `pip`:
    ```bash
    pip install -r requirements.txt
    ```
    (Note: On some systems, you may need to use `pip3` instead of `pip`)

---

## ▶️ How to Run

The entire scan is orchestrated by the `runall.py` script.

1.  From the `pentest_project` directory, run the script:
    ```bash
    python runall.py
    ```
    (Note: On some systems, you may need to use `python3` instead of `python`)

2.  The script will prompt you for all necessary information:
    * **Target Base URL:** (e.g., `http://testphp.vulnweb.com`)
    * **Crawl Depth:** (e.g., `2`)
    * **Port Scan Range:** (e.g., `1` to `1024`)
    * **Run PoC Module? (y/n):** Whether to attempt the safe PoC.

3.  The tool will log its progress to the console and to `pentest_run.log`.
4.  When complete, a final HTML report (e.g., `Scan_Report_testphp_vulnweb_com_...html`) will be generated and automatically opened in your default web browser.

---

## 🔧 Tools & Methodology

* **Primary Language:** Python 3 (The code uses features specific to Python 3)
* **Core Libraries:**
    * `requests` & `BeautifulSoup4`: For crawling and HTTP interactions
    * `socket`: For low-level port scanning
    * `concurrent.futures`: For multi-threading the port scanner
* **Methodology:** The scan follows a logical flow: Crawl -> Passive Scan (Headers, Paths) -> Network Scan (Ports) -> Active Scan (SQLi, XSS) -> (Optional) PoC -> Report.