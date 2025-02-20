# CyberTech_NextTeam

## ** Using Large Language Models (LLMs) with RAG to Detect Infrastructure Misconfigurations and Suggest fixes**

## ** Overview**
This project demonstrates how to use **RAG (Retrieval-Augmented Generation) + ZySec LLM** to **detect misconfigurations** in infrastructure settings based on **Ubuntu STIG security best practices**.  

**Built on:**  
- [Kotaemon](https://github.com/kotaemon) – An open-source, clean & customizable RAG UI for chatting with documents.  
- **ZySec LLM** ([Hugging Face Model](https://huggingface.co/koesn/ZySec-7B-v1-GGUF)) – A security-focused LLM for analyzing configurations.  

**Features:**  
**Compares system configurations against STIG best practices.**  
**Detects security misconfigurations in real-time.**  
**Provides fixes & recommendations for compliance.**  
**Works with Ubuntu STIG benchmarks for Canonical Ubuntu 22.04 LTS.**  

---

## **Project Structure**
---
│── /configs
│   ├── system_config.txt   # Extracted system configuration for Ubuntu
│   ├── Ubuntu_STIG.csv     # STIG security best practices for Ubuntu 22.04
│── /models
│   ├── zysec-7b-v1.gguf   # ZySec LLM model file
│── /rag_ui
│   ├── kotaemon-ui        # Kotaemon RAG-based UI for chat interface
│── README.md

---

## **Setup Instructions**

### **Clone the Repository**
```bash
git clone https://github.com/your_username/your_repo.git
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


### **Run Kotaemon RAG UI**
Start the Kotaemon RAG UI in your local environment

## **Usage & Example Queries**
After starting the UI, you can ask questions such as:

**Compare my system configuration (system_config.txt) with Ubuntu STIG best practices (Ubuntu_STIG.csv). What misconfigurations do you find?**
**Are there any security misconfigurations in my system according to Ubuntu STIG guidelines?**
**List the most critical security issues and provide fixes.**


## **How It Works**
## **1.System Config Data:**
**Uploads the Ubuntu system configuration file (system_config.txt).**

## **Security Best Practices:**
**Uses the STIG guidelines from Ubuntu_STIG.csv as a reference to detect security issues.**

## **RAG Workflow:**
**The system retrieves relevant security rules using a hybrid approach:**
### **Structured Query: Fetches data from MongoDB (or local storage) for exact matches.**
### **Vector Search: Uses FAISS to quickly retrieve similar best practices.88
**ZySec LLM then analyzes the matched data and identifies misconfigurations.**

## **Report & Recommendations:**
**The LLM provides a detailed report with recommended fixes and a severity assessment.**
**The output can be saved in various formats (e.g., JSON, Markdown) for further action.**

![image](https://github.com/user-attachments/assets/b2872a7d-7cfe-4a89-9c18-42569c08e050)






