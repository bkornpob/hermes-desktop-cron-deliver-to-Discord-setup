title: Hermes-Desktop Local Ollama Setup Guide

summary: A streamlined, private-first workflow for running Hermes-Desktop on Windows 11 with local Ollama models.

---

machine: windows 11 host, nvidia gpu

scenario: setup hermes-desktop, and hook to local ollama models

feats: free, private

---

### steps

#### 0. System Verification
- [ ] `nvidia-smi` 
	if command not found, install latest drivers from [NVIDIA website](https://www.nvidia.com/Download/index.aspx).
- [ ] `ollama --version` 
	Download and install from [ollama.com](https://ollama.com/download/windows).
- [ ] `ollama serve`
- [ ] `Invoke-RestMethod -Uri http://localhost:11434/api/tags`
	or `curl`.
- [ ] `ollama list`
	- [ ] proceeding, this guide assumes a model name `sec-lab:latest` exists via `ollama list`. *If missing:* Follow the "Ollama Baking Model" section below.

#### 1. hermes-desktop install
- [ ] **Download:** Get the latest `.exe` from [Releases](https://github.com/fathah/hermes-desktop/releases/).
- [ ] **Install:** Run the NSIS installer.
- [ ] **Dependencies:** look for `~/.hermes`; if not, runs the official Hermes installer with dependency resolution (Git, uv, Python 3.11+; see [Official Docs](https://hermes-agent.nousresearch.com/docs)).
- [ ] **Open:** Launch the Hermes-Desktop application.

#### 2. hooking local Ollama models to hermes-desktop
- [ ] **Providers tab:** fill this
	- [ ] Provider: Local/Custom
	- [ ] Model: sec-lab:latest
	- [ ] Base URL: http://localhost:11434/v1
- [ ] **Models tab:** click 'Add Model' and fill this
	- [ ] Display Name: llama3.2:3b_sec-lab
	- [ ] Provider: Local/Custom
	- [ ] Model ID: sec-lab:latest
	- [ ] Base URL (optional): http://localhost:11434/v1
	- [ ] API Key (optional): `[leave empty]`
- **Manual Config override (optional):** If UI fails to connect, edit `~\.hermes\config.yaml` in your preferred editor:
```yaml
provider: "ollama"
base_url: "http://127.0.0.1:11434/v1"
model: "sec-lab:latest"
```
- [ ] **Chat tab:** select the model and start chatting

---

### ollama baking model
- [ ] `ollama pull llama3.2:3b` >>> browse [Ollama Library](https://www.ollama.com/library) for more models
- [ ] Create `Modelfile`: (example)
```powershell
# In PowerShell:
@"
FROM llama3.2:3b
SYSTEM "You are an AI security red team specialist. Focus on: Prompt injection attacks, Jailbreak techniques, LLM vulnerabilities, Adversarial testing."
PARAMETER temperature 0.8
PARAMETER top_p 0.95
PARAMETER num_ctx 4096
"@ | Out-File -FilePath Modelfile -Encoding utf8
```
- [ ] `ollama create sec-lab -f Modelfile`
- [ ] `ollama list` >>> verify `sec-lab:latest` appears
