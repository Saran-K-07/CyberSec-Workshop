# Day 4: Social Engineering Attacks using SEToolkit

## Introduction
Welcome to Day 4 of the Foundations of Cybersecurity: Threats, Tools &amp; Practical Defence! Today, we will explore **Social Engineering Attacks** using the **Social-Engineer Toolkit (SEToolkit)**. Social engineering is a technique where attackers manipulate people into revealing confidential information or performing actions that compromise security. SEToolkit is an open-source tool that helps simulate these attacks for educational purposes.

This guide is designed for complete beginners. We'll walk through the basics step by step. Remember, this is for learning only—never use these techniques on real people or systems without permission.

## Prerequisites
- A computer with Kali Linux (or a virtual machine running Kali).
- Basic knowledge of the command line (from previous days).
- SEToolkit installed (if not, run `sudo apt update && sudo apt install setoolkit`).

## What is SEToolkit?
SEToolkit is a penetration testing framework that automates social engineering attacks. It includes modules for phishing, credential harvesting, and more. We'll focus on a simple phishing attack simulation.

## Step-by-Step Guide
1. **Open SEToolkit**:
    - Launch your terminal.
    - Type `sudo setoolkit` and press Enter.
    - Enter your password if prompted.

2. **Select an Attack Type**:
    - Choose option 1: "Social-Engineering Attacks".
    - Then select option 2: "Website Attack Vectors".
    - Choose option 3: "Credential Harvester Attack Method".
    - Select option 2: "Site Cloner" to clone a fake login page.

3. **Clone a Website**:
    - Enter the URL of a site to clone (e.g., a fake login page like `http://example.com/login`).
    - Provide the IP address of your machine (use `ifconfig` to find it).
    - SEToolkit will generate a fake site and start a listener.

4. **Test the Attack**:
    - Open a web browser and go to the IP address provided.
    - Try logging in with fake credentials—the tool will capture them.
    - Check the SEToolkit terminal for harvested data.

5. **Clean Up**:
    - Stop the listener with Ctrl+C.
    - Exit SEToolkit.

## Key Concepts
- **Phishing**: Tricking users into entering sensitive info on fake sites.
- **Credential Harvesting**: Collecting usernames and passwords.
- Always use in a controlled environment (e.g., your own network).

## Resources
- [SEToolkit Official Site](https://www.trustedsec.com/tools/the-social-engineer-toolkit-set/)
- [OWASP Social Engineering Cheat Sheet](https://owasp.org/www-pdf-archive/OWASP_AppSec_DC_2017_Social_Engineering_Cheat_Sheet.pdf)
- Ask questions in the whatsapp group!

Stay ethical and have fun learning!