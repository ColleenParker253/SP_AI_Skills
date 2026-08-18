# Adding a SKILL.md File to SharePoint  
### How to Deploy a SharePoint Skill So Anyone Can Run It

## Overview
SharePoint Skills are markdown-based definitions that Copilot in SharePoint can execute. A skill becomes available to all site users once its `SKILL.md` file is stored in the correct location within the site’s **Agent Assets** library.

This guide explains how to add a `SKILL.md` file to SharePoint and ensure it is runnable by any user with standard site permissions.

---

## Required Folder Structure

A skill **must** be stored in the following path:

Agent Assets/Skills/'<skill-name>'/SKILL.md


**Important:** Copilot will not load a skill unless the `SKILL.md` file is inside its own folder under **Skills**.

---

## Method 1 — Create the Skill Using Copilot (Recommended)

Copilot can create the folder and save the skill automatically.

### Steps
1. Open **Copilot in SharePoint** from your site.
2. Paste your skill definition (the full SKILL.md content).
3. Tell Copilot: Create a skill from the following definition and save it to this site.

4. Copilot will:
- Create the folder  
- Save `SKILL.md`  
- Register the skill  

### Running the Skill
In Copilot chat: Run <skill-name>

## Method 2 — Upload SKILL.md Manually

Use this method when you already have a prepared `SKILL.md` file.

### Steps
1. Go to your SharePoint site.
2. Open the **Agent Assets** document library.
3. Open the **Skills** folder.
4. Create a new folder named after your skill: <skill-name>
5. Upload `SKILL.md` into that folder.
6. Confirm the skill is recognized by Copilot: --agent-skills

---

## Permissions Model

SharePoint Skills run under the permissions of the user who invokes them.

- **View permission** → User can *run* skills  
- **Edit permission** → User can *create or modify* skills  

No elevated permissions or special configuration is required.

To restrict who can create skills:
- Break inheritance on **Agent Assets**
- Limit edit permissions to site owners or a governance group

---
## Verifying the Skill

Users can confirm the skill is available by running: --agent-skills


If the `SKILL.md` file is stored correctly, the skill will appear in the list.

---

## Common Mistakes to Avoid

- **Placing SKILL.md directly in `/Agent Assets/Skills/`**  
  - Must be inside `/Skills/<skill-name>/SKILL.md`

- **Using unsupported tools in the skill**  
  - Run `--agenttools` to check available tools

- **Expecting skills to run with elevated permissions**  
  - Skills run with the permissions of the user invoking them

---

## Summary

To add a SKILL.md file so anyone can run it:

1. Store it in: Agent Assets → Skills → <skill-name> → SKILL.md
2. Ensure users have **View** permission.
3. Run the skill by name in Copilot chat.
4. Use `--agent-skills` to verify it’s registered.

Your skill is now fully deployed and ready for use.


