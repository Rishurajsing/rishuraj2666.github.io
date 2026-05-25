# rishuraj2666.github.io

# 🛡️ RISHURAJ SINGH
### **Offensive Security Research & Vulnerability Intelligence**

---

[![Bugcrowd](https://img.shields.io/badge/Bugcrowd-rishuraj2666-orange?style=for-the-badge&logo=bugcrowd&logoColor=white)](https://bugcrowd.com/rishuraj2666)
[![Intigriti](https://img.shields.io/badge/Intigriti-rishuraj2666-blue?style=for-the-badge&logo=securityscorecard&logoColor=white)](https://intigriti.com)
[![HackerOne](https://img.shields.io/badge/HackerOne-rishusec-lightgrey?style=for-the-badge&logo=hackerone&logoColor=white)](https://hackerone.com)

🚀 **[Rishuraj2666@gmail.com](mailto:Rishuraj2666@gmail.com)** | 🌐 **[rishuraj2666.github.io](https://rishuraj2666.github.io)**


---

## 💻 Executive Profile
> High-accuracy offensive security researcher specializing in application security, architectural logic flaws, and automated exploit development. Proven track record of identifying high-severity systemic issues across enterprise targets within major crowdsourced security platforms.

---

## 🎓 Academic Foundation
* **Post Graduate Program (PGP) in Cybersecurity** — *IIIT Bangalore*
* **Academic Minors in Computer Science Engineering & Advanced Technologies** — *IIT Mandi*

---

## 📊 Platform Track Record
* **Bugcrowd Queue Triage:** Maintained a **90% Signal/Accuracy Rating** across enterprise perimeters.
  * *Alternative Routing:* `rishuraj266@bugcrowdninja.com`
* **Intigriti Ecosystem:** **Verified Researcher Status** awarded following high-impact vulnerability validation and responsible disclosure.

---

## 🔍 Featured Security Research

### 🔴 High/Critical Logic State Bypass
*In Review for Public Whitepaper Release / Responsible Disclosure Pending*
* **Core Focus:** Structural exploitation of multi-tenant session states. Currently converting this validated finding into a formal architectural root-cause analysis.

---

## 🛠️ Automated Exploit PoCs

### Concurrency Validation Engine
A production-grade lab simulation script designed to execute multi-threaded race-condition testing against isolated session nodes.

```python
import requests
import concurrent.futures

TARGET_URL = "[https://target-app.com/api/v1/resource](https://target-app.com/api/v1/resource)"
HEADERS = {"Authorization": "Bearer TEST_TOKEN"}

def validate_state(thread_id):
    try:
        response = requests.get(TARGET_URL, headers=HEADERS, timeout=5)
        if response.status_code == 200:
            print(f"[+] Thread {thread_id}: Node responding securely.")
    except requests.exceptions.RequestException:
        print(f"[-] Thread {thread_id}: Connection failed.")

def run_suite():
    print("[*] Launching Concurrency Verification Suite...")
    with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
        executor.map(validate_state, range(5))

if __name__ == "__main__":
    run_suite()
