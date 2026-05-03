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

## How It Was Built

I built the first working version of the intelligence layer by connecting GoHighLevel, Make.com, the OpenAI API, and Gmail as separate components. Each tool handled one part of the pipeline and passed data to the next.

After the first version was working and tested, I researched the architecture further. I identified redundant handoffs between components and rebuilt the entire system to consolidate all processing inside a single Make.com scenario. This reduced the number of failure points, simplified troubleshooting, and made the pipeline significantly easier to maintain.

I presented the refined system to the project sponsor. She reviewed the architecture and approved it.

After consolidating the intelligence layer, I researched whether the full assessment infrastructure could also be built inside one platform. I confirmed it could. I then built the AI Business Assessment system inside GHL, connecting the form, workflow triggers, pipeline logic, and webhook into a single cohesive flow. After validating that system end to end, I applied the same approach to build the Financial Readiness Scorecard system with its own fields, scoring logic, and output requirements.

---

## Architecture

### Version 1: Initial Build (Make.com)

```
GHL Survey Submission
        |
        v
GHL Workflow -- Webhook Trigger
        |
        v
Make.com Scenario
        |
        |-- Module 1: Custom Webhook (receives GHL payload)
        |
        |-- Module 2: OpenAI Generate a Completion (gpt-4o-mini)
        |              Prompt receives parsed survey field values
        |              Returns personalized Business Readiness Report
        |
        |-- Module 3: Gmail Send an Email
                       Delivers report to founder's email address
```

### Version 2: Consolidated Build (GHL)

After research, I rebuilt the system to run entirely inside GHL. This version powers both the AI Business Assessment and the Financial Readiness Scorecard.

```
GHL Survey Submission (AI Business Assessment or Financial Readiness Form)
        |
        v
GHL Workflow -- Trigger
        |
        |-- Scoring / Report Logic
        |    AI Business Assessment: generates qualitative readiness report
        |    Financial Readiness Scorecard: applies Futurpreneur weighted scoring
        |
        v
GHL Email Action
        Delivers output to founder's email address
```

---

## Tech Stack

### Version 1

| Layer | Tool |
|---|---|
| CRM and workflow automation | GoHighLevel (GHL) |
| Integration and orchestration | Make.com |
| AI report generation | OpenAI API (gpt-4o-mini) |
| Email delivery | Gmail via Make.com |
| Fallback automation | Zapier (evaluated, not deployed) |

### Version 2

| Layer | Tool |
|---|---|
| CRM, workflow automation, scoring, and email delivery | GoHighLevel (GHL) |

---

## What I Built

### Version 1: Make.com Intelligence Layer

I built the initial AI pipeline using Make.com as the processing layer between GHL and OpenAI.

**Module 1 - Custom Webhook**
Receives the GHL webhook payload. Parses survey Unique Keys and maps values to named variables for downstream use.

**Module 2 - OpenAI Generate a Completion**
Calls gpt-4o-mini with a structured prompt that includes the parsed survey values. Returns the full Business Readiness Report as a text completion.

**Module 3 - Gmail Send an Email**
Sends the generated report to the founder's email address pulled from the GHL contact record.

### Version 2: Consolidated GHL System

After researching whether the full pipeline could run inside one platform, I confirmed it could and rebuilt everything inside GHL. This version covers two assessments:

**AI Business Assessment**
Built the form, workflow trigger, report logic, and email delivery entirely inside GHL. The system processes survey responses and delivers a personalized Business Readiness Report to each founder on submission.

**Financial Readiness Scorecard**
Built the form, workflow trigger, scoring logic based on the Futurpreneur weighted framework, and email delivery inside GHL. The system scores each founder's financial readiness and delivers the result directly to their inbox.

---

## Key Technical Decisions

### Webhook field mapping

GHL surveys generate Unique Keys automatically. These keys follow a long concatenated format such as `contact.contacthow_prepared_do_you_feel_to_present_to_investors_m6k_copy` and cannot be edited inside the survey builder. I mapped each key to the correct merge field in the GHL webhook payload so Make.com could parse and pass them accurately to the OpenAI prompt.

### Prompt engineering

The OpenAI module uses a structured prompt that receives survey field values and generates a Business Readiness Report tailored to the founder's responses. The model is gpt-4o-mini, selected for speed and cost efficiency at the assessment volume this system handles.

### Scoring logic architecture

I evaluated using GHL native If/Else branching for the Funding Readiness Scorecard scoring logic. GHL If/Else creates separate END nodes with no merge point, which makes multi-variable weighted scoring impractical inside the workflow builder. The correct architecture routes scoring calculations to Make.com, where logic can be applied across all variables before returning a single result.

The scoring model is based on the Futurpreneur weighted scoring framework, adapted for this system.

### Platform consolidation

The first working version used GHL, Make.com, and the OpenAI API as loosely connected components. After reviewing the architecture, I identified redundant handoffs and rebuilt the pipeline to consolidate all processing inside a single Make.com scenario. This reduced failure points and made the system significantly easier to troubleshoot and extend.

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

Responsible for the AI intelligence layer, Make.com scenario build, OpenAI API integration, prompt engineering, Financial Readiness Scorecard system build, scoring logic design, and technical documentation.

---

## Tools and Platforms

GoHighLevel, Make.com, OpenAI API, Gmail, Trello
