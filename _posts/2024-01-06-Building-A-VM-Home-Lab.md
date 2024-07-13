---
title: Building a Virtual Machine (VM) Home Lab
date: 2024-02-01 20:18:30 -0700
categories: [Projects, Virtual Machine (VM) Home Lab]
tags: [projects]
description: Learn how I designed and created a virtual machine (VM) home lab in VirtualBox using free resources, tools, and services.
image: /assets/img/article_prev/VirtualBox_logo.jpg
---

In my [article](https://christiancarnate.com/posts/Competing-for-a-Cybersecurity-Role/) about competing for a cybersecurity role, I mentioned that projects are an excellent way to differentiate you from the competition. One of these projects that you can add to your résumé is a virtual machine (VM) home lab.

## Network Diagram

![Network diagram.](/assets/img/article_img/VM_HomeLab/VM_HomeLab_NetworkDiagram.png)

## Resources, Tools, and Services Used

### Resources

- **Building Virtual Machine Labs: A Hands-on Guide (Second Edition)**: A [textbook](https://leanpub.com/avatar2) by Tony Robinson that served as the main resource for building this VM home lab from scratch.
- **Splunk Enterprise Admin Manual:** The [official documentation](https://docs.splunk.com/Documentation/Splunk/9.2.2/Admin/Howtousethismanual) for the administration of Splunk Enterprise.
- **Your All-In-One Guide to Setting up pfSense and Suricata in Splunk:** An [article](https://hurricanelabs.com/splunk-tutorials/your-all-in-one-guide-to-setting-up-pfsense-and-suricata-in-splunk/) by Austin O'Neil that provides a walkthrough of forwarding pfSense and Suricata logs to an index on a Splunk indexer.
- **Deploying the Splunk Universal Forwarder on Windows:** An [article](https://hurricanelabs.com/splunk-tutorials/deploying-the-splunk-universal-forwarder-on-windows/) by Tom Kopchak that provides a walkthrough of installing and configuring the Splunk Universal Forwarder on a Windows machine.

### Tools

- **Azure Dev Tools for Teaching:** I obtained free software licenses from [Azure Dev Tools for Teaching](https://azureforeducation.microsoft.com/devtools) because I am a Grand Canyon University student.
- **mRemoteNG:** [mRemoteNG](https://mremoteng.org/) is an open-source, tabbed, multi-protocol remote connections manager for Windows.
- **WinSCP:** [WinSCP](https://winscp.net/eng/index.php) is an SFTP/FTP/SCP client for Windows.
- **PuTTYgen:** [PuTTYgen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) is a Windows application for generating SSH public/private keys.
- **Notepad++:** [Notepad++](https://notepad-plus-plus.org/) is a powerful text editor which I used to format the SSH keys generated from PuTTYgen to be compatible with Linux operating systems.

### Hypervisor

- **VirtualBox:** [VirtualBox](https://www.virtualbox.org/) is a free, open-source type 2 hypervisor for Windows, Mac, and Linux operating systems running x86/x64 CPU architectures that support virtualization.

### Firewall

- **pfSense:** [pfSense](https://www.pfsense.org/) is a free, open-source firewall based on the FreeBSD operating system.
- **Suricata:** [Suricata](https://suricata.io/) is a free, open-source intrusion detection and prevention system (IDPS) for Linux operating systems. In my VM home lab, the Suricata instance is an installed pfSense package.

### Management Network

- **Ubuntu Linux:** [Ubuntu Linux](https://ubuntu.com/) is a free, mostly open-source, and Debian-based Linux distribution that is commonly used for its flexibility.
- **Splunk Enterprise:** [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) is the on-premises installation of Splunk. I installed Splunk, configured the free license group, and configured the forwarding of Suricata logs (from the pfSense VM) and Aurora EDR/Windows Defender logs (from the Windows 10 VM Sandbox) to the Splunk indexer via the [Splunk Universal Forwarder](https://www.splunk.com/en_us/blog/learn/splunk-universal-forwarder.html).
- **Kali Linux:** [Kali Linux](https://www.kali.org/) is a free, open-source, Debian-based Linux distribution made for penetration testers and ethical hackers. Essentially, it is the script kiddie's best friend.

### System Administration Network

- **Windows Server 2022/Windows 10 Education:** [Windows](https://www.microsoft.com/en-us/windows) is a series of operating systems developed and owned by Microsoft for personal computers and enterprises. I configured the Windows Server 2022 VM to be an Active Directory Domain Controller, created a domain forest, and joined the Windows 10 Education VM to the domain.
- **Fedora Server 39/Fedora KDE Plasma Desktop 39:** [Fedora Linux](https://fedoraproject.org/) is a free, open-source Linux distribution developed by the Fedora Project, which is primarily sponsored by Red Hat. You can think of Fedora Linux as the playground for software development updates for CentOS and Red Hat Enterprise Linux.

### Malware Analysis Network

- **Flare-VM:** [Flare-VM](https://github.com/mandiant/flare-vm) is an overlay for malware analysis and reverse engineering on Windows 10+.
- **SIFT Workstation:** [SIFT Workstation](https://www.sans.org/tools/sift-workstation/) is an incident response and digital forensics toolkit for Linux.
- **REMnux:** [REMnux](https://remnux.org/) is a malware analysis and reverse engineering toolkit for Linux.
- **Aurora EDR (Lite Edition):** [Aurora EDR](https://www.nextron-systems.com/aurora/) is a lightweight and customizable EDR agent that uses Sigma rules for detection.
- **Splunk Universal Forwarder:** [Splunk Universal Forwarder](https://www.splunk.com/en_us/blog/learn/splunk-universal-forwarder.html) is a host-based agent that forwards data from Windows, Linux, macOS, FreeBSD, Solaris, and AIX machines.

## Configuration Files

You can view and/or download the network diagram and/or configuration files associated with this project [here](https://github.com/christian-carnate/vm-homelab).

## Conclusion

Although much work has already been completed, my VM home lab is a work-in-progress, and I will expand upon it to learn new skills when necessary. If you have an idea on how I can expand my VM home lab, feel free to message me through any of my social media contacts.
