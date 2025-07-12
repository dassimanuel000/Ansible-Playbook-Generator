
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
````

---

## 💡 Features

* ✨ Natural language-to-Playbook conversion
* 🧠 AI-powered prompt-to-YAML generation (OpenAI, LLM, or local model)
* 🛠️ Supports common deployment use cases
* ⚙️ Optional auto-deployment via `ansible-playbook`
* 📦 API-based interaction (e.g., `/generate-playbook`, `/execute`)

---

## 🧪 Tech Stack

* **Python** – Backend logic and API
* **FastAPI / Flask** – Lightweight REST API
* **OpenAI / LLM** – Text generation engine
* **Ansible** – Automation engine
* **Docker** – Containerized API service
* **ngrok / Serveo** – For exposing local dev environments (optional)

---

## 🧾 Example API Usage

### Request

```http
POST /generate-playbook
Content-Type: application/json

{
  "request": "Deploy a service accessible from this server's public IP on port 8080"
}
```

### Response

```yaml
- name: Install and start a web server on port 8080
  hosts: localhost
  become: true
  tasks:
    - name: Install Python HTTP server package
      apt:
        name: python3
        state: present

    - name: Start HTTP server on port 8080
      shell: nohup python3 -m http.server 8080 &
      args:
        chdir: /var/www/html
```

---

## ⚙️ Sample Python Endpoint

```python
from fastapi import FastAPI, Request
import openai

app = FastAPI()

@app.post("/generate-playbook")
async def generate_playbook(req: Request):
    body = await req.json()
    prompt = f"Write an Ansible playbook to: {body['request']}"
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    playbook = response.choices[0].message["content"]
    return {"playbook": playbook}
```

---

## 🔐 Security Notice

Running arbitrary playbooks automatically can be **dangerous**. You should:

* Sanitize input
* Limit AI-generated tasks to a safe set of actions
* Optionally disable auto-execution by default

---

## 🧪 Local Setup

```bash
# Clone repo
git clone https://github.com/yourname/ansible-ai-generator.git
cd ansible-ai-generator

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install requirements
pip install -r requirements.txt

# Run API
uvicorn main:app --reload
```

---

## 🧰 Dependencies

* `ansible`
* `openai` (or other LLM provider)
* `fastapi` or `flask`
* `uvicorn` (if using FastAPI)

---

## 📌 Optional Enhancements

* 🔁 History of generated playbooks
* 📤 Export to file/download
* 🔧 Execute on remote inventory
* 👥 User authentication & rate limiting
* 🌐 Web frontend for non-technical users

---

## 📫 Contact

Maintainer: \dassimanuel000
🌐 [GitHub](https://github.com/dassimanuel000)

---

## 📜 License

MIT License — feel free to use, fork, and contribute.


