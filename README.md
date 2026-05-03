# AI-Powered-Business-Assessment-System-NMCD-Inc.

Production-deployed AI automation system for NMCD Inc. automating personalized founder readiness reports using GoHighLevel, Make.com, and OpenAI GPT-4o-mini.

# AI-Powered Founder Readiness Assessment System

A graduate capstone project built at Montclair State University, Feliciano School of Business (INFO588 Analytics Capstone, Spring 2026).

This system automates founder readiness assessment using a CRM-integrated AI pipeline. It takes survey responses as input and delivers a personalized, AI-generated readiness report to each user within seconds of submission.

---

## What It Does

Founders complete a diagnostic assessment inside a CRM platform. On submission, the system:

1. Captures the survey response via webhook
2. Sends the structured data to an AI model
3. Generates a personalized Business Readiness Report
4. Emails the report directly to the founder

No manual review. No delay. The entire pipeline runs automatically from form submission to inbox delivery.

---

## Architecture

```
GHL Survey Submission
        |
        v
GHL Workflow (W2) -- Webhook Trigger
        |
        v
Make.com Scenario
        |
        |-- Module 1: Custom Webhook (receives GHL payload)
        |
        |-- Module 2: OpenAI Generate a Completion (gpt-4o-mini)
        |
        |-- Module 3: Gmail Send an Email (delivers report)
```

The architecture consolidates the full pipeline inside a single Make.com scenario. An earlier version distributed logic across separate tools. After further research, I rebuilt it into one unified flow, which reduced complexity and made the system easier to maintain and debug.

---

## Tech Stack

| Layer | Tool |
|---|---|
| CRM and workflow automation | GoHighLevel (GHL) |
| Integration and orchestration | Make.com |
| AI report generation | OpenAI API (gpt-4o-mini) |
| Email delivery | Gmail via Make.com |
| Fallback automation | Zapier (evaluated, not deployed) |

---

## Key Technical Decisions

### Webhook field mapping

GHL surveys generate Unique Keys automatically. These keys follow a long concatenated format such as `contact.contacthow_prepared_do_you_feel_to_present_to_investors_m6k_copy` and cannot be edited inside the survey builder. I mapped each key to the correct merge field in the GHL webhook payload so Make.com could parse and pass them accurately to the OpenAI prompt.

### Prompt engineering

The OpenAI module uses a structured prompt that receives survey field values and generates a Business Readiness Report tailored to the founder's responses. The model is gpt-4o-mini, selected for speed and cost efficiency at the assessment volume this system handles.

### Scoring logic architecture

I evaluated using GHL native If/Else branching for the Funding Readiness Scorecard scoring logic. GHL If/Else creates separate END nodes with no merge point, which makes multi-variable weighted scoring impractical inside the workflow builder. The correct architecture routes scoring calculations to Make.com, where logic can be applied across all variables before returning a result.

The scoring model is based on the Futurpreneur weighted scoring framework, adapted for this system.

### Platform consolidation

The first working version of the intelligence layer used GHL, Make.com, and the OpenAI API as loosely connected components. After reviewing the architecture, I identified redundant handoffs and rebuilt the pipeline to consolidate all processing inside a single Make.com scenario. This reduced the number of failure points and made the system significantly easier to troubleshoot.

---

## GHL Workflow Configuration

**Workflow name:** W2 - AI Business Assessment Completion Processing

**Trigger:** Diagnostic survey submission

**Actions:**
- Apply assessment tags to contact
- Fire webhook to Make.com with survey field values as payload
- Make.com handles all downstream processing and report delivery

---

## Make.com Scenario Configuration

**Module 1 - Custom Webhook**
Receives the GHL webhook payload. Parses survey Unique Keys and maps values to named variables for downstream use.

**Module 2 - OpenAI Generate a Completion**
Calls gpt-4o-mini with a structured prompt that includes the parsed survey values. Returns the full Business Readiness Report as a text completion.

**Module 3 - Gmail Send an Email**
Sends the generated report to the founder's email address, pulled from the GHL contact record included in the webhook payload.

---

## Assessment Forms

Two diagnostic forms power the system:

**AI Business Assessment**
Evaluates founder readiness across business planning, market understanding, operational capacity, and investor preparedness. Question logic and field structure were designed to produce survey payloads that the AI model can interpret accurately.

**Funding Readiness Scorecard**
Scores founders against a weighted rubric based on the Futurpreneur framework. Scoring logic runs externally in Make.com rather than inside GHL workflows.

---

## Documentation

A full SOP was written covering:

- Intelligence layer architecture and design rationale
- Step-by-step GHL and Make.com configuration
- Webhook field mapping reference
- Troubleshooting guide
- Future enhancement recommendations

This document was produced for operational handoff and long-term system maintainability.

---

## Role

Technical Support and Applied Research Lead

Responsible for the full AI Intelligence Layer: system architecture, GHL workflow configuration, Make.com scenario build, OpenAI API integration, prompt engineering, scoring logic design, and technical documentation.

---

## Tools and Platforms

GoHighLevel, Make.com, OpenAI API, Gmail, Trello
