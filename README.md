title: hermes-desktop cron deliver to Discord setup

summary: set up a cron job (Schedules) on hermes-agent as a local private Discord bot on Windows 11 with NVIDIA GPU and Ollama.

---

machine: windows 11 host, nvidia gpu; hermes-agent; hook to local ollama models; Discord user account

feats: free, private, remote accessible, shareable, automation

related:
- hermest-agent Scheduled Tasks (Cron) ... https://hermes-agent.nousresearch.com/docs/user-guide/features/cron
- hermes-desktop local Ollama setup guide ... https://github.com/bkornpob/Hermes-Desktop-Local-Ollama-Setup-Guide
- hermes-desktop Discord bot setup ... https://github.com/bkornpob/hermes-desktop-discord-bot-setup

---

## 🎛️ Goal

Schedule a hermes-agent cron job that sends a message to a Discord channel.

***

## 🧪 Preconditions

- [ ] `hermes` CLI is functional.
	guide: https://github.com/bkornpob/Hermes-Desktop-Local-Ollama-Setup-Guide  
- [ ] Discord bot hooked to hermes-agent is functional.
	guide: https://github.com/bkornpob/hermes-desktop-discord-bot-setup  
- [ ] in Discord, run `/sethome` for the output location

---

## 🧵 Steps: from zero → ticking Discord bot

- [ ] access to `hermes` cli
		install hermes-agent vis hermes-desktop hooked with local Ollama models ... 
		https://github.com/bkornpob/Hermes-Desktop-Local-Ollama-Setup-Guide
- [ ] `/cron add "every 1 minute" "send a test message with current datetime" {--deliver discord}`
		setup hermes-agent as Discord bot ...
		https://github.com/bkornpob/hermes-desktop-discord-bot-setup
- [ ] `/cron list` ... check added task and `<job_id>`
- [ ] `/cron run <job_id>` ... to run one-shot test
- [ ] verify output `~/.hermes/cron/output/<job_id>/`
- [ ] edit task:
	- [ ] `/cron pause <job_id>` ... to pause before edit (toggle off)
	- [ ] to edit the task
		- [ ] `/cron edit --key {value,"value"}` OR
		- [ ] edit `~/.hermes/cron/jobs.json`
	- [ ] `/cron run <job_id>` ... then verify output, iterate ... until happy
		- [ ] `/cron remove <job_id>` ... to remove the task and start over ... if needed
	- [ ] `/cron resume <job_id>` ... toggle on

---

## ⏱️ hermes-agent Scheduled Tasks (Cron)
https://hermes-agent.nousresearch.com/docs/user-guide/features/cron

**Function:** Hermes Cron schedules one-shot or recurring tasks from plain language or cron expressions, manages them through one unified `cronjob` interface, and can pause, resume, edit, trigger, or remove jobs. It runs each job in a fresh agent session, supports attached skills, can deliver to origin/local/Discord/etc., and can also run in no-agent script-only mode.

**Useful behavior:** 
- Jobs default to isolated sessions with no memory of prior runs, so prompts should be self-contained. 
- The gateway daemon checks cron every 60 seconds, 
- config: `~/.hermes/cron/jobs.json`
- output: `~/.hermes/cron/output/{job_id}/`

**Usage:**
![[Pasted image 20260522225603.png]]
![[Pasted image 20260522225231.png]]
![[Pasted image 20260522225603.png]]
  /cron
  /cron list
  /cron add "every 2h" "check server status"
  /cron edit <job_id> --key1 "value1" --key2 "value2"
  /cron pause <job_id>
  /cron resume <job_id>
  /cron run <job_id>
  /cron remove <job_id>
  
**Config params:** 
path `~/.hermes/cron/jobs.json`
```json
{
  "jobs": [
    {
      "id": "0ccc7281ec5e",
      "name": "send a test message with current datetime",
      "prompt": "send a test message with current datetime",
      "skills": [],
      "skill": null,
      "model": null,
      "provider": null,
      "base_url": null,
      "script": null,
      "no_agent": false,
      "context_from": null,
      "schedule": {
        "kind": "interval",
        "minutes": 1,
        "display": "every 1m"
      },
      "schedule_display": "every 1m",
      "repeat": {
        "times": null,
        "completed": 0
      },
      "enabled": true,
      "state": "scheduled",
      "paused_at": null,
      "paused_reason": null,
      "created_at": "2026-05-22T12:02:53.399153+07:00",
      "next_run_at": "2026-05-22T23:15:05.988719+07:00",
      "last_run_at": null,
      "last_status": null,
      "last_error": null,
      "last_delivery_error": null,
      "deliver": "discord",
      "origin": null,
      "enabled_toolsets": null,
      "workdir": null,
      "profile": null
    }
  ],
  "updated_at": "2026-05-22T23:14:05.989282+07:00"
}
```

---
### hermes-desktop Schedules limitations

![[Pasted image 20260522220658.png]]

![[Pasted image 20260522220822.png]]

❌ {add, edit, run}
✅ {list, pause, resume, remove}
