# AI-Powered-Business-Assessment-System-NMCD-Inc.

Production-deployed AI automation system for NMCD Inc. automating personalized founder readiness reports using GoHighLevel, Make.com, and OpenAI GPT-4o-mini.

Overview:

Production-deployed AI automation system built for NMCD Inc. as part of the DreamBuilder Suite capstone at Montclair State University, Spring 2026. The system automates personalized founder readiness reports triggered by survey submission, replacing hours of manual coaching review with a seconds-long automated delivery pipeline.

Contributions:

Designed and built the initial AI Intelligence Layer integrating GoHighLevel, Make.com, the OpenAI API, and Gmail to automate report delivery from survey submission.

Researched and rebuilt the system after the first version was working, consolidating everything under one platform to eliminate unnecessary complexity and improve maintainability.

Presented the refined system to sponsor Nikki Moodie and received direct approval on the architecture.

Built and configured the W2 AI Business Assessment Completion Processing workflow in GoHighLevel end to end.

Configured the Make.com scenario with three modules: Custom Webhook, OpenAI Generate a Completion, and Gmail Send an Email, to handle the full report pipeline.

Engineered prompt logic for GPT-4o-mini to generate personalized Business Readiness Reports from survey responses.

Built and structured the AI Business Assessment form and Financial Readiness form, mapping question logic and survey fields to drive the assessment pipeline.

Mapped GoHighLevel survey Unique Keys to webhook merge fields, solving an auto-generation limitation in the GHL survey builder.

Identified that GHL If/Else branching creates separate END nodes with no merge point and moved scoring calculations to Make.com.

Set up the OpenAI API account and coordinated funding with the sponsor.

Authored the full SOP document covering architecture, configuration, troubleshooting, and future enhancements.


Impact:

Delivered a working AI report generation system that moves from survey submission to personalized email report in seconds.

Built the two core assessment forms that power the entire DreamBuilder Suite intake process.

Created a scalable system requiring zero manual effort per client.

Produced reusable documentation enabling future team members to maintain and extend the system without starting from scratch.

Established a documented architecture NMCD can extend to future products and scoring models.


Tools and Platforms

GoHighLevel (CRM and workflow automation)

Make.com (pipeline automation)

OpenAI API, GPT-4o-mini (AI report generation)

Gmail API (automated report delivery)

Prompt engineering and webhook architecture

SOP documentation
