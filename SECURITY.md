# Security Policy

Sensitive security-related questions, comments, and reports should be reported privately via: [GitHub security advisories](https://github.com/NewEraCracker/suhosin/security/advisories/new)

## Security Advisory

**CVE-2026-109618** and **CVE-2026-109619** identify two critical remote code execution vulnerabilities in **PHP**. Upload processing and session upload-progress handling are among the relevant attack paths, but they do not fully describe both vulnerabilities.

**Suhosin does not completely mitigate these vulnerabilities**.

To reduce the attack surface regarding `php_rfc1867_callback` in `ufilter.c`, this project has implemented the following mitigation:

- The `SUHOSIN_FORWARD_RFC1867_CALLBACK` directive has been set to `0`. This disables external callback forwarding while preserving Suhosin's internal multipart filters and cleanup mechanisms.

To remediate the problem, the following companion solution is recommended:

- **[php_uploadprogress_guard](https://github.com/HOSTED-POWER/php_uploadprogress_guard)** - a hardened extension that provides additional protection for upload-progress tracking and reduces exposure to related attack vectors.

## Supported Versions

| Version | Supported |
|---------|-----------|
| `master` | :warning: **No active support** |
| Any release | :x: **No support** |

## Security Guidance

**Mitigate the risk** using other security controls (WAF, network segmentation, etc.).

**Consider migrating** to modern alternatives.

## Reporting a Vulnerability

This project is **deprecated** and receives **no security updates**.

If you discover a vulnerability, you may report it at your discretion, but **expect no response or remediation**.
