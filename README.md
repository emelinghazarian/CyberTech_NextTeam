# CyberTech_NextTeam

# Using Large Language Models (LLMs) with RAG to Detect Infrastructure Misconfigurations and Suggest fixes

## ** Overview**
This project demonstrates how to use **RAG (Retrieval-Augmented Generation) + ZySec LLM** to **detect misconfigurations** in infrastructure settings based on **Ubuntu STIG security best practices**.  

**Live Demo** (Gradio UI):  
[Access the Gradio Interface](https://451592b777de1bb5ce.gradio.live)  
**Username:** `admin`  
**Password:** `NextTeamsProjectsMinimumViableProductDemonstration$0$&/`

**Built on:**  
- [Kotaemon](https://github.com/Cinnamon/kotaemon/) – An open-source, clean & customizable RAG UI for chatting with documents.  
- **ZySec LLM** ([Hugging Face Model](https://huggingface.co/koesn/ZySec-7B-v1-GGUF)) – A security-focused LLM for analyzing configurations.  
- **Ubuntu STIG** – ([Canonical Ubuntu 22.04 LTS STIG Guide](https://www.stigviewer.com/stig/canonical_ubuntu_22.04_lts/)) – Used as a benchmark for security compliance.
- **Ansible** – Automates infrastructure data collection via **SSH keys for endpoint authentication**.

**Features:**  
**The architecture is designed for automated security analysis, leveraging Ansible for SSH-based access to endpoints.**  
**SSH keys of endpoints are provided to Ansible** for secure infrastructure data retrieval.    
**The system connects to an endpoint and extracts key infrastructure data. (used Ubuntu OS for testing and validation.)**
**Extracts infrastructure configurations from an Ubuntu endpoint and structures the data into a JSON file.**  
**Collected data includes:**  
   - Running **processes**  
   - **Services**  
   - **Security policies**  
   - **System settings**  
   - Organized across **multiple layers** for better analysis
**Compares system configurations against STIG best practices (Ubuntu 22.04 LTS).**  
**Detects security misconfigurations in real-time.**  
**Provides fixes & recommendations for compliance.**  


## **Project Structure**
```bash
│── /configs
│   ├── system_config.txt   # Extracted system configuration for Ubuntu
│   ├── Ubuntu_STIG.csv     # STIG security best practices for Ubuntu 22.04
│── /models
│   ├── zysec-7b-v1.gguf   # ZySec LLM model file
│── /rag_ui
│   ├── kotaemon-ui        # Kotaemon RAG-based UI for chat interface
│── /ansible
│   ├── gather_data.yml    # Ansible playbook for data collection
│   ├── system_data_vuln.json  # Collected JSON data with security vulnerabilities
│── README.md

```

## **Setup Instructions**

### **Clone the Repository**
```bash
git clone [https://github.com/your_username/your_repo.git](https://github.com/Cinnamon/kotaemon/?tab=readme-ov-file)
```

### **Install Dependencies**
Ensure you have Python and the required libraries installed:
```bash
pip install -r requirements.txt
```

### **Download & Load ZySec LLM **
Download the ZySec LLM model from Hugging Face and place it in the /models directory:
```bash
wget https://huggingface.co/koesn/ZySec-7B-v1-GGUF/resolve/main/zysec-7b-v1.gguf -P models/
```
![LMM](https://github.com/user-attachments/assets/c984b5e9-8a00-4dc7-a3b5-e0248bcd9f82)

### **Configure & Run Ansible for Data Collection**
The Ansible playbook connects to endpoint servers via SSH, retrieves system configurations, and hashes the collected data for tracking updates.
**Setup SSH Keys for Ansible**
The Ansible playbook (gather_data.yml) connects to remote Ubuntu endpoints via SSH to collect system configurations and stores them in a structured JSON file (system_data_vuln.json).
1.Install Ansible
If Ansible is not already installed, install it with:
```bash
sudo apt update && sudo apt install ansible -y
```
2.Generate SSH Keys (if not already set up)
If you haven't set up SSH keys for Ansible authentication, generate them with:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""
```

3. Copy SSH Key to Endpoint Servers
Replace 192.168.1.100 with your actual server's IP:
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@192.168.1.100
```

4. Configure Ansible Inventory
Edit ansible/inventory.ini to define your remote servers:
```ini
[ubuntu_servers]
192.168.1.100 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```
5.Run the Ansible Playbook to Collect Infrastructure Data
Navigate to the Ansible directory and run the playbook:
```bash
cd ansible
ansible-playbook -i inventory.ini gather_data.yml
```

### **Run Kotaemon RAG UI**
Start the Kotaemon RAG UI in your local environment

## **Usage & Example Queries**
After starting the UI, you can ask questions such as:

**Compare my system configuration (system_config.txt) with Ubuntu STIG best practices (Ubuntu_STIG.csv). What misconfigurations do you find?**
**Are there any security misconfigurations in my system according to Ubuntu STIG guidelines?**
**List the most critical security issues and provide fixes.**


## **How It Works**
## **1.System Config Data:**
**Collected via Ansible, retrieved from the endpoint, and structured into hierarchical layers.**
**Data is hashed to track changes in future scans.**
**Uploads the Ubuntu system configuration file (system_config.txt).**

## **Security Best Practices:**
**Uses the STIG guidelines from Ubuntu_STIG.csv as a reference to detect security issues.**

## **RAG Workflow:**
**hybrid approach:**
**1.Structured Query: Retrieves exact matches from a database**
**2.Vector Search: Uses FAISS to quickly retrieve similar best practices.**
**ZySec LLM then analyzes the matched data and identifies misconfigurations.**

## **Report & Recommendations:**
**The LLM provides a detailed report with recommended fixes and a severity assessment.**
**The output can be saved in various formats (e.g., JSON, Markdown) for further action.**

![image](https://github.com/user-attachments/assets/b2872a7d-7cfe-4a89-9c18-42569c08e050)


## **Team & Contributors**
This project was developed by **CyberTech_NextTeam**:

- [Davit](https://github.com/Xmansess)  
- [Marine](https://github.com/marineharutyunyan)
- [Emelin](https://github.com/emelinghazarian)  
- **Vahagn**  
- **Meri**  




