🤖 ATS Resume Scorer Agent (n8n + Google Gemini)
This n8n workflow uses the Google Gemini API to analyze uploaded resumes, score them for general ATS (Applicant Tracking System) compatibility, and extract key candidate data, saving the results directly to a Google Sheet.

The agent focuses on evaluating formatting, keyword relevance, and content quality (achievements vs. duties) without requiring a specific job description.

📁 Repository Contents

File,Description
ats_scorer_workflow.json,The complete n8n workflow file. Import this directly into your n8n instance.
screenshot_before_execution.png,Screenshot showing the node setup prior to running.
screenshot_after_execution.png,Screenshot showing the data output after the AI processing.
screenshot_google_sheet.png,Screenshot of the Google Sheet with the final structured data.

🚀 Key Integrations
AI Engine: Google Gemini API (via the n8n AI Agent node).

Data Input: Google Drive (or local file upload) to fetch the resume file.

Data Output: Google Sheets for structured data logging.

Authentication: Uses Google Drive / Gmail OAuth2 for Google services.

⚙️ Prerequisites and Setup
To run this workflow, you need the following:

1. n8n Instance
A running instance of n8n (Cloud or Self-Hosted).

2. API Keys
Gemini API Key: Required for the AI Agent node. You must create an n8n credential for the Gemini API.

3. Google Services
You will need to set up a shared Google OAuth2 Credential in n8n for these services.

Google Drive: Required to read the resume file (PDF/DOCX).

Google Sheets: A new spreadsheet must be created with the following exact column headers in the first row:

Applicant Name

Email Address

ATS Score

Improvement Summary

... (Plus any columns you wish to use for the nested feedback, if not consolidated).

Gmail (Optional but Recommended): Used for sending the detailed score/feedback report back to the candidate.

4. Workflow Import
In n8n, click New Workflow.

Click the menu icon (☰) and select Import from JSON.

Upload the ats_scorer_workflow.json file.

Replace all placeholder credentials with your newly created Gemini and Google credentials

🖼️ Workflow Execution Showcase
The workflow ensures a clean transformation from raw file to structured database entry.

1. Before Execution (Workflow Ready)
Description: The workflow is armed, waiting for a file trigger. 
The Extract from File node pulls the text, which is passed to the AI Agent. 
The Google Sheets node is configured with the correct column mappings (ats_score, resume_name, etc.).

2. After Execution (Data Flow)
Description: The screenshot shows the successful output of the AI Agent node.
The JSON object is visible, containing the key fields: ats_score (e.g., 89),
resume_name, resume_email, and the calculated improvement_summary which consolidates all feedback.

3. Final Output (Google Sheet)
Description: The final data is appended to the Google Sheet.
Each run creates a new row with the candidate's details, the calculated ATS Score,
and the Improvement Summary, making the data instantly readable and actionable for review.

🧠 AI Agent Prompt Design
The core intelligence is managed by a specific System Message to enforce structured output:

Goal: Act as an ATS parser and senior recruiter.

Scoring: Based on Format, Content Quality (metrics/achievements), and Keyword Relevance.

Output Format: Strictly a JSON object containing the applicant's name, email, the numeric score (ats_score), and the consolidated feedback (improvement_summary)







