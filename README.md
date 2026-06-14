# dnscrypt-proxy: Anonymized DNS Configuration

A hardened `dnscrypt-proxy` configuration focused on **Anonymized DNS**, strict European jurisdiction filtering, and zero-leak resilience.

<img width="880" height="275" alt="image" src="https://github.com/user-attachments/assets/948dba5e-8593-4399-847f-50b458da01be" />

## 🛡️ Key Features

*   **Anonymized DNS:** Double-hop routing ensures no single entity sees both your IP and query.
*   **Strict Jurisdiction:** Relays and resolvers restricted to FR, DE, CH, NL, DK (No US/UK/Five Eyes).
*   **Zero Leaks:** Hardcoded server lists with explicit IPv4/IPv6 relay mapping prevent fallback leaks.
*   **Security First:** Enforced DNSSEC, Quad9 malware filtering, and disabled DoH/system fallbacks.
*   **Optimized Latency:** ~137ms baseline from US via protocol-separated routing.

## ⚡ Quick Start

1.  **Backup & Replace Config**
    ```bash
    sudo cp /etc/dnscrypt-proxy/dnscrypt-proxy.toml{,.bak}
    # Paste the config below into /etc/dnscrypt-proxy/dnscrypt-proxy.toml
    ```

2.  **Lock System DNS**
    Ensure `/etc/resolv.conf` contains *only*:
    ```text
    nameserver 127.0.0.1
    nameserver ::1
    ```
    *(Tip: Use `chattr +i /etc/resolv.conf` or configure NetworkManager/iwd to ignore auto-DNS)*

3.  **Restart Service**
    ```bash
    sudo systemctl restart dnscrypt-proxy
    ```

## 🔍 Troubleshooting

| Issue | Fix |
| :--- | :--- |
| **FATAL error on start** | Ensure old TOML content was fully deleted before pasting. Check for syntax errors. |
| **DoH appearing in logs** | Verify `doh_servers = false`. Anonymization requires DNSCrypt only. |
| **Internet broken** | Your system is likely still using router/ISP DNS. Point it to `127.0.0.1`. |
| **Latency spikes** | Check logs for `[incompatible]` warnings; indicates relay/server mismatch. |

## 📜 Credits

Configuration maintained by [bttermlkchkn](https://github.com/bttermlkchkn). Built upon the excellent work of **Quad9**, **DCT**, **DNSCry.pt**, and the **dnscrypt-proxy** maintainers.

*Licensed under MIT. Use at your own risk.*
