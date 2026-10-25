# CS 305 Software Security – Portfolio (Noah Kersey)

**Artifact:** [Artemis Financial Practices for Secure Software Report](CS305_Project_Two_Practices_for_Secure_Software_Noah_Kersey.docx) (Project Two)

## Reflection

**Client and requirements.** Artemis Financial is a consulting company that builds individualized financial plans for its customers, covering savings, retirement, investments, and insurance. It wanted to modernize its operations with a secure web-based RESTful API. My job was to find the security vulnerabilities in its Spring Boot application, then refactor the code. The refactoring added a secure checksum for verifying data integrity and moved all traffic from HTTP to HTTPS so client data stays protected in transit.

**What I did well and why secure coding matters.** I was thorough. I combined a manual code review with an automated OWASP Dependency-Check scan and mapped each finding to the areas of the vulnerability assessment process flow diagram, such as input validation, APIs, cryptography, client/server, and code quality. I then prioritized fixes by severity. Secure coding matters because a single unpatched library or weak cipher can expose customers' financial data. Software security protects a company's reputation, keeps it compliant with regulations, avoids the cost of breaches, and builds the trust that keeps clients coming back.

**Challenging or helpful parts.** The most challenging part was the dependency work. The original Spring Boot 2.2.4 code base carried roughly 150 known CVEs, and it could not run the current Dependency-Check plugin. Working through upgrades until the scan came back clean taught me how much risk lives in third-party libraries, not just in the code you write yourself. The process flow diagram was helpful because it gave me a structured checklist, so nothing was skipped.

**Increasing layers of security.** I added layers instead of relying on one control:
- **Data integrity:** a SHA-256 checksum endpoint.
- **Encrypted transport:** HTTPS on port 8443 using a keystore and a certificate generated with Java Keytool, restricted to TLS 1.2 and 1.3.
- **Patched dependencies:** libraries upgraded to supported versions.
- **Documented suppressions:** each false positive suppressed with a written reason and a review date.

In the future, I would keep using OWASP Dependency-Check, the NVD and CVE databases, and the OWASP Top 10 to assess vulnerabilities. I would choose mitigations based on CVSS severity, exploitability, and the business impact on the client.

**Keeping the code functional and secure.** I ran the application and confirmed that `https://localhost:8443/hash` returned the expected data string and SHA-256 checksum. I verified the checksum independently and confirmed that the TLS connection was established. I also ran automated tests and did a manual functional review of the refactored code. After refactoring, I re-ran the Dependency-Check scan and compared the results with the original assessment to make sure no new vulnerabilities had been introduced. The final scan reported zero open vulnerabilities.

**Useful resources, tools, and practices.** These will carry into future work:
- OWASP Dependency-Check with an NVD API key, Maven, Java Keytool, and the Java Cryptography Architecture (`MessageDigest`)
- Spring Boot SSL configuration
- The OWASP Top 10
- Secure coding practices: keeping secrets out of source code and properties files, validating input, handling errors without leaking details, and keeping dependencies current

**What I would show employers.** This report shows that I can assess an application for vulnerabilities, explain the findings clearly to a client, and refactor code to fix them. It covers implementing cryptographic hashing, configuring HTTPS with certificates, managing dependency risk, and verifying that a fix actually worked. Those skills apply directly to secure software development and DevSecOps roles.
