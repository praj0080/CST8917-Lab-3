# 🛡️ Teams Chat Content Moderation Service – CST8917 Lab 3

## 📘 Overview

This project uses the **Logic Apps on Azure** to apply a **chat content moderation system** to **Microsoft Teams**. It is a solution that controls chat messages in real-time pushing an **email alert** in case inappropriate content is noticed. Additional integrations may be performed via optional Azure Functions and Azure Cognitive Services for Language, which offer additional filtering and analysis.

---

## 🧠 Technologies Used

- Azure Logic Apps - Moderates the moderation process.
- **Microsoft Teams Connector** - Notices the appearance of a new chat message.
- **Azure Functions** *(optional)* removes raw messages, cleans and processes raw messages.
- Azure Cognitive Services (Content Moderator) *(optional)* - Text analysis by AI.
- **Office 365 / Outlook Connector** - Sending alert e-mails to the administrator.

---

## 🗺️ Moderation Workflow Flowchart

![Moderation Flowchart](flowchart.png)  
> *Flowchart outlines how Teams messages are received, processed, analyzed, and lead to notifications.*

---

## ⚙️ Logic App Setup

### Trigger
- **Microsoft Teams (Preview) Connector**:  
  Trigger: `When new message is added in a channel.
  Is dependent upon Teams connection and the necessary Graph API rights.

### Message Processing (Optional)
- **Azure Function**:  
  - Function is used to clean the contents of the message: cut, delete symbols, lower-case.

### Message Analysis (Optional)
- **Azure Content Moderator (Text API)**:  
  - Monitors profanity, hate speech or offensive language by using NLP.
  - Returns scores are `Classification`, `Profanity`, and `Terms`.

### Conditional Logic
- **Condition Block**:  
  - ProfanityScore > 0.7, or special banned word types detected.

### Action
- **Email Notification**:
  Triggering an alarm to the administrator through outlook/Office 365 connector.
  - Contains subject and body format in predetermined format including violation details.

---

## ✅ Workflow Testing

### Test Cases
| Scenario | Expected Result |
|----------|-----------------|
| Harmless message | No alert sent |
| Profanity used (e.g., `damn`) | Email alert triggered |
| Message with banned keyword | Alert triggered |
| Azure Function error | Workflow fallback logic triggered |
| Invalid JSON | Logic App terminated gracefully |

### Steps Taken
1. They created test Teams channel and shared test messages.
2. Activated and tried Logic App manually.
3. Confirmed email warnings in outlook.
4. Viewed run history Azure portal.

---

## 🧪 Challenges and Resolutions

| Challenge | Resolution |
|----------|------------|
| Teams trigger not firing | Reconnected Teams connector and granted tenant permissions |
| Email connector failed initially | Reauthorized account, updated Logic App permissions |
| Content Moderator API returned errors | Corrected header and content type; used UTF-8 text |
| Logic App timeout with Azure Function | Set function timeout limit and optimized execution time |

---

## 🔁 Recommendations for Improvement

- Introduce attaching messages (e.g. files/images).
- Write log entries to a SharePoint list or an Azure Table Store.
- Power BI or Logic App run logs visual dashboard.
- B. Add retry policies and error handling into email connector.
- Implement sentiment analysis of identifying dangerous tones.

---

## 📹 Demo Video

🎥 [Watch Demo on YouTube](https://youtu.be/YOUR_DEMO_LINK)

---


