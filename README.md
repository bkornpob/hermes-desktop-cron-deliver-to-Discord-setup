title: Hermes-Desktop Discord Bot Setup Guide

summary: set up hernes-agent as a local private Discord bot on Windows 11 with NVIDIA GPU and Ollama.

---

machine: windows 11 host, nvidia gpu; hermes-desktop; hook to local ollama models; Discord user account

feats: free, private, remote accessible, shareable

related:
- hermes agent setup with discord (complete guide) ... https://www.youtube.com/watch?v=mVHXwlSMQlQ
- hermes desktop local ollama setup guide ... https://github.com/bkornpob/Hermes-Desktop-Local-Ollama-Setup-Guide

---

### steps

#### 0. System Verification
- [ ] **Open:** launch the hermes-desktop application.
- [ ] **Chat:** select a model and verify normal behaviour of the hermes-agent in hermes-desktop by chatting with the agent inside hermes-desktop.
- [ ] **Discord account:** confirm that you have a Discord USER account available to start hosting.
- [ ] **Discord channel:** confirm that you have a Discord channel where you can invite the bot into.
	- [ ] save the channel ID (right click on channel name > Copy Channel ID)
	- if missing, check User Settings > Developer > toggle on Developer Mode

#### 1. hooking hermes-agent to a Discord channel
- [ ] **Access Discord Developer Portal with your USER account:** https://discord.com/developers/applications
- [ ] **Create new applications:**
	- [ ] fill in 'General Information' (e.g., name and profile image)
	- [ ] set bot configs in 'Bot' tab ... fill in
		- [ ] username (BOTNAME)
		- [ ] toggle on 'Public Bot'
		- [ ] toggle on 'Presence Intent'
		- [ ] toggle on 'Server Members Intent'
		- [ ] toggle on 'Message Content Intent'
		- [ ] toggle on 'Administrator' in Bot Permissions > General Permissions
		- [ ] click Save
		- [ ] click 'View Token' > confirm to Reset Token > save your new token
- [ ] **Installation tab:**
	- [ ] toggle on 'User Install'
	- [ ] toggle on 'Guild Install'
	- [ ] add 'bot' to Default Install Settings > Guild Install
	- [ ] save the 'Install Link' (given Discord Provided Link selected)
![[Pasted image 20260521012513.png]]
- [ ] **Verify values for the next step:**
	- [ ] Discord Bot Token < Bot tab in discord.com/developers/applications
	- [ ] Discord Install Link < Installation tab
	- [ ] Discord Allowed Channel ID < right click on discord channel and save Channel ID

#### 2. Gateway setup for Discord bot on hermes-desktop
- [ ] **Gateway tab:** 
	- [ ] verify 'Status' as 'Running'
	- [ ] toggle on for Discord platform
		- [ ] add Discord Bot Token
		- [ ] add Discord Allowed Channel ID
- [ ] open the Discord Install Link in a browser
	- [ ] select 'Add to Server' > choose the corresponding server to the Discord Allowed Channel ID
- [ ] verify the bot is online (with green-dot) in the channel
- [ ] (option) use '/sethome'
- [ ] chat with the bot in the channel by using '@BOTNAME who is ZADDY?' for example
