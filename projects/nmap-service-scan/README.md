# Scoped Nmap service scan

## Objective

Identify services reported on four selected TCP ports of one owned Metasploitable 2 VM, and preserve the output for review.

## Environment and tools

Nmap 7.99 ran from Kali Linux 2026.3 on a [private VMware LAN segment](../virtual-lab-setup/README.md). The only target was `192.168.77.20`. Ports 21, 22, 80 and 445 were in scope.

## Method

1. Checked guest addresses, routes and local reachability.
2. Ran a TCP connect scan with light service-version detection, reverse DNS disabled and port-state reasons requested.
3. Saved normal, XML and grepable results and compared the displayed output with the saved file.

Portable equivalent of the recorded command, with the local output path shortened:

```sh
nmap -n -sT -sV --version-light --reason -p 21,22,80,445 -oA nmap-target 192.168.77.20
```

## Results

Nmap reported one host up and four open ports: FTP / vsftpd 2.3.4 on 21, SSH / OpenSSH 4.7p1 on 22, HTTP / Apache httpd 2.2.8 on 80, and netbios-ssn / Samba smbd 3.X–4.X on 445. It completed in 6.51 seconds. These are service observations and version estimates, not proof of exploitation or a confirmed CVE.

Evidence: [original Kali screenshot](evidence/nmap-result.png) and [sanitised output excerpt](evidence/scan-output.txt). The [pre-scan route check](../virtual-lab-setup/evidence/route-check.txt) records the private scope.

[Screenshot provenance and hashes](../../EVIDENCE.md)

## Next step

I would check the target's actual installed packages and configuration, then compare those details with a relevant advisory before claiming a vulnerability. The four selected ports do not describe the whole host. No exploitation was attempted.

[View the project page](index.html)
