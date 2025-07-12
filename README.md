# 🤖 Ansible Playbook AI Generator

This project combines the power of **AI** and **Ansible** to dynamically generate playbooks based on user intent. The goal is to provide a **natural language interface** to create and execute Ansible automation tasks — such as deploying services, configuring systems, or exposing ports — using simple API calls.

---

## 🔍 Use Case: Expose Current Server IP on Port 8080

Imagine you want to deploy a simple web service and make it **accessible via your current server’s public IP on port 8080**. Instead of writing Ansible manually, you just ask:

> _“Deploy a basic HTTP server accessible on port 8080 from the current machine's IP.”_

✅ The AI will generate the appropriate playbook and optionally execute it via Ansible.

---

## 🧠 Architecture

```mermaid
flowchart TD
    A[User sends request via API] --> B[AI processes user intent]
    B --> C[Generate Ansible Playbook]
    C --> D[Save playbook to disk]
    D --> E{Auto-execute?}
    E -- Yes --> F[Run ansible-playbook]
    F --> G[Service deployed]
    E -- No --> H[Return YAML playbook]
