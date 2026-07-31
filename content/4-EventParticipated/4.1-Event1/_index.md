---
title: "Event 1: Agentic AI Build Week & Solution Architecture Showcase"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>4.1 </b>"
---

# Event Report: Agentic AI Build Week & Solution Architecture Showcase

## Event Overview

The event was a showcase and demo session as part of the **Agentic AI Build Week** – a week-long hackathon where teams built AI-powered solutions on AWS. Each team presented their products, shared their build journey, architecture, cost analysis, and key lessons learned.

## Event Objectives

- Showcase real-world AI solutions built on AWS in a short timeframe.
- Share architecture design processes, cost optimization strategies, and service selection rationale.
- Promote **Solution Architecture** and **AI-native development** mindsets.
- Foster learning and exchange among participants and organizers.

## Featured Projects

### 1. Signal Scout – Detecting Corporate Strategic Changes

**Team:** Lê Tấn Lực, Đỗ Hoàng Hiếu, Triệu Quốc Hào, Nguyễn Văn Duy Khiêm, Nguyễn Công Minh, Nguyễn Trần Minh Quân

**Problem:** Corporate strategy teams often struggle to detect early signals of competitive or market changes.

**Solution:** Signal Scout is a platform that connects scattered signals from corporate and market data, building a clear narrative to support strategic decisions (Maintain, Adapt, Accelerate).

**Architecture:** Uses AWS for data processing and AI, LangFuse for monitoring, Apify for data collection, TinyFish for analysis.

**Key Highlight:** Focus on **transparency** and **verifiability** – every conclusion is supported by evidence.

---

### 2. Solution Architect Professional Native App

**Team:** Phạm Tiến Thuận Phát, Huỳnh Hoàng Long, Lê Minh Nghĩa, Trần Đại Vĩ, Nguyễn An

**Problem:** Solution architects spend too much time reading requirements, drafting architectures, drawing diagrams, and estimating costs.

**Solution:** An AI-native app that automates:
- Natural language requirement analysis
- Hybrid-cloud architecture drafting
- Draw.io diagram generation with official AWS icons
- AWS cost estimation for ap-southeast-1
- Recommendations, assumptions, and gap identification
- Refinement via chat sidebar with custom instructions

**Impact:** Reduces time from reading BRD/PRD to initial architecture from hours to minutes, eliminating repetitive manual work.

---

### 3. 3KA – Hackathon Journey

**Team:** Huỳnh An Khương, Nguyễn Quốc Huy, Ngô Quang Khôi, Hoàng Lê Thành Đức, Đặng Nguyễn Phước Lộc, Đặng Trường Hưng

**Story:** The presentation tells the team's emotional journey through the hackathon – from **DOUBT**, through **FLOW**, to **PRIDE** in their achievement.

**Key Highlight:** Emphasis on teamwork, perseverance, and adaptability when working with new technologies under time constraints.

---

### 4. OneTeam – AI-Powered Conversation Ordering

**Team:** Anh Duy, Tran Dong, Doan Trung, Minh Viet, Anshul Roy

**The Trigger:**
- Customers increasingly expect fast, convenient, and personalized ordering experiences.
- Traditional ordering systems often require manual steps, causing friction and reducing user experience.

**The Problem:**
- Current ordering processes are complex, requiring users to fill in many fields.
- Lack of natural language understanding forces users to follow rigid structures.
- No ability to suggest or customize based on conversation context.

**The Solution:**
- **OneTeam** is an AI-powered conversational ordering solution that allows users to interact naturally.
- The app understands and processes complex requests like modifying orders, adding items, or asking about promotions.
- Integrates with existing backend systems for order processing, payment, and confirmation.
- Uses AI to suggest items based on preferences and order history.

**Architecture:**
- Uses **Amazon Lex** or similar AI services for natural language processing.
- **AWS Lambda** for business logic processing.
- **Amazon API Gateway** as the API layer.
- Database for order and user information storage.

**Key Highlight:**
- Smooth user experience, like chatting with a real sales assistant.
- Automates ordering process, reducing manual errors.
- Highly scalable and customizable.

---

## Key Highlights

| Project | Key Technologies | Core Value |
|---------|-----------------|------------|
| Signal Scout | AWS, LangFuse, Apify, AI/ML | Early detection, evidence-based decisions |
| SA Professional Native App | AWS, AI, Draw.io integration | Architecture automation, time savings |
| 3KA | AWS, Full-stack development | Hackathon spirit, teamwork |
| OneTeam | AWS, Amazon Lex, Lambda, API Gateway | AI-powered conversational ordering, user experience |

---

## Lessons Learned

### 1. Solution Architecture Mindset
- Always start from the **business domain**, not the technology.
- Every architecture should include **cost estimation** and clear **assumptions**.
- **AI-native apps** are changing how architects work.

### 2. Cost Optimization is Part of Architecture
- All teams presented **Cost Analysis** sections, showing cost is a critical factor.
- Choosing the right service (serverless vs container vs VM) significantly impacts operational costs.

### 3. The Journey Matters as Much as the Result
- Lesson from team 3KA: **perseverance** and **teamwork** are key to overcoming challenges.
- **DOUBT → FLOW → PRIDE** is a very real emotional journey in tech projects.

### 4. Applying AI to Daily Work
- AI tools can assist from **requirement analysis** → **design** → **deployment** → **maintenance**.
- **Amazon Q Developer** and similar tools are becoming valuable assistants for engineers and architects.

### 5. AI in Customer Experience
- OneTeam shows how AI can revolutionize how customers interact with businesses.
- **Conversational AI** is not just a trend but becoming a user expectation.
- Integrating AI into products improves both experience and operational efficiency.

---

## Applying to Work

- ✅ Apply **domain-driven thinking** when designing architecture for the ML on AWS project.
- ✅ Integrate **cost estimation** into the design process.
- ✅ Explore **Amazon Q Developer** to accelerate development.
- ✅ Share the learning journey to inspire teammates.
- ✅ Research **conversational AI** applications in future products.

---

## Event Photos

*(Insert event photos here)*

![Event Photo 1](/static/images/event1.webp)
![Event Photo 2](/static/images/event2.webp)

---

## Personal Reflection

This event was a valuable opportunity to see **how real-world AI projects are built and operated on AWS**. I was particularly impressed by:

- How **Signal Scout** connects scattered signals into a strategic narrative – a practical application of AI in business.
- The **SA Professional Native App** shows how AI can completely transform a solution architect's workflow.
- The emotional journey of team **3KA** reminded me of the value of persistence and teamwork.
- The **OneTeam** project shows the immense potential of AI in improving customer experience – a direction I want to explore further.

I realized that building a system is not just about technology, but also about **telling a story** – from the customer's problem, to the solution, to the value delivered. This is an important lesson for my development journey.
