# Snort | Exploring Intrusion Detection and Prevention with Snort in My Homelab

Welcome to my Snort exploration project! In this repository, I invite you to delve into the world of Intrusion Detection and Prevention Systems (IDS/IPS) as I deploy Snort in my homelab environment.

<h3>WHAT IS SNORT?</h3>

Snort is a renowned open-source intrusion detection and prevention system that offers powerful network security monitoring capabilities. It can perform real-time traffic analysis and packet logging on IP networks, helping to detect and prevent a variety of attacks such as exploits, malware infections, and suspicious activities. With its signature-based and protocol analysis features, Snort is a valuable tool for enhancing network security.

<h3>WHY SNORT?</h3>

Understanding and effectively countering modern cyber threats are crucial skills in today’s digital landscape. Snort empowers security professionals to:

**1. Detect Intrusions:** Snort can identify unauthorized access attempts, unusual traffic patterns, and potential security breaches in real-time, enabling swift responses to mitigate threats.

**2. Prevent Attacks:** With its Intrusion Prevention System (IPS) capabilities, Snort can actively block and prevent suspicious network traffic, adding an extra layer of defense against various cyberattacks.

**3. Analyze Network Traffic:** Snort’s rich set of analysis tools provides insights into network behaviors, aiding in the identification of vulnerabilities and security gaps.

<h3>HANDS ON, TIME TO INSTALL SNORT</h3>

**Prerequisites:**

In my case, as I'm using Proxmox, I'm going to deploy Snort using a container (LXC) running Ubuntu, you can follow these steps:

**Step 1: Create an Ubuntu LXC Container**

1. Log in to the Proxmox web interface.
2. Select the node where you want to create the LXC container.
3. Click on "Create CT" (Container).
4. In the "General" tab, provide a unique ID for the container (e.g., 100) and set a hostname.
5. Under "Template," select "ubuntu-20.04" or the Ubuntu version of your choice.
6. Set the "Root Password" and any other necessary options.
7. Click "Next" and review your settings. Then, click "Finish" to create the container.
8. Start the container by selecting it in the Proxmox web interface and clicking "Start."

**Step 2: Access the Ubuntu Container**

1. Once the Ubuntu container is running, you can access it via SSH or the Proxmox web terminal.
2. Open a terminal or SSH client and connect to the IP address of the LXC container. You'll need the root username and password you set during container creation.

**Step 3: Update & Upgrade your Container**

1. Update the package list inside the container:

````
sudo apt update
sudo apt upgrade
````

**Step 4: Install Snort**

1. Install Snort and necessary dependencies:
````
sudo apt install -y snort
````
2. During the installation, you will be prompted to configure the Oinkcode. If you have a registered account on the **Snort website**(https://www.snort.org/), enter your Oinkcode. If not, you can skip this step.

3. Configure Snort to run in IDS mode:
Edit the configuration file:
````
sudo nano /etc/snort/snort.conf
````
Find the line **config detection_mode** and change it to:
````
config detection_mode: none
````
Save and exit the editor.

4. Create a Snort rules directory:
````
sudo mkdir /etc/snort/rules
````
5. Download the community rules:
````
sudo snort -q --daq-list
sudo snort -A alert -q -u snort -g snort -c /etc/snort/snort.conf -i <Your_Network_Interface>
````
Replace **<Your_Network_Interface>** with the appropriate network interface where you want Snort to monitor traffic.

6. Start Snort:
````
sudo snort -q -u snort -g snort -c /etc/snort/snort.conf -i <Your_Network_Interface>
````
Replace **<Your_Network_Interface>** with the same network interface as above.

7. Snort is now running in IDS mode, monitoring network traffic based on the rules.

Please note that this basic setup provides you with a functional Snort installation. For production environments or more complex setups, additional configurations and tuning are required. Make sure to consult the Snort documentation for in-depth configurations and best practices.

**Contributions are more than Welcome**

I encourage contributions, feedback, and collaboration from the community. If you have suggestions, improvements, or questions, please feel free to open issues or submit pull requests.

Thank you,</br>
Lucas

