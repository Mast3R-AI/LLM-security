# Docker AI Homelab

Welcome to the configuration and setup directory for my local AI Homelab. The main goal of this project is to build a secure, fully local Large Language Model (LLM) environment using **Docker**. 

Running models locally ensures complete data privacy and creates a safe sandbox for security testing, behavioral analysis, and daily AI-assisted tasks.

---

#### 1. Architecture & Components
The environment is entirely containerized and consists of the following core components:
* **Ollama in Docker:** The core engine used to download and serve open-source LLMs locally. Running it in an isolated container ensures the host system remains untouched.
* **Open-WebUI:** A user-friendly browser interface connected directly to the Ollama container, making it easy to interact with the models.
* **Cursor Integration:** The local Ollama instance is configured to act as a backend for the Cursor IDE. This allows for AI-assisted programming without sending any code or data to external APIs.
