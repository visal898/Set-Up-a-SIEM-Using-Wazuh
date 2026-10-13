# Set-Up-a-SIEM-Using-Wazuh
As I started moving deeper into security operations and defensive security, one tool kept showing up in job descriptions, SOC interviews, and real world security discussions: SIEM. I had read about SIEM platforms before, but I realized that understanding them conceptually was not enough. I wanted to know how they actually work in practice.
This project was my way of building that experience. I set up a Wazuh SIEM from scratch, connected both Linux and Windows endpoints, and explored the security data those systems generate in real time. My goal was to simulate a realistic SOC style environment where logs from multiple systems are centralized, analyzed, and used for security visibility and detection.

This article walks through exactly how I did that and what I learned along the way.
<img width="720" height="421" alt="image" src="https://github.com/user-attachments/assets/5fe36c22-a04d-4754-b992-b2644e18d2af" />
What a SIEM Is and Why It Matters
A SIEM, which stands for Security Information and Event Management, is a platform that collects logs and security events from multiple systems, analyzes them, and presents them in a centralized interface.

In a real environment, a SIEM helps security teams answer questions like:

Are there suspicious login attempts happening right now?
Did someone modify system files they should not have?
Are there indicators of brute force activity or privilege misuse?
What changed on the network in the last hour?
Without a SIEM, this information is scattered across individual machines. With a SIEM, it becomes centralized, searchable, and actionable.

Why I Chose Wazuh
I chose Wazuh because it aligns closely with real world SOC tooling and workflows. It is open source, actively maintained, and widely used in security monitoring environments.

Wazuh provides:

Log collection and analysis
File integrity monitoring
Authentication and system activity monitoring
Endpoint visibility for both Linux and Windows systems
It also integrates with OpenSearch and a web dashboard, which makes it ideal for learning how security data is visualized and investigated in practice.

Step 1: Setting Up the Wazuh SIEM Server on Ubuntu
I deployed the Wazuh manager on Ubuntu Server, which mirrors how SIEM infrastructure is commonly deployed in production environments.

First, I updated the system:

**sudo apt update && sudo apt upgrade -y**

Next, I downloaded and ran the official Wazuh installation script on Ubuntu terminal. This installer sets up the Wazuh manager, API, OpenSearch backend, and dashboard automatically.

<img width="1400" height="882" alt="image" src="https://github.com/user-attachments/assets/c84f4101-d89d-4d4d-8283-fcde8af4d871" />

**curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a**

<img width="866" height="629" alt="image" src="https://github.com/user-attachments/assets/5e6c24ce-f6be-4869-bd26-7e9cc1d739ef" />

The installation took some time, but once it completed, I had a fully operational SIEM backend. At the end of the process, Wazuh generated dashboard login credentials, which I saved for later access.

Press enter or click to view image in full size


<img width="866" height="629" alt="image" src="https://github.com/user-attachments/assets/012da77a-69c0-4f98-a844-476044c9676f" />

At this stage, the SIEM infrastructure was live but had no endpoint data yet.

Step 2: Logging Into the Wazuh Dashboard
Using a browser, I accessed the dashboard at:



