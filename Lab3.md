# Standard Operating Procedure: Setup a Virtual Linux Server for Web Application Test

## Revision Information:
* **Version:** 1.0
* **Date:** 2025-07-18
* **Author:** John Florendo

## Approved Table:
*(This section is for formal sign-offs. In a real-world scenario, signatures of relevant stakeholders would be placed here to indicate approval of the procedure.)*

---

## Purpose

The objective of this Standard Operating Procedure (SOP) is to provide fundamental, step-by-step guidance for establishing a virtual Linux server environment specifically tailored for web application testing. This procedure aims to ensure a straightforward and consistent setup process, facilitating effective testing of web applications.

---

## Scope

This document is applicable to individuals responsible for the initial configuration and testing of web applications within a controlled environment. The SOP outlines the core process for setting up a virtual machine, installing a basic Linux operating system, configuring essential network settings, and deploying fundamental software components necessary for web application functionality.

**Key objectives to be achieved through this SOP:**
* Establish a foundational operating system environment.
* Ensure network connectivity for the server.
* Install core web server software.
* Install basic database management capabilities.
* Facilitate the deployment of web application code.

---

## Accountability Matrix

| Role                       | Responsibility                                                                |
| :------------------------- | :---------------------------------------------------------------------------- |
| **System Administrator** | Provisioning virtual machine resources, initial OS installation, network configuration. |
| **Quality Assurance Analyst** | Deploying web applications and executing functional tests.        |
| **Developer** | Deploying and debugging web applications during development phases.  |
| **Security Reviewer** | Conducting preliminary security assessments of the web application.               |

---

## Definitions

* **SOP:** Standard Operating Procedure; a documented set of instructions for a routine task.
* **VM:** Virtual Machine; a software-based emulation of a computer system.
* **Linux:** An open-source operating system kernel, forming the basis of distributions like Ubuntu.
* **Web Application:** A client-server software application where the client (user interface) runs in a web browser.
* **SSH:** Secure Shell; a cryptographic network protocol for secure remote command-line access.
* **IP Address:** A numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication.

---

## Procedure Steps

This section details the sequential actions required to configure the virtual Linux server.

### Step 1: Virtual Machine Creation

1.  **Select Hypervisor:** Choose a virtualization software platform (e.g., VirtualBox, VMware Workstation).
2.  **Initiate VM Creation:** Begin the process of creating a new virtual machine within the chosen hypervisor.
3.  **Resource Allocation:**
    * **Operating System Type:** Specify Linux / Ubuntu (64-bit).
    * **Processor Cores (CPU):** Assign at least 2 virtual CPU cores.
    * **Memory (RAM):** Allocate a minimum of 4GB of RAM.
    * **Storage (Disk Space):** Provide at least 50GB of virtual disk space.
    * **Network Configuration:** Configure the network adapter in `Bridged` mode to ensure the VM is directly accessible on the host's network.
4.  **ISO Image Attachment:** Mount the Ubuntu Server (e.g., 22.04 LTS) installation ISO image to the virtual CD/DVD drive.

### Step 2: Ubuntu Server Installation

1.  **Start Virtual Machine:** Power on the newly created virtual machine.
2.  **Language Selection:** Choose the desired installation language and keyboard layout.
3.  **Network Setup:** Proceed with the default DHCP network configuration during installation.
4.  **Disk Partitioning:** Select the option to use the entire virtual disk for installation.
5.  **User Profile Setup:**
    * **Full Name:** Provide your full name.
    * **Server Hostname:** Assign a descriptive hostname (e.g., `test-web-server`).
    * **Username:** Create a user account (e.g., `adminuser`).
    * **Password:** Establish a robust password for the user account.
6.  **SSH Server Installation:** Select and install the OpenSSH server component to enable secure remote access.
7.  **System Reboot:** Upon completion of the installation, restart the virtual machine.

### Step 3: Initial Server Setup and Updates

1.  **Establish SSH Connection:** Access the server remotely using SSH from your host machine: `ssh adminuser@<server_ip_address>`.
2.  **System Package Update:**
    * `sudo apt update` (to refresh available package lists)
    * `sudo apt upgrade -y` (to install all pending updates)
3.  **Install Essential Utilities:** `sudo apt install -y curl git nano htop` (installs commonly used command-line tools).
4.  **Configure Firewall:**
    * `sudo ufw allow OpenSSH` (permits SSH connections)
    * `sudo ufw allow 80/tcp` (permits standard web traffic on port 80)
    * `sudo ufw enable` (activates the firewall; confirm with 'y')

### Step 4: Web Server Installation (Apache)

1.  **Install Apache2:** Execute the command: `sudo apt install -y apache2`.
2.  **Verify Web Server Functionality:** Open a web browser on your host machine and navigate to `http://<server_ip_address>`. The default Apache welcome page should be displayed.

### Step 5: Database Server Installation (MySQL)

1.  **Install MySQL Server:** Execute the command: `sudo apt install -y mysql-server`.
2.  **Secure MySQL Installation:** Run `sudo mysql_secure_installation` and follow the prompts
