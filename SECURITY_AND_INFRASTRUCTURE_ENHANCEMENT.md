# Security & Infrastructure Enhancement Blueprint

## Target Projects
- [vulnerability management](file:///G:/My%20Drive/Antigravity/Projects/vulnerability%20management)
- [MY Security](file:///G:/My%20Drive/Antigravity/Projects/MY%20Security)
- [ai defense](file:///G:/My%20Drive/Antigravity/Projects/ai%20defense)
- [RHCSA Exam200](file:///G:/My%20Drive/Antigravity/Projects/RHCSA%20Exam200)
- [Scripting](file:///G:/My%20Drive/Antigravity/Projects/Scripting)
- [openshift](file:///G:/My%20Drive/Antigravity/Projects/openshift)
- [aws](file:///G:/My%20Drive/Antigravity/Projects/aws)
- [windows event viewer](file:///G:/My%20Drive/Antigravity/Projects/windows%20event%20viewer)
- [bot finder](file:///G:/My%20Drive/Antigravity/Projects/bot%20finder)
- [spam block](file:///G:/My%20Drive/Antigravity/Projects/spam%20block)
- [reverse engineer applications](file:///G:/My%20Drive/Antigravity/Projects/reverse%20engineer%20applications)
- [REA](file:///G:/My%20Drive/Antigravity/Projects/REA)
- [docker](file:///G:/My%20Drive/Antigravity/Projects/docker)
- [opensource](file:///G:/My%20Drive/Antigravity/Projects/opensource)
- [Cert Training Guide](file:///G:/My%20Drive/Antigravity/Projects/Cert%20Training%20Guide)
- [Popular Github Projects](file:///G:/My%20Drive/Antigravity/Projects/Popular%20Github%20Projects)

---

## 1. Vulnerability Management & MY Security: Cisco PSIRT, openvuln-mcp & Zero-Trust

### Cisco PSIRT openVuln & Model Context Protocol (`CiscoPSIRT/openvuln-mcp`)
- **Cisco Model Context Protocol Server (`openvuln-mcp`)**: 
  - Deploys an official MCP server at `https://apix.cisco.com/api/mcp/openvuln` exposing 12+ read-only tools to stream Cisco PSIRT advisories directly into AI security agents via Streamable HTTP JSON-RPC using OAuth 2.0 Client Credentials.
  - Allows autonomous agents to dynamically query security advisories by CVE, Cisco Bug ID, severity, or Network Operating System (NX-OS, IOS XR, ASA, ISE, APIC).
- **October 2026 High-Severity Cisco Advisory Ingestion**:
  - **CVE-2026-76418 (CVSS 8.6 - High / Actively Exploited in the Wild)**: Cisco Secure Firewall Adaptive Security Appliance (ASA) Software and Secure Firewall Threat Defense (FTD) Software Remote Access SSL VPN DoS via secondary authentication logic flaw (`cisco-sa-asaftd-tunnel-dos-s6mgkb75`). Unauthenticated remote attackers trigger a fatal crash and device reload by transmitting crafted connection handshake sequences.
    - **CISA KEV Status**: Cataloged with mandatory federal remediation deadlines.
    - **Fixed Software Releases**: ASA 9.16.4.104+, 9.18.4.96+, 9.20.4.50+, 9.22.3.200+, 9.23.1.48+, 9.24.1.27+; FTD 7.0.11+, 7.2.13+, 7.4.9+, 7.6.7+, 7.7.14+.
    - **Emergency Mitigation**: If unable to upgrade immediately, disable secondary authentication on vulnerable tunnel groups (`tunnel-group <name> general-attributes -> no secondary-authentication`) to eliminate the attack vector.
  - **CVE-2026-20349 (CVSS 8.6 - High / Actively Exploited in the Wild)**: Cisco ASA and FTD Software Remote Access SSL VPN HTTP request processing vulnerability (`cisco-sa-asaftd-vpn-dos-dzv4mQFF`). Unauthenticated remote attackers trigger device reloads (denial of service) by transmitting crafted HTTP requests to active SSL VPN or IKEv2 endpoints.
  - **CVE-2026-20271**: Cisco IOS and IOS XE Software IKEv2 control-flow and memory-leak denial of service vulnerability leading to resource exhaustion or unexpected reload under unauthenticated remote traffic.
  - **Cisco Secure Client Privilege Escalation (`cisco-sa-sec-client-priv-esc-muF8eZdm`)**: Secure Firewall Posture Module Local Privilege Escalation vulnerability via IPC channels.
  - **CVE-2026-76482 (CVSS 10.0 - Critical / Maximum Severity)**: Cisco Smart Software Manager On-Prem / License On-Prem security hardening release addressing unauthenticated remote privilege escalation.
  - **CVE-2026-76519 (CVSS 9.8 - Critical / Actively Exploited in the Wild)**: Cisco Secure Email Gateway relative path traversal in Advanced Malware Protection (AMP) feature allowing unauthenticated remote attackers to write arbitrary files and execute root commands via crafted email attachments (cataloged in CISA KEV - `cisco-sa-esa-afw-zqYJkjxp`).
  - **Cisco Secure Firewall ASA, FTD & FMC Hardening Release (`cisco-sa-hardening-asaftdfmc-uvpPROhN`)**: Comprehensive semiannual hardening update across Secure Firewall ASA, Threat Defense, and Management Center.
  - **Cisco Identity Services Engine Hardening Release (`cisco-sa-hardening-ise-XU5EwX5T`)**: ISE platform security hardening addressing administrative interface vulnerabilities.
  - **Cisco NX-OS & Data Center Hardening Batch**: Nexus 3000/7000/9000 Series, MDS 9000, and UCS Fabric Interconnect critical vulnerabilities:
    - **CVE-2026-76465 (CVSS 9.8)**: MPLS OAM Remote Code Execution.
    - **CVE-2026-76485, CVE-2026-76486, CVE-2026-76501 (CVSS 9.8)**: NGOAM Remote Code Execution.
    - **CVE-2026-76471 (CVSS 9.8)**: NX-API Remote Code Execution.
    - **CVE-2026-76453 through CVE-2026-76459**: General NX-OS hardening RCE bundle (`cisco-sa-hardening-nxosw1-cWzSbtR`).
  - **Cisco APIC**: API Command Injection and Hardening flaws (**CVE-2026-76498, CVE-2026-76499, CVE-2026-76500**, CVSS 9.8 - `cisco-sa-hardening-apic-UOXWtfh`).
  - **Cisco Expressway Series**: Static credential / Remote Code Execution (**CVE-2026-76466**, CVSS 9.8 - `cisco-sa-vcs-static-cred-hr7EWZ8t`) and client certificate validation hardening (`cisco-sa-exwy-hardening-FhcqBVcs`).
  - **Cisco Unified Communications Products**: Voice security hardening updates addressing remote execution and privilege escalation (`cisco-sa-voice-hardening-twgbH9e3`).
  - **Cisco FMC, ASA & FTD Semiannual Bundled Advisories**:
    - **Cisco Secure Firewall Management Center (FMC)**: SQL injection (`cisco-sa-fmc-sql-inject-2EnmTC8v`), command injection (`cisco-sa-fmc-cmd-inj-2HBkA97G`), and privilege escalation (`cisco-sa-fmc-priv-esc-CMQ4S6m7`).
    - **Cisco ASA & FTD Software**: Remote Access SSL VPN DoS vectors (`cisco-sa-asa-vpn-nyH3fhp`, `cisco-sa-asa-vpn-4gYEWMKg`) and AnyConnect/NSG ACL bypass vulnerabilities (`cisco-sa-asaftd-acl-bypass-VvnLNKqf`, `cisco-sa-asaftd-nsgacl-bypass-77XnEAsL`).
  - **Snort 3 Security Hardening Batch (`cisco-sa-hardening-snort3-ybgmhTQe`)**:
    - **CVE-2026-20043, CVE-2026-20236, CVE-2026-20291, CVE-2026-20356 (CVSS 9.0 - Critical)**: Multiple out-of-bounds write and code execution vulnerabilities in Snort 3 detection engine affecting Cisco Meraki MX, Secure Firewall Threat Defense (FTD), and Cloud-delivered Firewalls.
    - **CVE-2026-76524 (CVSS 7.8 - High)**: Open Source Snort 3 control channel socket arbitrary command execution flaw.
  - **PHP Core Corruptions ("php2shell")**: `cisco-sa-php-october26-Jj384Daq` covering CVE-2026-109618 and CVE-2026-109619 (CVSS 9.2) affecting web management appliances.
  - **Node.js Critical Runtime Flaws**: `cisco-sa-oct2026-node-js-Jj3SQ19u` addressing out-of-bounds write and potential RCE (**CVE-2026-111497**) in Brotli decoders integrated into management interfaces.
  - **November 2026 Disclosures, Hardening Releases, CISA KEV Additions & Cisco EOY Freeze**:
    - **OpenSSH Authentication Bypass ("SSHole" / CVE-2026-123158 - CISA KEV Cataloged November 9, 2026)**:
      - **Vulnerability**: CWE-394 (Unexpected status code / return value) password authentication bypass in OpenSSH (`sshd`) affecting versions up to 10.6p1 on Linux systems utilizing **musl libc** without Pluggable Authentication Modules (PAM)—most notably **Alpine Linux** container workloads.
      - **Root Cause & Attack Vector**: Accounts intended to be locked or restricted to key-only login carry an asterisk (`*`) in the password hash field in `/etc/shadow`. In `musl libc`, supplying an overlong password (between 256 and 1024 characters) triggers an internal error in `crypt()` that returns `*`. OpenSSH performs dummy password-hashing checks on locked accounts to mitigate timing attacks; because musl returns `*`, OpenSSH mistakenly treats this error string as a successful password match against `/etc/shadow`, granting immediate unauthorized shell access.
      - **Active Exploitation & CISA KEV**: Proof-of-concept exploits surfaced within hours of public disclosure; active in-the-wild exploitation against internet-facing cloud and container workloads was observed within 40 hours. Added to the **CISA Known Exploited Vulnerabilities (KEV) catalog on November 9, 2026** with mandatory remediation requirements.
      - **Remediation & Hardening**: Upgrade OpenSSH to **version 10.6p2+**; update Alpine Linux base images; or enforce `PasswordAuthentication no` globally in `/etc/ssh/sshd_config`.
    - **Cisco BroadWorks Remote Code Execution & XXE (`cisco-sa-bw-xxe-2026` / CVE-2026-20320 - CISA KEV Cataloged November 10, 2026)**: An XML External Entity (XXE) injection flaw residing within the Open Client Interface (OCI) XML parser of Cisco BroadWorks provisioning services. Allows unauthenticated remote attackers to read arbitrary configuration files and credentials, cause denial-of-service, or execute code. Confirmed actively exploited in the wild and **cataloged into CISA's Known Exploited Vulnerabilities (KEV) on November 10, 2026**; upgrade to release **RI.2026.07+** and rotate any potentially exposed credentials.
    - **Node.js Brotli Multi-Product Vulnerabilities (`CVE-2026-105482`, `CVE-2026-105483`)**: Upstream Brotli decoder out-of-bounds write flaws integrated into Cisco web management consoles, addressed via scheduled maintenance batches.
    - **Cisco Meraki OS Security Hardening Release (`cisco-sa-hardening-meraki-os-drbEX9GH`)**: Comprehensive software hardening release addressing multiple vulnerabilities discovered during internal security audits across the Cisco Meraki OS line. Grouped by Common Weakness Enumeration classes (CWE-682 incorrect calculation and improper input validation). No workarounds exist; software upgrades must be scheduled via the Meraki Dashboard.
    - **Cisco UCS Central Software Remote Code Execution (`cisco-sa-cucs-rce-LzHSFRDQ`)**: **CVE-2026-76506** (CWE-22 Path Traversal, CVSS Base Score 7.6, Bug ID `CSCwv60193`). Disclosed on November 4, 2026; unauthenticated remote attackers can execute arbitrary code with root/administrative privileges on the underlying Linux OS via crafted HTTP requests.
    - **Cisco Unified Communications Manager (CUCM) Cross-Site Scripting (`cisco-sa-cucm-xss-5mQn2U5z`)**: **CVE-2026-76419** (CVSS Base Score 6.1) affecting web-based administrative consoles (`cisco-sa-voice-hardening-twgbH9e3`).
    - **Cisco Identity Services Engine (ISE) Authorization Bypass (`cisco-sa-hardening-ise-XU5EwX5T`)**: **CVE-2026-20241** (CVSS Base Score 5.3, `CWE-285`) affecting internal certificate management services and administrative controls.
    - **Cisco End-of-Year Vulnerability Publication Freeze Notice (`cisco-sa-notice-I8z3n6lK`)**: Cisco PSIRT officially confirmed that following the November 4, 2026 batch, **no further security hardening advisories** will be published for the remainder of calendar year 2026. The next scheduled cycle for security-hardened releases is slated for **January 20, 2027**, establishing a fixed vulnerability freeze baseline for enterprise change control.
  - **Additional November 2026 CISA KEV Additions (Cross-Vendor Tracking)**:
    - **Google Chromium / Chrome (`CVE-2026-125350`, CVSS 8.8 - High / Actively Exploited)**: Use-After-Free (UAF) in XML/XSLT processing allowing sandboxed remote code execution via crafted pages; patched in **Chrome 157 (`157.0.8103.50/.51+`, 200+ total security fixes)** (8th Chrome zero-day in 2026). Mandatory verification across `Plugins`, `chrome tab and bar`, and desktop workstations.
    - **OpenJDK / Oracle Java "Java4Shell" (`CVE-2026-114938`, CVSS v4.0 9.2 Critical / CISA KEV Urgent)**: Out-of-bounds heap write (~62 bytes past buffer) in OpenJDK handwritten **AVX-512 VBMI** Base64 assembly decoder affecting Java 17.0.6+, 21, 25, 27, and SE 8 Performance Pack (`8u511b33-perf`) on x86-64 Ice Lake+ / Zen 4+ CPUs. Enables pre-auth RCE via Base64-decoded HTTP Basic Auth, tokens, SAML, and uploads across Spring Boot, Keycloak, Jira/Confluence, Jenkins, and Apache Kafka. Patch JDK immediately or apply x86-64 emergency workaround `-XX:UseAVX=2` (do not use on ARM64).
    - **Linux Kernel "NoisyTCP" (`CVE-2026-99288`, CVSS 7.5 High)**: 11-year-old ABA race condition in kernel TCP `ehash` socket lookup/free paths across multi-RX-queue / RPS hosts causing unauthenticated NULL-pointer dereference and remote kernel panic across web, SSH, and multi-tenant container hosts. Apply November 2026 RHEL/upstream kernel updates immediately.
    - **Microsoft Outlook (`CVE-2026-124194`)**: Missing user-interaction / spoofing vulnerability enabling NTLMv2 hash disclosure and user impersonation.
    - **Check Point Gaia OS (`CVE-2026-123039`)**: Incorrect permission assignment in DynamicCLI daemon enabling local privilege escalation to root.
    - **Barracuda Networks ESG (`CVE-2026-116606`, `CVE-2026-111560`)**: Critical authentication bypass and command injection chain leading to root compromise.
    - **IBM Aspera Faspex (`CVE-2026-123218`)**: Incorrect authorization flaw leading to privilege escalation.
    - **Mid-November 2026 Critical Exploits & CISA KEV Additions (Nov 13–20, 2026)**:
      - **Nov 20, 2026 CISA KEV Batch (BOD 26-04 — 3-Day Federal Remediation Deadline Nov 23, 2026)**:
        - **Cisco Expressway Series & Expressway Select (`CVE-2026-76466` — CVSS 9.8 Critical, CWE-798)**: Hard-coded credentials allowing unauthenticated remote attackers (with persistent cookies and cluster network access) to execute **root** commands on clustered devices via the database service; actively weaponized against enterprise edge gateways. **Mandatory Fix**: Upgrade clustered Expressway devices to **15.5.21+** (`cisco-sa-vcs-static-cred-hr7EWZ8t`), restrict cluster ports to trusted peers, and conduct forensic triage for unauthorized persistence.
        - **Apache Roller (`CVE-2026-129448` — CVSS 9.8 Critical)**: Untrusted data deserialization via the XML-RPC endpoint enabling unauthenticated RCE.
        - **Broadcom VMware vCenter (`CVE-2026-123890` — CVSS 9.8 Critical)**: Authentication bypass via alternate path/channel.
        - **SAP NetWeaver Enterprise Portal (`CVE-2025-42884` — CVSS 6.5)**: Unauthenticated JNDI property/URL injection.
      - **BerriAI LiteLLM Sandbox Escape & RCE (`CVE-2026-40217` — CISA KEV Added Nov 18, 2026)**: Hand-rolled Python sandbox in `/guardrails/test_custom_code` bypassed via runtime bytecode manipulation (chained with `CVE-2026-47101`/`47102` for root container RCE & LLMjacking credential theft). **Mandatory Fix**: Upgrade to `litellm >= 1.83.11` / `1.83.14-stable` (`RestrictedPython` replacement), block `POST /guardrails/test_custom_code` at WAF/gateway, and rotate all AI provider API keys.
      - **Linux Kernel Critical IPv4 TCP Use-After-Free (`CVE-2026-98432` / `RHSB-2026-016` — CVSS 9.8 Critical)**: Unauthenticated remote DoS/RCE triggered via crafted TCP SYN packets carrying IPv4 options (Timestamp / Record Route) racing connection setup across RHEL 8/9/10 (`RHSA-2026:93414`) and OpenShift 4.21/4.22 `ose-rhel-coreos` (`RHSA-2026:95408`). If reboot is temporarily deferred, apply Red Hat's `nftables` workaround filtering incoming IPv4 packets with unusual IP options.
      - **NGINX HTTP/2 "NGINX2Root" & Cisco Third-Party Advisories (`CVE-2026-123007`, `123633`, `113425`, `121810`) + ClamAV DoS**: Integer underflow in HTTP/2 flow control causing heap buffer overflow/RCE (`CVE-2026-123007`) and HTTP/2 upstream proxy draining UAF (`CVE-2026-123633`), alongside Cisco-tracked NGINX mail/HTTP RCE advisories (`CVE-2026-113425`, `CVE-2026-121810`) and **ClamAV DoS** vulnerabilities affecting Cisco Secure Endpoint Connectors on Windows, Linux, and macOS.
      - **Podman 5.8.x, Go Stdlib & Container Runtime Escapes (`RHSA-2026:100547` / `RHSA-2026:98554` / `97533` / `93464`) + Docker "CopyEscape" (`CVE-2026-17106`)**: Resolves Go stdlib DoS/MitM flaws (**`CVE-2026-78667`** `net/http` Range header DoS, **`CVE-2026-97031`** `crypto/tls` ECH outer extension DoS, **`CVE-2026-111943`** `crypto/x509` untrusted intermediate cert MitM, **`CVE-2026-46597`** `golang.org/x/crypto/ssh` AES-GCM DoS, `CVE-2026-33818`, `CVE-2026-56860`), **CRI-O `bind_mount_prefix` intermediate symlink bypass (`CVE-2026-76061`)**, **`sssd` protocol negotiation null-pointer dereference (`CVE-2026-127101`)**, rootless `podman-remote save` / `podman rm` Buildah mount cleanup bugs, TLS/mTLS on Podman API sockets, and malicious tar/OCI archive write (`CVE-2025-11395`). Upgrade RHEL 8/9/10 Podman (`sudo dnf upgrade podman podman-remote podman-docker`) and Docker Desktop.
      - **Additional Nov 13–22 CISA KEV & `r/netsec` / `r/cybersecurity` Intelligence**: **Perforce Puppet Enterprise (`CVE-2026-115731`, CVSS 9.4, Nov 17)** untrusted deserialization RCE; **Check Point Gaia OS (`CVE-2026-123039`, Nov 13)** DynamicCLI local root socket LPE; **UnrealIRCd (`CVE-2026-114713`, Nov 13)**; **Synology DSM (`CVE-2024-10441`, Nov 18)**; **Apache Axis (`CVE-2026-90436`, Nov 18)**; **REDCap (`CVE-2026-90817`, Nov 18)**; active **PHP2Shell (`CVE-2026-109618`/`109619`)** Mirai-loader exploit waves; **Anthropic Project Glasswing / Mythos** CVE floods (VulnCheck KEV-over-CVSS prioritization); **GitHub Actions & npm hook credential-stealing supply-chain attacks**; and **eBPF memory histograms + ML pressure scoring** for zero-day memory-corruption detection (`r/netsec` Nov 2026).
- **CSAF 2.0/3.0 JSON Feeds**: Automated parsing of Common Security Advisory Framework machine-readable feeds to pinpoint first-fixed software versions.
- **DefectDojo v2/v3 Aggregation**: Automated vulnerability deduplication, SLA breach alerting, and CVE tracking across scanned subnets.
- **NetBird Zero-Trust Network Access (`netbirdio/netbird`)**: Extend the C# security monitor to enforce WireGuard-based endpoint posture verification:
  - Verify BitLocker encryption status, Windows Defender real-time protection, OS build version, and local firewall profiles before granting network access.

### .NET 10 / C# High-Performance Codebase & Portfolio Security Hardening (Nov 18, 2026)
- **Production Security Hardening Middleware (`vulnerability management/Middleware/SecurityHardeningMiddleware.cs` & `MY Security/Program.cs`)**: Deployed across both .NET 10 security hubs on Nov 18, 2026, enforcing `Content-Security-Policy` (`frame-ancestors 'none'; base-uri 'self'; form-action 'self'`), `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `Referrer-Policy`, `Permissions-Policy`, `X-Permitted-Cross-Domain-Policies: none`, and strict same-origin `Origin`/`Referer` validation blocking cross-origin `POST`/`PUT`/`PATCH`/`DELETE` mutations (HTTP 403), paired with portfolio-wide `SECURITY.md` disclosure policies across 10+ repositories (`MY Security`, `vulnerability management`, `Popular Github Projects`, `using ai agents for profit`, `stock watch`, `screen reader`, `mobile game`, `email organizer`, `agent 365`, `AAC`).
- **Native AOT Compilation**: Compile scanning agents with Native AOT for zero-dependency, sub-10ms startup binaries that execute without a .NET runtime installed.
- **Memory-Efficient Streaming**: Use `IAsyncEnumerable<VulnerabilityRecord>` to stream port scan results and CVE matches directly to SQLite without memory spikes:
```csharp
public async IAsyncEnumerable<VulnerabilityRecord> ScanSubnetStreamAsync(
    string cidr, 
    [EnumeratorCancellation] CancellationToken ct = default)
{
    foreach (var ip in IPNetwork.Parse(cidr))
    {
        ct.ThrowIfCancellationRequested();
        var record = await ProbeHostAsync(ip, ct);
        if (record != null) yield return record;
    }
}
```

---

## 2. Windows Event Viewer & Threat Hunting: Sysmon & MITRE ATT&CK

### High-Signal Sysmon 15+ Telemetry
Ingest and prioritize critical event IDs mapped to MITRE ATT&CK techniques:

| Sysmon ID | Name | MITRE ATT&CK Mapping | Detection Logic / Indicator |
| :--- | :--- | :--- | :--- |
| **Event ID 1** | Process Creation | **T1059 / T1204** | Office/utility parent (`winword.exe`, `excel.exe`) spawning `cmd.exe` or `powershell.exe`. |
| **Event ID 3** | Network Connection | **T1071 / T1095** | Outbound non-standard connections from script hosts or PowerShell to external IPs. |
| **Event ID 7** | Image Loaded | **T1574.001** (DLL Side-Loading) | System processes (`lsass.exe`, `explorer.exe`) loading unsigned DLLs from `AppData\Local\Temp`. |
| **Event ID 10** | Process Access | **T1003.001** (Credential Dumping) | Handle access to `lsass.exe` with permissions `0x1010` or `0x1ffff` (Mimikatz signature). |
| **Event ID 22** | DNS Query | **T1071.004** (DNS Tunneling) | High-entropy DNS queries or subdomains exceeding 45 characters. |
| **Event ID 25** | Process Tampering | **T1055** (Process Hollowing) | External modification of process memory sections or image headers. |

### Automated Remediation, Scanner Orchestration & RustText Log Inspector
Integrate `windows event viewer` tools (`Invoke-McAfeeScanner.ps1`, `Manage-McAfeeAlerts.ps1`, `fix_event_viewer_issues.ps1`, and newly deployed **`Open-EventLogInRustText.ps1`**) into an automated response pipeline. Scheduled hourly and daily McAfee scans are actively executing (verified active through **November 23, 2026 02:31 AM** with continuous hourly `McAfeeScan_Hourly_*.log` and daily `McAfeeScan_Daily_*.log` telemetry), paired with Sysmon Event ID 10 alerts for unauthorized LSASS handle access and SHA-256 verified **`RustText v2.5.0`** (`Illson/RustText`, staged in `Popular Github Projects/agent-tools/rusttext/RustText.zip`) for high-speed large-file event log tailing, severity filtering, and JSON/JSONL validation:
```powershell
# Automated Sysmon & McAfee Alert Triage Pipeline
$Alerts = Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-Sysmon/Operational'; ID=1,3,10} -MaxEvents 50
foreach ($Event in $Alerts) {
    if ($Event.Id -eq 10 -and $Event.Message -match "lsass.exe") {
        Write-Warning "CRITICAL: Potential LSASS Dump attempt detected!"
        # Isolate offending process and invoke McAfee Quick Scan
        & ".\Invoke-McAfeeScanner.ps1" -ScanType Quick
    }
}
```

---

## 3. RHCSA Exam200: Modern RHEL 9.5/9.6 & RHEL 10 Lab Simulator

### RHEL 9.6 Kernel & Security Modernization
- **Modern Enterprise Toolchain**: RHEL 9.6 updates core developer compilers and runtimes to **GCC 14**, **LLVM 19**, and **Rust 1.84**, enabling modern language syntax, strict memory safety checks, and optimized native code compilation across user space.
- **Landlock LSM (Linux Security Module)**: RHEL 9.6 integrates the Landlock security module, allowing unprivileged processes and custom agent tools to self-restrict their filesystem and network access without requiring root privileges or custom SELinux policy compilations.
- **Unified Kernel Images (UKIs)**: Combines kernel, initrd, and UEFI stub into a single cryptographically signed PE binary, providing an unbroken hardware root-of-trust during Secure Boot.
- **Enterprise Network & Storage**: NetworkManager 1.52 with native IPsec IPv6 subnet-to-subnet peering and encrypted RPC over TLS for NFS filesystems.
- **Podman 5.4+ Multi-Architecture Builds**: Single-command multi-arch image compilation (`podman build --platform linux/amd64,linux/arm64`) with streamlined OCI layer generation.
- **RHEL 10 Image Mode (`bootc`), RHEL 10.3 & Post-Quantum Cryptography (PQC)**: Built on the Linux 6.12 kernel lineage (maturing through **RHEL 10.3** released Nov 10, 2026 with RHEL Lightspeed AI integration, **CVE-2026-98432** critical IPv4 TCP UAF emergency kernel patches, **NoisyTCP `CVE-2026-99288`** kernel hardening, and **Podman `RHSA-2026:93464`/`98554`** archive/Go fixes), **Image Mode for RHEL** builds, distributes, and updates the entire operating system (kernel through systemd) as an immutable OCI container image via `bootc`, eliminating configuration drift across bare-metal, VM, and cloud nodes. Native OpenSSL integration embeds NIST-approved quantum-resistant algorithms (**ML-KEM** key encapsulation and PQC signature suites) to mitigate "harvest now, decrypt later" attacks. Upstream mainline Linux has progressed to **Linux 7.4-rc** and Podman continues evolving into 6.x branches while Quadlets remain standard.
- **Container Supply Chain & CISA KEV Vulnerability Auditing**: In response to **CVE-2026-123158 ("SSHole")**, RHCSA environments enforce baseline image inspection. Podman and container builds utilizing `musl libc` (such as Alpine Linux) must verify OpenSSH is patched to 10.6p2+, ensure `PasswordAuthentication no` is explicitly set in `/etc/ssh/sshd_config`, or standardize on glibc/PAM-backed base images (e.g. `ubi9-minimal` / `ubi10-micro`).

### The Podman 5 Quadlets & Modern Networking Paradigm
Red Hat has deprecated `podman generate systemd` in favor of declarative **Podman Quadlets**. Modern RHCSA exam environments test Quadlet creation (`.container`, `.image`, `.volume`, `.network`, `.kube`, `.pod`, `.build`) for service persistence across reboots.

#### Podman 5 Core Networking: Pasta & Netavark
- **Default Rootless Networking (`pasta`)**: Podman 5 replaced legacy `slirp4netns` with **`pasta`** (from the `passt` tool suite). Pasta operates directly in the user namespace, providing near-native throughput, lower latency, and zero elevated privileges while eliminating complex port-forwarding overhead.
- **Netavark & Aardvark-DNS**: Netavark serves as the standard network backend, integrating seamlessly with `nftables` and delivering reliable container name resolution through `aardvark-dns`.
- **Quadlet Lifecycle Supervision**: Quadlets are translated into native `systemd` service units at boot/reload via Podman's internal generators. Stopping or reloading Quadlet `.network` or `.volume` units automatically handles cleanup when dependent containers terminate, letting PID 1 supervise containers with cgroup v2 resource limits without an intermediary daemon.

#### Rootless Quadlet Implementation (`~/.config/containers/systemd/web.container`):
```ini
[Unit]
Description=NGINX Microservice Container
After=network-online.target
Wants=network-online.target

[Container]
Image=docker.io/library/nginx:alpine
ContainerName=web-prod
PublishPort=8080:80
Volume=%h/public_html:/usr/share/nginx/html:Z
Network=app-net.network
AutoUpdate=registry

# Healthcheck integration
HealthCmd=curl -f http://localhost/ || exit 1
HealthInterval=30s
HealthRetries=3

[Service]
Restart=always
TimeoutStartSec=90

[Install]
WantedBy=default.target
```

#### Dedicated Network Quadlet (`~/.config/containers/systemd/app-net.network`):
```ini
[Unit]
Description=Isolated Microservice Bridge Network

[Network]
NetworkName=app-net
Driver=bridge
IPv6=false
```

#### Declarative Kubernetes Pod Quadlet (`~/.config/containers/systemd/pod.kube`):
```ini
[Unit]
Description=Multi-Container Web & Redis Pod
After=network-online.target

[Kube]
Yaml=microservice-pod.yaml
AutoUpdate=registry

[Install]
WantedBy=default.target
```

#### Key Exam Execution Commands:
```bash
# 1. Enable lingering so rootless services start at boot without active login
sudo loginctl enable-linger $USER

# 2. Reload systemd generator to parse new Quadlets
systemctl --user daemon-reload

# 3. Start and verify the generated systemd service
systemctl --user enable --now web.service
systemctl --user status web.service

# 4. Stream service logs directly via journald
journalctl --user -u web.service -f

# 5. Enable periodic registry auto-update timer
systemctl --user enable --now podman-auto-update.timer

# 6. Execute privileged operations via systemd v256+ run0 (SUID-free polkit execution)
run0 systemctl restart firewalld

# 7. Execute interactive debug shell inside running Podman container via run0
run0 --machine=web-prod /bin/sh

# 8. Encrypt and inject production secrets into Quadlets via systemd-creds
# Encrypt secret payload:
echo "super_secret_db_pass" | systemd-creds encrypt - web_db_pass.cred
# In web.container Quadlet [Service] block:
# SetCredentialEncrypted=db_password:%h/web_db_pass.cred
```

### Automated Self-Grading Lab Harness (`grade_rhcsa_lab.sh`)
Test and validate:
1. **LVM & Storage Persistence**: Validates `/etc/fstab` mounts via `UUID`, verifies thin provisioning, and checks LVM online resizing.
2. **SELinux & Firewall Posture**: Verifies permanent port allowances (`firewall-cmd --permanent --add-port`), service flags, and boolean configurations (`setsebool -P httpd_can_network_connect on`).
3. **ACLs & SGID Permissions**: Tests collaborative directory group rights (`chmod 2770`) and default access control lists (`setfacl -d -m g:wheel:rwx /shared`).

---

## 4. AWS Cloud Certification & Infrastructure as Code (IaC)

### CDK & Terraform Modular Blueprints
Supplement the Cloud Practitioner markdown study guides with production-grade Terraform modules:
- **Zero-Trust IAM Identity Center**: Declarative AWS SSO permission sets replacing hardcoded IAM users and access keys.
- **Service Control Policies (SCPs)**: Guardrail policies preventing region proliferation and enforcing mandatory KMS CMK encryption on EBS and S3.
- **GuardDuty & EventBridge Remediation**: EventBridge rule triggering an AWS Lambda function to automatically revoke exposed IAM credentials or quarantine compromised EC2 instances.

---

## 5. Reverse Engineering & Binary Analysis: REA & Ghidra 11.4 / 12.0

### The REA Architecture (`G:\My Drive\Antigravity\Projects\REA`)
The `REA` project serves as the centralized disassembler, decompiler, and binary inspection hub.

```mermaid
flowchart TD
    Binary[Target Executable / Game Asset] --> Triage[binary_inspector.py]
    Triage --> HeaderCheck{PE / Section Check}
    HeaderCheck -- Packed / High Entropy --> Unpack[x64dbg / OllyDbg Unpack Recipe]
    HeaderCheck -- Normal Entropy --> GhidraRun[ghidra_headless_runner.py]
    GhidraRun --> GhidraSuite[Ghidra 11.3 Headless Decompiler]
    GhidraSuite --> OutputC[Structured C Decompiled Source]
    GhidraSuite --> TargetMod[Modding / Target Integration: Ninja Gaiden, Tekken 8, Naraka]
```

### Ghidra 12.2 (`JDK 25+` Required) & Tooling Innovations
1. **PyGhidra (Official CPython 3 Integration)**:
   - **Ghidra 12.2 Baseline (Oct/Nov 2026)**: Upgrades minimum runtime from JDK 21 (Ghidra 12.1) to **JDK 25+** (Java Compact Object Headers, updated Jetty 12; ensure JDK 25 patches **CVE-2026-114938 Java4Shell** or guard x86-64 launches with `-XX:UseAVX=2`). Retains native Python 3 scripting via JPype (`./support/pyghidra`) with `numpy`, `capstone`, `pefile`, and `z3-solver`.
   - **`GhidrAssistMCP`, `morluto/rea` (`rea-agents-6.10.1`) & `erkamyaman/rust-anything` (`v2.1.0`/`v3.3.0`) Integration**: Native FastMCP server plugin inside Ghidra exposing functions, decompiled pseudocode, data types, and cross-references over SSE/HTTP directly to AI agents (build with `./gradlew` against `JAVA_HOME` JDK 25 and `GHIDRA_INSTALL_DIR`); pair with GitHub's #1 trending **`morluto/rea`** (`npx rea-agents setup`, 473.6k stars in `Popular Github Projects/reports/2026-11-22.md`) for clean-room JS/Electron/.NET/website and Ghidra-backed native binary reverse engineering, plus newly integrated **`REA/tools/Invoke-RustAnythingAudit.ps1`** (SHA-256 verified `rust-anything v2.1.0` staged in `agent-tools/rust-anything/`, `v3.3.0` upstream + `EL4CTEO/fast-anything v0.6.1`) for incremental behavioral trace verification (`record -> bridge -> diff -> lift`) and clean-room Rust porting alongside Xbox Series static recompilation research (**`ItsNotRexed/Leonida`**, **`R0Y00/Xbox2Windows`**, **`omonkeyz/xbox-emulator`**).
   - Includes both an interactive GUI CPython plugin and the `./support/pyghidra` CLI wrapper for automated headless analysis.
2. **JIT-Accelerated P-Code Emulator (`JitPcodeEmulator`)**:
   - Standard P-code interpretation is slow during heavy unpacking, deobfuscation, and crypto loops.
   - `JitPcodeEmulator` acts as a drop-in replacement for the standard `PcodeEmulator` (`new JitPcodeEmulator(...)`), dynamically compiling P-code blocks directly into JVM bytecode at runtime.
   - Delivers a **3×–5× execution speedup**, making dynamic unpacking and emulation feasible within headless CI/CD analysis pipelines:
```python
# Headless JIT-Accelerated String Decryption via PyGhidra
import pyghidra

with pyghidra.open_program("target_binary.exe") as flat_api:
    program = flat_api.getCurrentProgram()
    from ghidra.pcode.emu.jit import JitPcodeEmulator

    # Initialize JIT-accelerated P-code emulator (compiles P-code blocks to JVM bytecode)
    emu = JitPcodeEmulator(program)
    
    # Target decryption subroutine address
    decrypt_addr = program.getAddressFactory().getAddress("00401500")
    print(f"[REA] Initialized JIT P-Code Emulator for routine at {decrypt_addr}")
    # Execute JIT bytecode emulation passage to dump decrypted payloads
```
3. **Visual Studio Code Integration**:
   - Native Ghidra 11.3 actions (`Tools -> Create VSCode Module Project...` and `Edit Script with Visual Studio Code`) provide full IntelliSense and interactive debugging for Ghidra extensions.
4. **Game Target Feasibility & Anti-Cheat Boundaries**:
   - **Ninja Gaiden 2**: Xenon PowerPC decompilation via Ghidra-XEX loader; PC Sigma 2 `.dat` asset unpacking. Fully offline modding.
   - **Tekken 8**: Unreal Engine 5 IoStore asset extraction via FModel and `~mods` packaging; REFramework offline hooks. (Strict online multiplayer safety boundary).
   - **Naraka: Bladepoint**: Unity IL2CPP offline asset inspection via AssetStudio/UABEA. Strictly no tampering with live memory or EAC/NeacProtect anti-cheat systems.

---

## 6. Spam Block & Privacy Engineering: Automated OSINT Reduction & Data Broker Suppression

### Threat Model & OSINT Reduction Architecture (`spam block`)
Commercial data brokers (Whitepages, Spokeo, Radaris, LexisNexis, BeenVerified) aggregate consumer PII (full legal names, mobile phone numbers, residential addresses, relative trees) scraped from public records and marketing lists. This creates severe attack surface exposure for spear-phishing, credential stuffing, SIM swapping, and social engineering.

```mermaid
flowchart TD
    UserPII[Encrypted PII Profile: Email, Phone, Address] --> Engine[optout_engine.py]
    Engine --> DB[(data_brokers.json - 15+ Top Brokers)]
    Engine --> LegalGen[Statutory Request Generator: CCPA/CPRA + Texas TDPSA]
    LegalGen --> Mailto[Direct Pre-Composed Mailto Removal Envelopes]
    LegalGen --> PlaywrightRunner[Headless Playwright Form Automation Runner]
    PlaywrightRunner --> BrokerPortals[Broker Opt-Out Web Endpoints]
    BrokerPortals --> StatusTracker[optout_tracker.json: Pending / Sent / Suppressed]
    Engine --> FilterGen[gmail_filter_rules.py]
    GmailXML --> GmailImport[Gmail Native Auto-Trash Rules]
    GmailImport --> EmailOrganizerSync[email organizer Pipeline Telemetry]
```

### Automated Headless Opt-Out Runner (Playwright & Privotron Pattern)
While paid services (DeleteMe, Incogni, Kanary) require transmitting personal identifiers to third-party cloud databases, `spam block` executes 100% locally on the user's workstation.
- **Automated Web-Form Automation**:
Upgrade `optout_engine.py` to support headless Playwright script execution based on the open-source `kevinl95/privotron` architecture and `yaelwrites/Big-Ass-Data-Broker-Opt-Out-List`:
```python
# /// script
# requires-python = ">=3.12"
# dependencies = [
#     "playwright>=1.48.0",
#     "pydantic>=2.8",
# ]
# ///

import asyncio
from playwright.async_api import async_playwright

async def automate_optout_submission(broker_url: str, email: str, phone: str, name: str):
    """Execute headless form submission against data broker opt-out portal."""
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=True)
        context = await browser.new_context(user_agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/130.0.0.0")
        page = await context.new_page()
        await page.goto(broker_url, wait_until="networkidle")
        
        # Match standard input selectors for name, email, phone
        if await page.locator("input[type='email'], input[name*='email']").count() > 0:
            await page.locator("input[type='email'], input[name*='email']").first.fill(email)
        if await page.locator("input[name*='phone'], input[id*='phone']").count() > 0:
            await page.locator("input[name*='phone'], input[id*='phone']").first.fill(phone)
        if await page.locator("input[name*='name'], input[id*='name']").count() > 0:
            await page.locator("input[name*='name'], input[id*='name']").first.fill(name)
            
        await page.screenshot(path=f"_snapshots/optout_{broker_url.split('/')[2]}.png")
        await browser.close()
```

### Statutory Legal Framework & Multi-State Compliance
The engine crafts legally binding deletion requests citing active state and federal statutes:
1. **California Consumer Privacy Act (CCPA / CPRA, Cal. Civ. Code § 1798.100 et seq.)**:
   - Mandates full deletion of consumer PII and cessation of data sales within a strict statutory 45-day window.
2. **California DELETE Act (SB 362 / DROP Platform)**:
   - Establishes centralized deletion across all registered brokers maintained by the California Privacy Protection Agency (CPPA).
3. **Texas Data Privacy and Security Act (TDPSA) & Texas HB 2802**:
   - Texas Business and Commerce Code Chapter 509 mandates registration of commercial data brokers operating in Texas and grants consumers enforceable opt-out rights against the sale or profiling of personal data.

### Gmail Shield & Dynamic XML Filter Pipeline
- **Importable `gmail_spam_filters.xml`**: Automatically exports multi-criteria XML filter rules applying `shouldTrash=true` and `shouldNeverSpam=false` to:
  - High-spam Top-Level Domains (`.top`, `.click`, `.xyz`, `.club`, `.work`, `.rest`, `.cam`).
  - Predatory sweepstakes and scam bait patterns (`wire transfer confirmation`, `crypto prize won`, `urgent parcel delivery fee`, `beneficiary funds`).
  - Relentless political marketing blasts.
- **Cross-Project Synergy with `email organizer`**:
  - When `email organizer` identifies recurring unsolicited bulk marketing senders during daily triage, it automatically updates `spam block/data_brokers.json` and pushes new filter criteria into the active Gmail shield.

---

## 7. Scripting Practice, Enterprise Systems Engineering & Automated Verification Suite (`Scripting`)

### Architectural Blueprint (`G:\My Drive\Antigravity\Projects\Scripting`)
The `Scripting` project provides a comprehensive, production-grade training, automation, and verification environment for **Red Hat Enterprise Linux (RHEL 9.5 & RHEL 10)** and **Modern PowerShell (5.1 & 7+)**. It features 14 hands-on labs, automated test harnesses (`Test-Runner.ps1`, `test.sh`), an interactive browser-based portal (`webpage/index.html`), and a dedicated Antigravity plugin (`plugin/script-practice`) powered by the `script-coach` AI mentor.

```mermaid
flowchart TD
    UserReq[Engineering Practice & Automation Task] --> Coach[script-coach Expert Agent]
    Coach --> RHELLabs[Red Hat Enterprise Linux Track: 7 Labs]
    Coach --> PSLabs[Modern PowerShell Track: 7 Labs]
    RHELLabs --> BashStandards[Defensive Bash: set -euo pipefail, run0, Quadlets, SELinux]
    PSLabs --> PSStandards[Pipeline Objects: CmdletBinding, PSCustomObject, Pester 5.5+]
    BashStandards --> RHELTest[test.sh Harness Execution]
    PSStandards --> PSTest[Test-Runner.ps1 Harness Execution]
    RHELTest & PSTest --> WebPortal[Interactive Lab Webpage: webpage/index.html]
    WebPortal --> DeployTelemetry[Deploy Suite & Health Status Badges]
```

### Production Red Hat Enterprise Linux / Bash Guidelines (RHEL 9.5 & 10)
1. **Strict Error Handling & Delimiter Hygiene**:
   - Every script enforces `set -euo pipefail` at entry to ensure instantaneous failure upon unhandled errors, unbound variables, or broken pipes.
   - Set `IFS=$'\n\t'` when iterating line-separated streams to prevent whitespace tokenization errors.
2. **Defensive Variable Quoting & Parameter Expansions**:
   - Double-quote all variables and command substitutions: `"${VAR}"`, `"$(command)"`.
   - Provide default fallback expansions: `"${1:-default_value}"`.
   - Use Bash built-in compound testing `[[ ... ]]` over POSIX `[ ... ]`.
3. **Deterministic Resource Lifecycle**:
   - Never leave temporary artifacts in `/tmp` without bound handlers. Allocate via `mktemp -d` and bind automatic cleanup:
   ```bash
   SCRATCH_DIR="$(mktemp -d)"
   cleanup() {
       rm -rf "${SCRATCH_DIR}"
   }
   trap cleanup EXIT INT TERM
   ```
4. **Modern RHEL 10 & systemd v256+ Alignment**:
   - **`run0` Privilege Management**: Transition from legacy `setuid` sudo to systemd `run0`, which allocates isolated, transient execution units under PID 1 governed by polkit rules.
   - **Service Auditing**: Query unit status with `systemctl is-active --quiet <svc>` and inspect failures with `journalctl -u <svc> -n 50 --no-pager`.
   - **Firewalld Rich Rules**: Enforce permanent granular restrictions: `firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" port port="8080" protocol="tcp" accept' && firewall-cmd --reload`.
   - **SELinux Enforced Contexts**: Always execute `restorecon -R` when provisioning services, container volume binds (`:Z`), or web root assets. Validate sudoers drop-in configuration using `visudo -cf <file>`.

### Modern PowerShell Guidelines (PowerShell 5.1 & 7+)
1. **Cmdlet Architecture & Approved Verbs**:
   - Enforce standard `Verb-Noun` format utilizing Microsoft Approved Verbs (`Get`, `Set`, `New`, `Invoke`, `Test`, `Start`, `Stop`).
   - Decorate functions with `[CmdletBinding(SupportsShouldProcess)]` to support `-WhatIf` and `-Confirm`.
2. **High-Throughput Pipeline Processing**:
   - Implement `begin {}`, `process {}`, and `end {}` blocks whenever handling pipeline input:
   ```powershell
   function Get-ServiceHealthAudit {
       [CmdletBinding(SupportsShouldProcess)]
       param(
           [Parameter(ValueFromPipeline, ValueFromPipelineByPropertyName)]
           [ValidateNotNullOrEmpty()]
           [string[]]$ComputerName = @($env:COMPUTERNAME)
       )
       begin {
           $ErrorActionPreference = 'Stop'
       }
       process {
           foreach ($Node in $ComputerName) {
               try {
                   $Services = Get-CimInstance -ClassName Win32_Service -Filter "StartMode = 'Auto' AND State != 'Running'" -ComputerName $Node
                   foreach ($Svc in $Services) {
                       [PSCustomObject]@{
                           ComputerName = $Node
                           ServiceName  = $Svc.Name
                           DisplayName  = $Svc.DisplayName
                           State        = $Svc.State
                           StartMode    = $Svc.StartMode
                       }
                   }
               }
               catch [System.Runtime.InteropServices.COMException] {
                   Write-Error "CIM connection failed for $Node: $_"
               }
           }
       }
       end {}
   }
   ```
3. **Object Streaming Over Strings**:
   - Emit strongly-typed `[PSCustomObject]` instances.
   - **Zero Presentation Cmdlets**: Never call `Format-Table` or `Format-List` inside functions or reusable modules. Formatting belongs exclusively to the end-user presentation layer.
4. **Robust Exception Handling**:
   - Enforce `$ErrorActionPreference = 'Stop'` across automation routines.
   - Catch specific .NET exceptions (`[System.IO.FileNotFoundException]`, `[System.Net.Http.HttpRequestException]`) before fallback general catches.
   - Release handles and network sessions cleanly in `finally {}` blocks.
5. **Cross-Version Compatibility**:
   - Avoid PowerShell 7-only null-coalescing operators (`??`) in shared scripts; prefer `if ($null -ne $var) { ... } else { ... }`.
   - Wrap potential scalar outputs in array subexpressions `@($result).Count` when checking counts in PowerShell 5.1.
   - Avoid aliases (`dir`, `ls`, `select`, `where`, `gc`); use full cmdlet names.
6. **Pester 5.5+ Automated Unit Testing**:
   - Validate functions using modern Pester syntax (`Describe`, `Context`, `It`, `Should -Be`, `InModuleScope`).

### Interactive Lab Curriculum (14 Labs)
- **Red Hat Enterprise Linux Labs (`redhat-linux/labs/`)**:
  - `01-user-automation`: Automated user onboarding with secondary groups and password expiration.
  - `02-systemd-timer`: Custom microservice unit with scheduled monotonic systemd timers.
  - `03-backup-rotator`: Tar-gzip rotation with MD5/SHA-256 integrity verification and prune retention.
  - `04-lvm-storage-monitor`: Dynamic LVM volume group free-space alerting and thin-pool tracking.
  - `05-firewalld-network-manager`: Permanent rich-rule deployment, port forwards, and IP whitelisting.
  - `06-selinux-user-hardening`: Confined SELinux user mappings (`staff_u`), boolean adjustments, and context restoration.
  - `07-performance-tuned-monitor`: Tuned profile switching (`throughput-performance`), dirty ratio tuning, and sysctl verification.
- **Modern PowerShell Labs (`powershell/labs/`)**:
  - `01-advanced-functions-pipeline`: Production pipeline streaming with `begin/process/end` and `SupportsShouldProcess`.
  - `02-object-pipeline-filtering`: Grouping, calculated properties, and `[PSCustomObject]` emission.
  - `03-robust-error-handling`: Specific .NET exception catches and clean resource release.
  - `04-cim-wmi-service-auditor`: WQL querying, hardware inventory sweeps, and remote CIM sessions.
  - `05-active-directory-user-sync`: CSV ingestion, employee onboarding, OU assignment, and account security.
  - `06-rest-api-webhooks`: `Invoke-RestMethod` HTTP JSON payload construction with retry loops and bearer tokens.
  - `07-module-pester-testing`: Manifest creation (`.psd1`), root module export (`.psm1`), and Pester 5.5+ test suite.

### Cross-Portfolio Synergy
- **With `RHCSA Exam200`**: Linux labs provide automated verification harnesses for practicing RHCSA performance objectives.
- **With `windows event viewer`**: PowerShell CIM and service monitoring modules feed directly into Sysmon threat hunting scripts.
- **With `automate my day`**: Morning execution audits run `Test-Runner.ps1` to report script health and syntax compliance in daily logs.
- **With `My Custom Gui` & `Github Portfolio`**: The interactive lab portal (`webpage/index.html`) is linked into the Nexus Hub and showcased as a premier systems engineering project.

---

## 8. Red Hat OpenShift Enterprise Platform & EX280 Certification Suite (`openshift`)

### Architectural Scope (`G:\My Drive\Antigravity\Projects\openshift`)
The `openshift` repository is an offline-capable, interactive platform engineering and certification academy designed to take operators from container fundamentals to **Red Hat Certified OpenShift Administrator (EX280)** and Enterprise Platform Engineer. It aligns directly with the official Red Hat curriculum:
- **DO180**: Red Hat OpenShift I: Containers & Kubernetes (OCI specifications, Podman, Buildah, Skopeo).
- **DO280**: Red Hat OpenShift Administration II: Operating a Production Kubernetes Cluster (Core EX280 competencies).
- **DO380**: Red Hat OpenShift Administration III: Scaling Deployments in the Enterprise (GitOps, Pipelines, Operators).

### OpenShift & Kubernetes Version Mapping (2026 Production Standards)
- **OpenShift 4.17 (Kubernetes 1.30)**: Complete removal of legacy *OpenShift SDN*. All clusters must run strictly on **OVN-Kubernetes**. Enforces updated TLS 1.3/ECDHE cipher suites and `restricted-v2` SCC defaults.
- **OpenShift 4.18 (Kubernetes 1.31 - EUS)**: Even-numbered Extended Update Support (EUS) release.
  - **User Defined Networks (UDNs) Reach GA**: Empowers administrators to build custom Layer-2 and Layer-3 network segments on the default OVN-Kubernetes stack for enhanced multi-tenant network isolation across pods and OpenShift Virtualization VMs.
  - **Secrets Store CSI Driver Operator (GA)**: Workloads securely fetch secrets directly from external vault systems (HashiCorp Vault, AWS Secrets Manager) without persisting plaintext secrets natively in etcd.
  - **`cert-manager` v1.15 Operator & `istio-csr`**: Centralized, automated TLS certificate lifecycle management across Ingress controllers, API servers, and service mesh sidecars.
- **OpenShift 4.19 (Kubernetes 1.32)**:
  - **Unified Console Experience**: Merges the traditional Administrator and Developer perspectives into a single cohesive default interface for streamlined topology and workload management.
  - **BGP Route Advertisements for CUDNs**: Native Border Gateway Protocol (BGP) route advertisements for ClusterUserDefinedNetworks (CUDNs), dynamically learning and advertising routes to pods/services on provider networks without NAT overhead.
  - **Network Observability Operator Integration**: Native support for tracking, filtering, and flow-processing across multi-tenant User-Defined Networks (UDNs) directly in the console.
  - **Complete Deprecation & Removal of cgroups v1**: OpenShift 4.19 completely removes support for `cgroup v1` on all new installations, enforcing strict **cgroup v2** cluster-wide. Pre-upgrade validation of `node.config/cluster` and JVM container memory thresholds is required.
  - **ServiceAccountTokenNodeBinding Enabled by Default**: Aligns with upstream Kubernetes 1.32 to bind service account tokens directly to node objects, mitigating token replay attacks across disjoint nodes.
  - **Container Supply Chain & KEV Defense (CVE-2026-123158 "SSHole")**: Automated cluster-wide admission checks via OpenShift Kyverno / OPA Gatekeeper auditing deployed Alpine/musl-based container pods to ensure OpenSSH 10.6p2+ compliance or disabling of password authentication.
  - **Cloud-Native Tooling Updates**: OpenShift Service Mesh 3.1 (Istio 1.26 + Kiali 2.11), OpenShift GitOps (Argo CD & Argo Rollouts), OpenShift Serverless 1.36 (Knative 1.16).
  - **Multi-Part OCI/GCS Upload**: Native support for large OCI artifacts and model weight distribution without HTTP buffer timeouts.
- **OpenShift 4.20 (EUS — Kubernetes 1.33 & CRI-O 1.33)**:
  - **Post-Quantum Cryptography (PQC) Control-Plane TLS**: Introduces `X25519MLKEM768` hybrid key exchange (via Go 1.24) securing internal TLS communication across API server, kubelet, and scheduler channels against "harvest now, decrypt later" threats.
  - **OVN-Kubernetes Native BGP (`FRR-K8s`) & EVPN Support**: Integrates FRRouting 10+ via `FRRConfiguration` CRDs in `openshift-frr-k8s`, enabling Ethernet VPN (EVPN) extensions for Primary Cluster User-Defined Networks (`P-CUDNs`) with both **MAC-VRF** (L2 stretching for VM live migration) and **IP-VRF** (L3 tenant routing) over single VXLAN encapsulation (eliminating Geneve-in-VXLAN double encapsulation).
  - **GA Kubernetes Gateway API & AI Orchestration**: Native Ingress Operator lifecycle support for `GatewayClass`, `Gateway`, `HTTPRoute`, `GRPCRoute`, and `ReferenceGrant` (`gateway.networking.k8s.io/v1`), native Sidecar containers GA (`initContainers` with `restartPolicy: Always`), and `LeaderWorkerSet` GA + Gateway API Inference Extension for distributed AI serving.
- **OpenShift 4.21 / 4.22 (Kubernetes 1.34+ & CRI-O 1.34+)**:
  - **Dynamic Resource Allocation (DRA) GA**: Replaces rigid count-based device plugins (`nvidia.com/gpu: 1`) with CEL expression-driven GPU scheduling (matching exact VRAM thresholds $\ge 40\text{GB}$, compute capability, and NVLink/NUMA topology).
  - **Converged AI/ML & Virtualization Fabric**: Native **Kueue** queueing, **JobSet Operator** enhancements for distributed multi-node AI training, and unified VM + container orchestration.
  - **Nov 2026 Kernel, Operator, CRI-O & CSI Node Errata**: Apply `ose-rhel-coreos` (`RHSA-2026:95408` / `RHSB-2026-016`) remediating **CVE-2026-98432** (CVSS 9.8 Linux kernel IPv4 TCP UAF, actively tracked on OpenShift 4.22 RHCOS nodes), **CRI-O `bind_mount_prefix` intermediate symlink bypass (`CVE-2026-76061`)**, **`sssd` null-pointer dereference (`CVE-2026-127101`)**, OpenShift Sandboxed Containers `systemd-gpt-auto-generator` confidential peer-pod swap/partition leakage hardening, **`brace-expansion` (`CVE-2026-14257` / `69152`)** & Go HTTP/2 (**`CVE-2026-33814`**) operator patches, and CSI driver advisory **CVE-2026-85781**; verify NGINX Ingress/sidecar HTTP/2 builds against **CVE-2026-123007 / 123633**.

```mermaid
flowchart TD
    Admin[OpenShift Administrator / Platform Engineer] --> CLI[oc CLI & Web Console]
    CLI --> Tenancy[Multitenancy & Projects: ProjectRequest, Quotas, Limits]
    CLI --> Security[Security & Access: RBAC, ServiceAccounts, SCC restricted-v2]
    CLI --> Network[Ingress & Routing: Edge, Passthrough, Re-encrypt, OVN-K8s]
    CLI --> Storage[Storage Management: PVC, StorageClasses, Dynamic CephFS/EBS]
    CLI --> Ops[Operators & Diagnostics: OLM, must-gather, ovn-trace, crictl]
    Ops --> Verification[Automated Lab Tests: deploy-hello-world.ps1, diagnose-route.ps1]
    Verification --> MockExam[EX280 Performance Mock Exam: 2.5-hour Timed Drill]
```

### Core EX280 Competencies & Declarative Manifests

#### 1. Projects, Resource Quotas & Multitenancy
OpenShift enforces strict tenant boundary separation via `Project` objects (wrappers over Kubernetes namespaces with security annotations):
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-alpha-quota
  namespace: team-alpha
spec:
  hard:
    requests.cpu: "4"
    requests.memory: 8Gi
    limits.cpu: "8"
    limits.memory: 16Gi
    pods: "10"
    services: "5"
---
apiVersion: v1
kind: LimitRange
metadata:
  name: team-alpha-limits
  namespace: team-alpha
spec:
  limits:
  - type: Container
    default:
      cpu: 500m
      memory: 512Mi
    defaultRequest:
      cpu: 200m
      memory: 256Mi
    max:
      cpu: "2"
      memory: 4Gi
    min:
      cpu: 50m
      memory: 64Mi
```

#### 2. Role-Based Access Control (RBAC) & Service Accounts
Scoped permissions ensure the principle of least privilege:
```bash
# Create dedicated service account for microservice deployment
oc create sa pipeline-deployer -n team-alpha

# Grant edit role within specific project namespace
oc policy add-role-to-user edit -z pipeline-deployer -n team-alpha

# Verify permissions via user impersonation
oc auth can-i create deployments --as=system:serviceaccount:team-alpha:pipeline-deployer -n team-alpha
```

#### 3. Security Context Constraints (SCC) vs Pod Security Standards (PSS)
OpenShift utilizes SCCs to control pod capabilities (UID allocation, SELinux, host ports, privileged mode). In OpenShift 4.16+, workloads adhere to `restricted-v2`:
- Default UIDs are dynamically assigned from the namespace's allocated UID range (`openshift.io/sa.scc.uid-range`).
- Never grant `privileged` or `anyuid` SCC cluster-wide; scope custom SCCs or bind to dedicated ServiceAccounts:
```bash
# Add non-root custom capability safely to specific service account
oc adm policy add-scc-to-user nonroot-v2 -z backend-sa -n production
```

#### 4. Ingress Routing & TLS Profiles
OpenShift Ingress provides built-in HAProxy routing supporting three distinct TLS termination modes:
1. **Edge Termination**: TLS is terminated at the Ingress router; traffic to pod is plaintext HTTP.
2. **Passthrough Termination**: Encrypted TLS traffic passes untouched directly through the router to the pod (zero-trust end-to-end TLS).
3. **Re-encrypt Termination**: Router terminates external TLS and re-encrypts traffic to the backend pod using the internal destination CA certificate.

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: secure-api-route
  namespace: production
spec:
  host: api.apps.cluster.example.com
  to:
    kind: Service
    name: api-service
    weight: 100
  port:
    targetPort: 8443
  tls:
    termination: reencrypt
    certificate: |-
      -----BEGIN CERTIFICATE-----
      ... (External TLS Cert) ...
      -----END CERTIFICATE-----
    key: |-
      -----BEGIN PRIVATE KEY-----
      ... (External Private Key) ...
      -----END PRIVATE KEY-----
    destinationCACertificate: |-
      -----BEGIN CERTIFICATE-----
      ... (Service Mesh / Backend Pod CA) ...
      -----END CERTIFICATE-----
```

#### 5. Persistent Storage & Dynamic Provisioning
Dynamic PVC allocation utilizing modern CSI drivers:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: database-storage-pvc
  namespace: production
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 50Gi
  storageClassName: gp3-csi
```

#### 6. User-Defined Networks (UDNs) & BGP Route Advertisements (OpenShift 4.18 / 4.19)
OpenShift 4.18 and 4.19 introduce declarative multi-tenant network fabric routing without SNAT or NodePort overhead. By pairing OVN-Kubernetes with the native Free Range Routing (FRR) provider, pod and VM subnets on `ClusterUserDefinedNetwork` (CUDN) resources are advertised directly to top-of-rack data center routers via Border Gateway Protocol (BGP).

##### Step 1: Enable FRR Routing Provider and Route Advertisements
```bash
oc patch Network.operator.openshift.io cluster --type=merge -p='{
  "spec": {
    "additionalRoutingCapabilities": {
      "providers": ["FRR"]
    },
    "defaultNetwork": {
      "ovnKubernetesConfig": {
        "routeAdvertisements": "Enabled"
      }
    }
  }
}'
```

##### Step 2: Declare ClusterUserDefinedNetwork (CUDN)
```yaml
apiVersion: k8s.ovn.org/v1
kind: ClusterUserDefinedNetwork
metadata:
  name: enterprise-workload-udn
  labels:
    advertise: "true"
spec:
  network:
    layer2:
      role: Primary
      subnets:
        - 10.120.0.0/16
```

##### Step 3: Configure BGP Route Advertisements Custom Resource
```yaml
apiVersion: k8s.ovn.org/v1
kind: RouteAdvertisements
metadata:
  name: enterprise-bgp-advertisements
spec:
  nodeSelector: {}
  frrConfigurationSelector: {}
  networkSelectors:
    - networkSelectionType: ClusterUserDefinedNetworks
      clusterUserDefinedNetworkSelector:
        networkSelector:
          matchLabels:
            advertise: "true"
      advertisements:
        - "PodNetwork"
```

#### 7. High-Availability Diagnostics & Troubleshooting Runbook
Performance-based exams test rapid triage under pressure:
- **Cluster Diagnostics**: Run `oc adm must-gather` to dump complete etcd, network, and node state for post-mortem analysis.
- **Node-Level Debugging**:
  ```bash
  oc debug node/<node-name>
  # Within debug shell:
  chroot /host
  crictl ps
  crictl logs <container-id>
  systemctl status kubelet
  journalctl -u crio -n 50 --no-pager
  ```
- **Network Tracing (OVN-Kubernetes)**:
  ```bash
  # Trace packet flows through OVS flow tables
  ovn-trace --ct=new <logical-switch> 'inport == "pod-port" && eth.src == ...'
  ```

#### 8. OpenShift 4.19 Platform Architecture & Kubernetes 1.32 Foundation
OpenShift 4.19 is engineered upon **Kubernetes 1.32** and **CRI-O 1.32** running on **RHEL 9.6 RHCOS**, delivering critical enterprise cloud advances:
1. **Complete Transition to Strict cgroups v2**: OpenShift 4.19 permanently discontinues support for `cgroups v1` across all new cluster installations and upgrades, standardizing strictly on Linux kernel cgroups v2 for fine-grained memory pressure stall information (PSI) and container resource limits.
2. **Kubernetes Gateway API (Generally Available)**: Supported natively via **OpenShift Service Mesh 3** (Istio 1.26 + Envoy), the Gateway API (`gateway.networking.k8s.io/v1`) becomes a premier, highly flexible ingress paradigm for advanced L4/L7 traffic routing, weighted traffic splitting (canary rollouts), and unified TLS management managed directly by the Ingress Operator.
3. **Unified Console Experience**: The OpenShift web console merges the traditional Admin and Developer views into a single, unified interface, streamlining navigation across topology mapping, workloads, and cluster resources.
4. **Cert-Manager Router Integration**: Direct secret loading into the router, simplifying TLS certificate lifecycle management and ingress renewal automation.
5. **Air-Gapped Supply-Chain Verification (`oc-mirror` v2)**: Enhances disconnected registry management with native support for Cosign tag-based SigStore signatures for verifying container provenance in isolated environments.

#### 9. ClusterUserDefinedNetworks (CUDNs) & BGP Route Advertisements (OpenShift 4.18/4.19 GA)
OpenShift 4.18 (EUS) and 4.19 deliver native Layer 3 routing via BGP Route Advertisements, allowing pods and OpenShift Virtualization VMs attached to User-Defined Networks to advertise routes directly to physical network routers via `frr-k8s` (Free Range Routing), eliminating traditional NAT and hairpin bottlenecks.

```bash
# 1. Enable RouteAdvertisements feature & configure FRR provider in Cluster Network Operator (CNO)
oc patch Network.operator.openshift.io cluster --type=merge \
  -p='{"spec":{"additionalRoutingCapabilities":{"providers":["FRR"]},"defaultNetwork":{"ovnKubernetesConfig":{"routeAdvertisements":"Enabled"}}}}'
```

##### Declarative ClusterUserDefinedNetwork (`cudn-tenant-l2.yaml`):
```yaml
apiVersion: k8s.ovn.org/v1
kind: ClusterUserDefinedNetwork
metadata:
  name: tenant-enterprise-net
spec:
  network:
    topology: Layer2
    layer2:
      role: Primary
      subnets:
        - "10.200.0.0/16"
      ipam:
        lifecycle: Persistent
```

##### Native BGP Route Advertisements Custom Resource (`route-advertisements.yaml`):
```yaml
apiVersion: k8s.ovn.org/v1
kind: RouteAdvertisements
metadata:
  name: bgp-cudn-advertisements
spec:
  nodeSelector:
    matchLabels:
      node-role.kubernetes.io/worker: ""
  networkSelector:
    matchLabels:
      k8s.ovn.org/network: tenant-enterprise-net
  targetVRF: default
  frrConfiguration:
    bgp:
      as: 65001
      neighbors:
        - ip: 10.10.10.1
          as: 65000
          password: "SecretBgpKey2026"
```

### Lab Automation & Verification Scripts
The repository provides automated PowerShell validation routines:
- `00-getting-started/check-binary.ps1`: Verifies `oc` and `podman` binary PATH availability and cluster login token validity.
- `labs/deploy-hello-world.ps1`: Deploys sample multi-container pods, ClusterIP services, and edge routes.
- `labs/diagnose-route.ps1`: Validates DNS resolution, TLS certificate handshakes, and HTTP 200 response codes from exposed endpoints.
- `04-mock-exams-and-drills/01-ex280-mock-exam.md`: 12 comprehensive challenge tasks simulating the 2.5-hour official Red Hat EX280 practical exam.

### Cross-Portfolio Synergy
- **With `RHCSA Exam200`**: Transitions Linux system administrator skills from single-host systemd/Podman management to distributed cluster orchestration.
- **With `Scripting`**: Leverages Bash and Modern PowerShell pipeline standards to automate cluster deployment and health sweeps.
- **With `vulnerability management` & `MY Security`**: Continuously checks cluster images against Cisco PSIRT, CSAF, and CVE feeds before admitting workloads.
- **With `My Custom Gui` & `Github Portfolio`**: Displays OpenShift certification progress and active cluster health status badges across developer showcase dashboards.

---

## 9. Aegis-AI Defense Matrix: Autonomous Agent Zero-Trust Sandboxing & Containment Architecture (`ai defense`)

### Threat Model & Defense-in-Depth Architecture (`G:\My Drive\Antigravity\Projects\ai defense`)
The **`ai defense`** platform establishes an enterprise zero-trust containment architecture, live attack laboratory, and web operational console built to prevent autonomous AI agents and language models from escaping sandboxed environments, exploiting Linux kernel vulnerabilities, and moving laterally across corporate subnets.

```mermaid
flowchart TD
    UntrustedData[Untrusted Ingestion / Adversarial Prompt Injection] --> Layer1[Layer 1: Deterministic AST & Strict Schema Barrier]
    Layer1 --> Layer2[Layer 2: MicroVM Hard Isolation - gVisor runsc / Firecracker]
    Layer2 --> Layer3[Layer 3: Zero-Trust Ephemeral Egress & FQDN DNS Enclave]
    Layer3 --> Layer4[Layer 4: Real-Time In-Kernel Telemetry & eBPF Tetragon]
    Layer4 --> Layer5[Layer 5: Capability Governors, 120s TTL & Emergency Killswitch]
    Layer5 --> ExecutionZone[Contained Sandbox Execution or Instant SIGKILL]
```

### The 6 Critical AI Escape Vectors & Active Mitigations
1. **Kernel Exploits & Shared-Host Namespace Breakouts**:
   - Standard Docker/LXC containers share the host Linux kernel directly via namespaces and cgroups. Untrusted code exploiting kernel bugs (e.g. `dirty COW`, `io_uring` race conditions, unmasked `/proc` and `/sys` mounts) can break out to root on the physical host.
   - *Mitigation*: **gVisor (`runsc`)** user-space virtual kernel or **Firecracker MicroVMs**. All syscalls terminate in user space without touching host ring-0.
2. **Indirect Prompt Injection & Tool Weaponization**:
   - Unvetted instructions embedded in scraped HTML, customer emails, or PDFs hijacking agent tool loops.
   - *Mitigation*: Deterministic AST schema validation. Eliminate arbitrary raw shell tools; parameterize tool calls through strictly-typed Pydantic schemas with path bounds checking.
3. **Covert Side-Channels & DNS Egress Tunneling**:
   - Escaping agents encoding credentials into DNS query labels (`exfil.<base64>.attacker-c2.net`).
   - *Mitigation*: Default-deny egress; isolate agents in dedicated network namespaces routed exclusively through an egress inspection proxy that drops high-entropy subdomains.
4. **Recursive Subagent Spawning & Resource Starvation (Fork Bombs)**:
   - Runaway agent spawning consuming CPU/GPU compute, exhausting API quotas, and persisting as background daemons.
   - *Mitigation*: Hard recursion depth cap $= 1$, 120-second execution TTL ceilings, and cgroups v2 `PIDsLimit=64` with strict memory bounding.
5. **Model Context Protocol (MCP) Server Pivoting**:
   - Using read-only filesystem MCP access to pivot into sibling terminal execution tools across unrestricted JSON-RPC sockets.
   - *Mitigation*: Loopback binding only (`127.0.0.1`), ephemeral HMAC-signed operation tokens, and strict per-invocation capability scoping.
6. **Token-Level Steganography & Memory Smuggling**:
   - Smuggling shellcode inside zero-width Unicode characters (`\u200b`, `\u200c`) or fragmented multi-turn buffers.
   - *Mitigation*: Unicode NFKC normalization, entropy threshold auditing, and strict JSON deserialization prior to execution surfaces.

### Operational Daemon & High-Gloss Lacquer Web Console
- Zero-dependency Python server (`server.py`) serving the interactive command dashboard on `http://127.0.0.1:5050`.
- Integrated with Antigravity High-Gloss Lacquer design system (`high-gloss-lacquer.css`, `high-gloss-lacquer.js`) and Anti-Slop Craftsman guidelines (pure SVG vectors, $\ge 48\times 48\text{ dp}$ ergonomics).
- Rapid launch cmdlet: `Start-AiDefensePlatform.ps1 -Port 5050`.

---

## 10. Enterprise Container Virtualization & WSL2 Architecture (`docker`)

### Architectural Scope (`G:\My Drive\Antigravity\Projects\docker`)
The **`docker`** project provides an enterprise container virtualization substrate, host kernel tuning framework, and validation testbed tailored for high-performance development on Windows 11 with WSL2. Engineered for the **Acer Predator PH16-71** workstation (Intel Core i9-13900HX, 24 cores / 32 threads, 64 GB DDR5, NVIDIA GeForce RTX 4080 Mobile 12GB), this project bridges local development, Podman/Docker parity, and production OpenShift/Kubernetes workflows.

```mermaid
flowchart TD
    Firmware[Host Hardware: Acer Predator i9-13900HX - BIOS VT-x & VT-d Enabled] --> Windows[Windows 11 Pro - Hyper-V Hypervisor Substrate]
    Windows --> WSLConfig[Global WSL2 Engine Config: C:\Users\chase\.wslconfig]
    WSLConfig --> NetMirrored[networkingMode=mirrored: Direct Host Adapter Parity & Corporate VPN Transparency]
    WSLConfig --> VirtioFS[virtiofs=true: High-Speed Shared-Memory Volume Mounts]
    WSLConfig --> MemoryReclaim[autoMemoryReclaim=gradual & pageReporting=true: Zero vmmem Bloat]
    WSLConfig --> ResourceCaps[Cap: 16 Cores, 16GB RAM, 4GB Swap, sparseVhd=true]
    
    ResourceCaps --> DockerDesktop[Docker Desktop 4.35+/4.98+ WSL2 Engine]
    DockerDesktop --> ComposeStack[docker-compose.yml: Web Microservice & Database Service]
    DockerDesktop --> DiagnosticSuite[Test-DockerEnvironment.ps1: Automated Validation Harness]
    DiagnosticSuite --> PodmanInterop[Rootless Podman 5 & OpenShift Cluster Parity]
```

### Key Technical Pillars

#### 1. Hardware Virtualization (VT-x / VT-d) Firmware Baseline
- **Workstation Configuration**: Intel Core i9-13900HX architecture requires explicit CPU virtualization flags enabled in UEFI/BIOS for hardware-assisted nested paging (SLAT) and I/O virtualization:
  - Access UEFI menu via `F2` (or `Fn + F2`) at cold boot.
  - Press `Ctrl + S` in the *Main* or *Advanced* tab to expose vendor-hidden virtualization menus.
  - Set **Intel (VMX) Virtualization Technology** to **Enabled**.
  - Set **Intel VT-d** (Direct I/O Virtualization) to **Enabled**.
  - Commit changes with `F10` (Save and Exit).

#### 2. Cutting-Edge WSL2 Configuration Matrix (`C:\Users\chase\.wslconfig`)
To completely eliminate traditional Windows virtualization pitfalls—such as the memory-hogging `vmmem` runaway process, sluggish 9P bind mounts, and corporate VPN routing breakages—deploy the following production `.wslconfig`:

```ini
[wsl2]
# Workstation allocation: 16 GB RAM capped for containers (leaves 48 GB for Windows 11 host)
memory=16GB
processors=16
swap=4GB

# Mirrored Networking Mode: Maps Windows host network interfaces directly into Linux.
# Bypasses legacy Hyper-V NAT virtual switch; provides seamless localhost parity and VPN transparency.
networkingMode=mirrored
dnsTunneling=true
autoProxy=true

[experimental]
# VirtioFS: High-performance shared-memory file protocol eliminating legacy 9P file share bottlenecks
virtiofs=true

# Dynamic Memory Reclaim: Hyper-V communicates with guest kernel to return free pages to Windows host
autoMemoryReclaim=gradual
pageReporting=true

# Sparse VHD: Automatically compacts and shrinks virtual hard disk size when files are deleted
sparseVhd=true
```

#### 3. Automated Validation Harness (`Test-DockerEnvironment.ps1`)
The project provides a comprehensive PowerShell test suite enforcing pre-flight verification:
```powershell
# Execute comprehensive host and container diagnostic
.\Test-DockerEnvironment.ps1 -RunContainerTest -Verbose
```
- **Firmware Verification**: Queries `Win32_Processor` WMI classes to verify `VirtualizationFirmwareEnabled: True`.
- **WSL Feature Registry**: Validates Windows features `Microsoft-Windows-Subsystem-Linux` and `VirtualMachinePlatform`.
- **WSL Distro Health**: Checks `wsl -l -v` status for running distributions (Ubuntu, docker-desktop, docker-desktop-data).
- **Docker Daemon Probe**: Verifies named pipe `\\.\pipe\docker_engine` connectivity and Docker CLI version (`docker version`).
- **Live Container Execution**: Spins up transient test container (`hello-world` or `alpine`) and validates clean exit code 0. *(Host Baseline Note verified `2026-11-21`: `Docker Desktop` is currently not installed on the local Windows workstation—install via `winget install Docker.DockerDesktop` or route `DOCKER_HOST` to WSL2 rootless Podman 5.8.x).*

#### 4. Rootless Podman 5.8+ vs. Docker Desktop Interoperability
- **CLI Context Bridging**: Easily switch between standard Docker Desktop and rootless Podman 5.8.x (`RHSA-2026:100547` / `98554` / `97533`, TLS/mTLS API sockets & Go `net/http` `CVE-2026-78667`, `crypto/tls` `CVE-2026-97031`, `crypto/x509` `CVE-2026-111943`, Go SSH `CVE-2026-46597` patched) without modifying scripts:
  ```powershell
  # Target Docker Desktop engine:
  $env:DOCKER_HOST = "npipe:////./pipe/docker_engine"
  
  # Target rootless Podman 5 engine:
  $env:DOCKER_HOST = "unix:///run/user/1000/podman/podman.sock"
  ```
- **SELinux & Volume Semantics**: Standardize bind-mount flags across environments: use `:Z` labels for rootless Podman compatibility while maintaining transparent path mounting in Docker via VirtioFS.
- **Compose Parity**: Ensure `docker-compose.yml` services declare resource limits (`cpus: "2.0"`, `memory: 2048M`) adhering to modern Compose v2 specifications.

### Cross-Portfolio Synergy
- **With `RHCSA Exam200` & `openshift`**: Provides the foundational local container testing environment before transitioning manifests into Podman Quadlets or OpenShift Ingress routes.
- **With `vulnerability management` & `MY Security`**: Local container images and Alpine base layers are actively audited against Cisco openVuln feeds, **CVE-2026-123158 ("SSHole")**, **`CVE-2026-76061`** (CRI-O symlink bind-mount bypass), **`CVE-2026-17106` ("CopyEscape" in `moby/go-archive`)**, and **Podman `RHSA-2026:100547` / `93464` / `98554`** prior to registry promotion.
- **With `Scripting`**: Leverages PowerShell diagnostic cmdlets (`Test-DockerEnvironment.ps1`) adhering strictly to Approved Verbs and object-streaming guidelines.
- **With `deploy`**: Synchronizes container health status into the master deployment telemetry suite.

---

## 11. OpenSource: Enterprise Open-Source Program Office (OSPO), Supply Chain Security & Upstream Governance Hub (`opensource`)

### Architectural Scope (`G:\My Drive\Antigravity\Projects\opensource`)
The **`opensource`** project serves as the centralized Open-Source Program Office (OSPO), software supply chain security control plane, and upstream contribution pipeline across the entire Antigravity **87-project** ecosystem. It establishes standards-based governance for license compliance, automated Software Bill of Materials (SBOM) generation, OpenSSF Scorecard posture checks, SLSA Level 3 build provenance, and automated upstream fork synchronization.

```mermaid
flowchart TD
    Portfolio[Antigravity 87-Project Portfolio] --> Scanner[OSPO Compliance Scanner: ospo_governance.py]
    Scanner --> SBOM[Automated SBOM Generator: CycloneDX 1.6 & SPDX 3.0]
    Scanner --> License[OpenChain ISO/IEC 5230 Engine: License Compliance & Compatibility]
    Scanner --> OpenSSF[OpenSSF Scorecard & SLSA L3 Supply Chain Verifier]
    
    SBOM --> DependencyGraph[Dependency Track & Vulnerability Correlation]
    License --> HeaderCheck[Automated SPDX License Header Validator]
    OpenSSF --> Provenance[Cosign / Sigstore Keyless Attestations]
    
    Upstream[Upstream Open-Source Repos] <--> SyncDaemon[Sync-UpstreamForks.ps1: Automated Rebase & PR Dispatch]
    SyncDaemon --> LocalForks[Local Forks & Subtrees]
    LocalForks --> ReleaseAutomation[git-cliff / release-please: Automated SemVer & Changelog]
```

### Key Technical Pillars

#### 1. Automated Software Bill of Materials (SBOM) Generation (`Generate-ProjectSbom.ps1`)
Standardizes automated SBOM generation adhering to **CycloneDX v1.6 (JSON)** and **SPDX v3.0** formats across all package ecosystems (npm, pip/uv, NuGet, Cargo, Go), fully satisfying global regulatory mandates including CISA Minimum Elements and the European Union Cyber Resilience Act (CRA):
- **CycloneDX v1.6 / v1.7 (OWASP & Ecma International ECMA-424)**: Built *security-first*, providing native support for Vulnerability Exploitability Exchange (VEX), Software-as-a-Service SBOMs (SaaSBOM), Hardware BOMs (HBOM), cryptographic asset tracking, and AI/ML model bill of materials.
- **SPDX v3.0 (Linux Foundation & ISO/IEC Standard)**: Built *provenance- and license-first*, utilizing a modular graph model with specialized profiles for core security, software build pipelines, datasets, and AI/ML dependencies.
- **Interoperability & Translation**: Integrates OpenSSF *Protobom* and *BomCTL* tooling to enable lossless bidirectional conversion between CycloneDX and SPDX without vendor lock-in.

#### 2. OpenSSF Scorecard & Automated Repository Health (0–10 Rating)
The OSPO scanner evaluates all portfolio repositories against 18 automated OpenSSF Scorecard security checks:
- Branch-Protection (enforcing code review and status checks before merge).
- Binary-Artifacts (verifying zero compiled executables or JARs committed to git history).
- Dangerous-Workflow (auditing untrusted GitHub Actions trigger contexts and defending against `r/cybersecurity` Nov 2026 GitHub Actions & npm hook credential-stealing supply-chain campaigns).
- Pinned-Dependencies (verifying SHA-pinned dependencies in action workflows, npm lifecycle scripts, and containerfiles).
- SAST & CodeQL integration.
- Assigns each project a cryptographic health rating from 0.0 to 10.0 to audit supply chain risk.

#### 3. SLSA Level 3 Build Provenance & Sigstore Keyless Attestations
- Generates tamper-proof build provenance statements (in-toto attestation format) certifying exactly *who* built the software, in *which* ephemeral runner, and from *what* immutable git commit SHA.
- Cosign / Sigstore keyless signing verifies releases via OpenID Connect (OIDC) identities, eliminating persistent private key compromise risks.
```powershell
# Generate CycloneDX 1.6 SBOM across portfolio repositories
[CmdletBinding()]
param(
    [Parameter(Mandatory=$false)]
    [string]$TargetProjectDir = "G:\My Drive\Antigravity\Projects"
)

$ErrorActionPreference = 'Stop'
$ScriptDir = Split-Path -Parent $MyInvocation.MyCommand.Path
if (-not $ScriptDir) { $ScriptDir = $PSScriptRoot }
Set-Location -Path $ScriptDir

$Projects = Get-ChildItem -Path $TargetProjectDir -Directory | Where-Object { $_.Name -notmatch '^\.' }

foreach ($Proj in $Projects) {
    Write-Host "Auditing SBOM for: $($Proj.Name)" -ForegroundColor Cyan
    $OutputDir = Join-Path -Path $Proj.FullName -ChildPath ".sbom"
    if (-not (Test-Path $OutputDir)) { New-Item -ItemType Directory -Path $OutputDir -Force | Out-Null }
    
    # Python uv/pip audit
    if (Test-Path (Join-Path $Proj.FullName "requirements.txt")) {
        python -m cyclonedx_py requirements (Join-Path $Proj.FullName "requirements.txt") --output-format json --output-file (Join-Path $OutputDir "bom-python.cdx.json")
    }
    
    # Node.js npm audit
    if (Test-Path (Join-Path $Proj.FullName "package.json")) {
        npx @cyclonedx/cyclonedx-npm --output-file (Join-Path $OutputDir "bom-npm.cdx.json") --output-format JSON
    }
}
```

#### 2. OpenChain (ISO/IEC 5230) License Compliance & Header Validation
Enforces standardized open-source licensing hygiene to prevent unintended copyleft contamination (e.g. GPL-3.0 infecting permissive MIT/Apache-2.0 libraries):
- **SPDX Header Convention**: Every source file must declare an explicit SPDX identifier:
  `// SPDX-License-Identifier: MIT` or `# SPDX-License-Identifier: Apache-2.0`.
- **License Compatibility Matrix**: Automates evaluation of dual-licensed components and flags reciprocal license obligations before production packaging.

#### 3. SLSA Level 3 Build Provenance & OpenSSF Scorecard
- **OpenSSF Scorecard**: Evaluates repos against 18 automated security checks (Branch-Protection, Vulnerabilities, Binary-Artifacts, SAST, Signed-Releases, Security-Policy).
- **Sigstore / Cosign Keyless Attestation**: Signs container images and release artifacts using OpenID Connect (OIDC) identities, binding git commit SHA, runner environment, and builder identity into verifiable in-toto statements.

#### 4. Automated Upstream Synchronization (`Sync-UpstreamForks.ps1`)
Automates tracking and rebasing of cloned and forked upstream repositories:
```powershell
# Automated upstream synchronization loop
[CmdletBinding()]
param()

$Forks = @(
    @{ Name = "TensorRT-LLM"; Path = "G:\My Drive\Antigravity\Projects\How to train your AI\upstream\TensorRT-LLM"; Upstream = "https://github.com/NVIDIA/TensorRT-LLM.git"; Branch = "main" },
    @{ Name = "vLLM"; Path = "G:\My Drive\Antigravity\Projects\How to train your AI\upstream\vllm"; Upstream = "https://github.com/vllm-project/vllm.git"; Branch = "main" },
    @{ Name = "Model-Optimizer"; Path = "G:\My Drive\Antigravity\Projects\How to train your AI\upstream\Model-Optimizer"; Upstream = "https://github.com/NVIDIA/Model-Optimizer.git"; Branch = "main" }
)

foreach ($Fork in $Forks) {
    if (Test-Path $Fork.Path) {
        Write-Host "Syncing upstream for $($Fork.Name)..." -ForegroundColor Green
        Set-Location $Fork.Path
        git fetch upstream $($Fork.Branch)
        git rebase "upstream/$($Fork.Branch)"
    }
}
```

### Cross-Portfolio Synergy
- **With `deploy`**: Exports consolidated portfolio SBOM telemetry into `deploy/PROJECT_CATALOG.json` and health scans.
- **With `vulnerability management`**: Feeds dependency graphs directly into CVE vulnerability matching engines and Cisco openvuln-mcp.
- **With `ai slop`**: Pairs licensing hygiene with anti-slop code quality audits across all 79 projects.
- **With `Github Portfolio`**: Powers public GitHub contribution graphs and open-source project badges.

---

## 12. Cram Exam TV Live Companion & Certification Training Environment (`Cert Training Guide`)

### Architectural Blueprint (`G:\My Drive\Antigravity\Projects\Cert Training Guide`)
The **`Cert Training Guide`** project establishes an enterprise-grade, fullscreen ($100\text{vw} \times 100\text{vh}$) certification training command center and companion suite. Built around the 24/7 live **Cram Exam TV** broadcast (`@cramexam` on YouTube), it directly bridges video lectures with local terminal labs across CompTIA Security+ SY0-701, Red Hat Certified System Administrator (RHCSA EX200), Red Hat OpenShift Administrator (EX280), Docker, and enterprise scripting.

```mermaid
flowchart TD
    Shell[Fullscreen 100vw x 100vh Learning Shell: index.html] --> Stream[24/7 Embedded Live Stream: YouTube @cramexam]
    Shell --> Syllabus[30-Day Day-by-Day Curriculum: DAILY_TRAINING_GUIDE.md]
    Shell --> Bridge[Cross-Project Simulator Bridge: CRAM_EXAM_INTEGRATION_MAP.md]
    Shell --> Tools[Exam Drill Tools: Pomodoro, L.O.C. Engine, Quizzes, Scratchpad]
    
    Bridge --> SecuritySim[comptia exam simulator: 5 SY0-701 Full Exams & PBQs]
    Bridge --> LinuxLab[RHCSA Exam200: RHEL 9/10 Lab Exercises]
    Bridge --> ContainerLab[docker & openshift: Podman, CRI-O, K8s 1.32]
    Bridge --> ScriptingLab[Scripting: Bash & Modern PowerShell Automation]
    
    Scheduler[Schedule-WatchSessions.ps1] --> TaskScheduler[Windows Task Scheduler 3-Tier Watchtime Cadence]
    TaskScheduler --> Morning[07:30 - 08:15 Morning Concept Priming]
    TaskScheduler --> Lunch[12:30 - 13:00 Lunch Rapid Scenario Review]
    TaskScheduler --> Evening[18:30 - 19:30 Evening Hands-on Terminal Lab]
```

### Key Technical Pillars

#### 1. Fullscreen Enterprise Interface ($100\text{vw} \times 100\text{vh}$) & Zero Dead Margins
- **GitHub Primer Dark Material Theme**: Strict 1px high-contrast borders, dual-tone inline vector SVGs, and responsive split view docking without window scrolling.
- **Embedded 24/7 Cram Exam TV Player**: Zero-latency, zero-interruption YouTube embed of `@cramexam`'s live stream with 1-click external popup and theater expand controls.
- **Real-Time Stream Scratchpad**: Notes area with automatic timestamp generation (`[07:35:12]`) and persistent `localStorage` synchronization across sessions.

#### 2. Cross-Project Lab Integration Matrix (`CRAM_EXAM_INTEGRATION_MAP.md`)
Directly maps theoretical video topics covered on stream to local hands-on practice environments:
- **CompTIA Security+ SY0-701 & ISC2 CC**: Deep links to `comptia exam simulator` for 5 complete timed practice exams, diagnostic PBQ network topologies (`diagnose.html`), and audio cheat sheet.
- **RHCSA EX200 (RHEL 9/10)**: Deep links to `RHCSA Exam200` for 22 terminal tasks (LVM storage, Podman Quadlets, systemd v256+ `run0`, Landlock LSM, and SGID permissions).
- **Red Hat OpenShift EX280**: Deep links to `openshift` for DO280 administration, Gateway API HTTPRoutes, ClusterUserDefinedNetworks (CUDNs), and Cosign supply chain verification.
- **Scripting & Containers**: Deep links to `Scripting` (14 enterprise bash/powershell labs) and `docker` (`Test-DockerEnvironment.ps1`, WSL2 Mirrored networking).

#### 3. Cram Exam L.O.C. Framework Decision Engine (`app.js`)
An interactive architectural evaluation calculator assessing AWS Cloud Data Architectures (DEA-C01) across 3 dimensions:
- **L (Latency)**: Batch vs. Micro-batch vs. Real-time streaming (Kinesis, Kafka, MSK).
- **O (Operational Overhead)**: Serverless (Athena, Glue) vs. Managed clusters (EMR) vs. Self-hosted.
- **C (Cost)**: Spot vs. On-demand vs. Serverless compute tradeoffs.

#### 4. Automated Daily Watchtime Cadence (`Schedule-WatchSessions.ps1`)
Production-grade PowerShell automation script managing scheduled study sessions in Windows Task Scheduler:
- **Morning Priming (`07:30 - 08:15`)**: Concept overview, flashcards, and Web Speech API audio read-aloud of high-yield acronyms.
- **Lunch Active Recall (`12:30 - 13:00`)**: Interactive scenario quizzes and common exam trap triage.
- **Evening Hands-On Lab (`18:30 - 19:30`)**: Hands-on terminal simulation, PBQ solving, and mock exam execution.
- Cmdlet execution syntax:
  ```powershell
  Set-Location "G:\My Drive\Antigravity\Projects\Cert Training Guide"
  .\Schedule-WatchSessions.ps1 -Action Register  # Registers 3 daily scheduled tasks
  .\Schedule-WatchSessions.ps1 -Action Launch    # Immediately opens index.html & live stream
  ```

### Cross-Portfolio Synergy
- **With `comptia exam simulator` & `RHCSA Exam200`**: Synchronizes flashcards, PBQs, and terminal lab scenarios.
- **With `deploy`**: Monitored as a healthy deployable project in `PROJECT_CATALOG.json` and `health_status.json`.
- **With `automate my day`**: Morning briefings ingest scheduled study goals and upcoming certification milestones.



