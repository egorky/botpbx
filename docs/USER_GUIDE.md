# BotPBX User Guide

Welcome to BotPBX! This guide explains how to configure, use, and leverage the features of your AI-powered PBX system.

## Table of Contents
1. [Overview](#overview)
2. [Configuration](#configuration)
3. [Accessing the Interface](#accessing-the-interface)
4. [Features](#features)
   - [Inbound Routing](#inbound-routing)
   - [AI Agents](#ai-agents)
   - [IVR Menus](#ivr-menus)
   - [Queues & Ring Groups](#queues--ring-groups)
   - [Extensions](#extensions)
   - [Campaigns](#campaigns)
5. [Telegram Bot](#telegram-bot)

---

## Overview

BotPBX is a modern PBX system that integrates traditional VoIP features (extensions, queues, IVR) with cutting-edge AI capabilities. It allows you to create AI voice agents that can answer calls, qualify leads, and handle support queries using OpenAI Realtime API or ElevenLabs.

## Configuration

### Prerequisites
-   A server with Docker or Node.js >= 23.0.0
-   PostgreSQL database
-   Asterisk (for VoIP switching)
-   SIP Trunk provider (e.g., Twilio, Telnyx)
-   OpenAI API Key (for AI Agents)

### Environment Setup
Create a `.env` file in the root directory with the following keys:

```bash
# Database
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=yourpassword
DB_NAME=botpbx

# Asterisk
ASTERISK_AMI_HOST=localhost
ASTERISK_AMI_PORT=5038
ASTERISK_AMI_USER=admin
ASTERISK_AMI_SECRET=secret

# AI Providers
OPENAI_API_KEY=sk-...
ELEVENLABS_API_KEY=...

# Web Admin
JWT_SECRET=somelongrandomstring
ADMIN_USERNAME=admin
ADMIN_PASSWORD=securepassword
```

### Installation
1.  Install dependencies: `npm install`
2.  Run migrations: `npm start` (migrations run automatically on startup)
3.  Build the project: `npm run build`

## Accessing the Interface

Once the server is running, you can access the web interface:

-   **URL:** `http://<your-server-ip>:3000` (or the configured domain)
-   **Default Login:** `admin` / `admin` (Change this immediately after logging in!)

## Features

### Inbound Routing
Configure what happens when someone calls your phone number (DID).
-   Go to **Routes** > **Inbound**.
-   **DID:** Enter your phone number (e.g., `+1234567890`) or `_` for a catch-all route.
-   **Target Type:** Choose where to route the call:
    -   **IVR Menu:** Send to an auto-attendant.
    -   **Extension:** Ring a specific phone.
    -   **Queue:** Send to a call center queue.
    -   **AI Agent:** Route directly to an AI voice bot.

### AI Agents
Create intelligent voice bots that talk naturally.
-   Go to **AI Agents**.
-   Click **Create Agent**.
-   **System Prompt:** Define the agent's personality (e.g., "You are a helpful receptionist...").
-   **Voice:** Select a voice (OpenAI Alloy, Echo, etc.).
-   **Functions:** Enable capabilities like transferring calls or sending SMS.

### IVR Menus
Build "Press 1 for Sales" menus.
-   Go to **IVR**.
-   Create a menu and add options (Keys 0-9, *, #).
-   Assign actions to each key (e.g., Transfer to Extension 101).

### Queues & Ring Groups
-   **Queues:** Callers wait in line with hold music until an agent is available. Great for support teams.
-   **Ring Groups:** Ring multiple phones at once (or in order). Great for small teams.

### Extensions
Manage SIP extensions for your physical phones or softphones (Zoiper, MicroSIP).
-   Go to **Extensions**.
-   Create an extension (e.g., 1001).
-   Use the generated password to configure your SIP client.

### Campaigns
Run outbound dialing campaigns.
-   Upload a CSV of contacts.
-   Select an AI Agent or IVR to handle the call when answered.
-   The system dials automatically and connects the call.

## Telegram Bot
You can manage the system via Telegram.
1.  Start a chat with your bot.
2.  Use `/start` to authenticate.
3.  Commands:
    -   `/status`: Check system health.
    -   `/calls`: See active calls.
    -   `/agent <id>`: Control AI agents.
