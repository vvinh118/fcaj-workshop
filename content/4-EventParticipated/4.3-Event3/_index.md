---
title: "Event 3: AWS FCAJ Agent Forge - Deep Dive Day 2"
date: 2026-08-08
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Report on “AWS FCAJ Agent Forge - Deep Dive Day 2”

### General Information
- **Event Name:** AWS FIRST CLOUD AI JOURNEY - AGENT FORGE DEEP DIVE.
- **Date & Time:** 09:00 AM - 12:00 PM, Saturday, August 08, 2026.
- **Location:** 26th Floor, Bitexco Financial Tower.
- **Speakers:** Mr. Nghia Tran (Agentic SA) and Mr. Anh Pham (Cloud Consultant, G-AsiaPacific Vietnam).
- **Role:** Attendee.

### Event Overview
The Agent Forge Deep Dive Day 2 event focused deeply on the theory and practical application of building production-ready Agentic systems using Amazon Bedrock AgentCore. The well-structured program was divided into two main parts: theoretical concepts on core memory architecture presented by Mr. Nghia Tran, and a direct Hands-on Lab guided by Mr. Anh Pham.

### In-Depth Content

#### 1. AgentCore Memory Architecture (Presented by: Nghia Tran)
The Agent's memory system is designed into distinct streams, connected via the Automatic Memory Extraction Module:
- **Short-term Memory (STM):** Comprises Chat Messages and Session State. This architecture specifically supports Branching mechanisms to organize advanced event flows, which is highly useful for scenarios like message editing or alternative conversation branches.
- **Long-term Memory (LTM):** Supports various storage strategies, including:
  - *Summary:* Generates condensed representations of content and interaction outcomes.
  - *User Preferences:* Stores and learns from recurring patterns in user behavior.
  - *Semantic & Episodic:* Maintains domain-specific knowledge and captures decisions to improve the Agent's performance.

**Optimization using Namespaces & Metadata:**
- Namespaces help logically group and organize long-term memory using a hierarchical format (e.g., `/`), supporting dynamic variables such as `{actorId}` and `{strategyId}`.
- While Namespaces are used to isolate subjects, Metadata defines the scope within that namespace and allows the configuration of indexed Keys to pre-filter semantic search results.

#### 2. Hands-on Lab (Guided by: Anh Pham)
The practical session was deployed directly on the AWS Lab environment, allowing attendees to interact directly with the tools:
- Practiced adding memory configurations to personalize AI behavior.
- Utilized AgentCore Evaluations to track and evaluate performance.
- Explored Observability features to monitor processing flows and worked with Harness tools within the AgentCore ecosystem.

### Experience and Knowledge Gained

The event was highly professional and held at Bitexco. The speakers delivered logical knowledge, perfectly combining deep theory with a practical Lab environment, making it easy for attendees to master the latest Generative AI technologies.

The course provided a solid foundation on how to design memory for modern AI Agents. The clear separation of STM and LTM, combined with the partitioning technique using Namespaces, helps optimize the LLM's ability to maintain context without consuming excessive tokens.

### Application to Real-world Project (Cloud Finance Platform)

AWS FCAJ Agent Forge opened up new perspectives for me to refine my intelligent Personal Finance Management system:
- **Optimizing the AI Financial Assistant:** Applying the LTM (*User Preferences*) strategy so the chatbot can automatically remember and learn from the familiar spending behavior patterns of each user.
- **NLP Data Security and Authorization:** Applying the *Namespaces* structure combined with identifier variables (like `{actorId}`) to absolutely isolate the transaction history data and conversational context of each individual, ensuring the highest level of information security.

### Event Gallery

![event 3](event3.jpg)