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

## 🔬 Research Whitepaper: Architectural Analysis of Response Manipulation & Client-Side State Injection in GraphQL-Based Authentication Gateways

**Author:** Rishuraj Singh  
**Focus:** Offensive Security Research / Vulnerability Intelligence  
**Date:** May 2026  

### Abstract
Modern decentralized applications and financial platforms increasingly rely on GraphQL APIs to orchestrate complex user onboarding and Know Your Customer (KYC) workflows. This whitepaper analyzes a structural architectural pattern where the decoupling of frontend application logic from backend state validation introduces critical client-side vulnerabilities. Specifically, we investigate the mechanics of **Response Manipulation and State Injection** within GraphQL verification schemas (`verifyPhone`), demonstrating how an attacker can manipulate boolean indicators (`"verifyPhone": true`) to completely subvert frontend authentication gates. Finally, we evaluate the systemic operational risks of this behavior and propose mitigation strategy rules for server-side state enforcement.

### 1. Introduction & Architectural Context
In traditional RESTful architectures, multi-step validation processes often rely on explicit server-side session tokens generated per transaction step. Conversely, contemporary GraphQL endpoints frequently design lightweight mutation queries to handle atomic actions, such as One-Time Password (OTP) verification. 

When a client queries a GraphQL gateway, the architecture often uses a unified structure where responses are mapped directly to client-side state management frameworks (e.g., Apollo Client, Redux). If the client application state implicitly trusts the Boolean resolution of a GraphQL mutation array without checking a corresponding cryptographically signed state token on subsequent requests, a critical logic gap emerges between the presentation layer and the server-side access control boundary.

### 2. Vulnerability Mechanism: GraphQL State Injection
The vulnerability lies in the client-side execution framework's absolute trust in downstream proxy traffic. During an outbound phone validation sequence, the client transmits an identity token or temporary contact number to the staging sandbox endpoint:

`POST /graphql HTTP/2`  
`Host: api-sandbox.uphold.com`

#### 2.1 Native Error Response
When an invalid or arbitrary OTP token is injected by the client, the backend correctly processes the syntax failure and returns a structured GraphQL validation error array:

```http
HTTP/2 200 OK
Alt-Svc: h3=":443"; ma=86400
Content-Type: application/json

{
  "errors": [
    {
      "message": "Validation Failed",
      "locations": [{"line": 1, "column": 101}],
      "path": ["verifyPhone"],
      "code": 400,
      "errors": {
        "token": [{"code": "invalid", "message": "This value is not valid"}]
      }
    }
  ],
  "data": null
}

##2.2 Response Tampering & Injected State
Because the application pipeline evaluates the data array structure to determine UI rendering paths, an attacker intercepting the runtime traffic via a localized proxy (e.g., Burp Suite) can strip the error stack entirely and inject an affirmative boolean payload into the stream:

HTTP/2 200 OK
Alt-Svc: h3=":443"; ma=86400
Content-Type: application/json

{
  "data": {
    "verifyPhone": true
  }
}
Upon receiving this forged structural data packet, the client-side routing controller updates its local authentication context state, explicitly marking the current workflow branch as validated and unlocking restricted verification layers.
3. Attack Vector & Execution Flow
1 Interception Phase: Outbound verification requests are mapped using transient, random parameters to bypass unique tracker limitations.
2 Execution Phase: The structural logic failure response is caught post-execution by the testing agent's local environment.
3 Exploit Phase: The raw downstream payload is dynamically rewritten to represent an active execution state (⁠true⁠), causing the application layer to drop safety barriers.
4. Threat Landscape Impact Analysis
While modern systems may maintain zero-trust backend logic that blocks final database entry writes if the initial validation states don't align on the server side, response manipulation of this nature introduces compounding threat vectors:
 Deceptive KYC Compliance Paths: Attackers can bypass localized identification walls to map deeper structural application layout surfaces, escalating overall attack footprints.
 Denial of Service via State Desynchronization: Forcing frontend components into authenticated states while the backend maintains an unauthenticated posture generates extreme data friction, potentially exposing application-level trace routes or error logs useful for crafting complex chained exploits.
5. Architectural Remediation & Mitigation Matrix
To eliminate vulnerabilities arising from client-side state injection, developers should replace the standard boolean return design with strict cryptographic verification flows.
 State Trust: Client must not trust local response arrays. Server should issue short-lived, signed cryptographic nonces upon successful validation.
 Logic Checks: Presentation layer must not gate workflows alone. Multi-stage workflows require server-verified session states at every interaction step.
 API Errors: Avoid structural 200 OK headers containing application-level errors. Use native HTTP strict status codes matching GraphQL error categories.
Implementation Blueprint:
# Recommended Secure State Schema Change
type VerifyPhonePayload {
  success: Boolean!
  stateVerificationToken: String! # Cryptographically signed server-side token containing timestamped session hash
}

All subsequent onboarding mutations must explicitly demand the ⁠stateVerificationToken⁠ as an mandatory parameter header, verifying its signature server-side before processing user registration data.


🛠️ Automated Exploit PoCs
Concurrency Validation Engine
A production-grade lab simulation script designed to execute multi-threaded race-condition testing against isolated session node

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
