# AI-Driven Infrastructure Misconfiguration Detection with RAG and RLHF

## Overview
This repository implements an **AI-powered system** that detects **infrastructure misconfigurations** and suggests fixes using **Large Language Models (LLMs) with Retrieval-Augmented Generation (RAG)**. We enhance accuracy over time by integrating **user feedback** through **short-term retrieval, real-time feedback storage, and long-term RLHF
fine-tuning**.

📌 **Graphical Representation of the AI System:**  
[🔗 View the Excalidraw Diagram](https://excalidraw.com/#room=7ca328fea12a23472798,fRy6cW96Ks_Dpd0xOBUe_g)

---

## **System Architecture**
The system follows **three progressive approaches** to improve response quality:

### **1. Short-Term Retrieval (Basic RAG Approach)**
**How it Works:**
- Infrastructure data is collected and stored in **MongoDB** (structured storage).
- Embeddings are generated and stored in **FAISS** (vector similarity search).
- RAG retrieves relevant infrastructure data + best practices (e.g., **STIG, CIS**).
- LLM generates **misconfiguration fixes** based on retrieved data.

**Why MongoDB + FAISS?**
- **MongoDB** enables structured queries (e.g., filtering based on system type).
- **FAISS** provides fast **vector-based similarity search**.
![image](https://github.com/user-attachments/assets/efec9ff9-f33d-4a84-92de-d05753a9c698)

---

### **2. Real-Time Feedback Storage (User Feedback Integration)**
**How it Works:**
- User interactions (e.g., feedback on past responses) are stored in **MongoDB**.
- Useful feedback is **converted into embeddings** and stored in **FAISS**.
- RAG retrieves **both infrastructure data + past user feedback**.
- LLM **generates better responses** by combining **STIG rules + user feedback**.

**How Feedback is Retrieved?**
- **Hybrid Search Approach:**
  - **Step 1**: Use **MongoDB full-text search** to find relevant past queries.
  - **Step 2**: Apply **vector similarity search** in FAISS for refinement.
  - **Step 3**: Combine **keyword matching + semantic similarity** for retrieval.
![image](https://github.com/user-attachments/assets/9f79dbf8-d564-4c76-94ad-21e6b494b128)

---

### **3. Long-Term Learning with RLHF (Reinforcement Learning from Human Feedback)**
**How it Works:**
- User feedback is **used to fine-tune both RAG’s retrieval system and the LLM**.
- **Two Fine-Tuning Processes:**
  1. **Fine-Tune RAG’s Retrieval Mechanism (RLHF)**
     - A **reward model** is trained to **score retrieved documents**.
     - Over time, RAG learns which retrievals **led to useful responses**.
     - Fine-tune **retrieval layers** using **PPO (Proximal Policy Optimization)**.

  2. **Fine-Tune the LLM (ZySec-7B) with RLHF**
     - If the LLM’s reasoning is flawed, even perfect retrieval won’t help.
     - RLHF is used to **fine-tune the LLM** based on **user preferences**.
     - **Implicit feedback tracking**: Did the user copy the response? Ask for a rephrase?

 **How RLHF Works in this System?**
1. A **reward model** assigns **scores to retrieved documents**.
2. Retrieval ranking is improved using **RLHF with PPO**.
3. **LLM is fine-tuned** to generate **better responses based on implicit feedback**.
![image](https://github.com/user-attachments/assets/991efc30-bce6-4d1a-98a9-cea54011a15b)

---

