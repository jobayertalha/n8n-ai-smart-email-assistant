# AI-Powered Smart Email Assistant

<p align="center">
  <img width="100%" alt="n8n AI Smart Email Assistant" src="https://github.com/user-attachments/assets/1e531527-a9b0-433d-8143-1dcd3a0aa558" />
</p>

<p align="center">
  <b>Intelligent Gmail automation using n8n, Groq LLMs, and JavaScript</b>
</p>

---

## Project Overview

**AI-Powered Smart Email Assistant** is an email automation workflow built with n8n that helps users organize incoming Gmail messages, identify important emails, and streamline email responses.

The workflow extracts email information, classifies messages by priority, applies corresponding Gmail labels, and integrates AI-powered response generation to support context-aware email handling.

By combining rule-based classification with large language models (LLMs), this project demonstrates how AI and workflow automation can reduce repetitive tasks and improve email management.

## What This Automation Does

- Monitors incoming Gmail messages using an n8n Gmail Trigger.
- Extracts relevant email information, including the sender, subject, and message content.
- Classifies emails into High, Medium, or Low priority.
- Routes messages through conditional workflow branches.
- Applies corresponding Gmail labels.
- Integrates Groq LLMs for AI-powered response generation.
- Processes AI-generated responses before downstream Gmail actions.
- Supports different response-handling strategies based on email priority.

---

## Key Features

### 1. Priority Classification Engine

The workflow uses JavaScript-based classification logic to evaluate incoming email content.

- **High Priority:** Potentially urgent messages, interview invitations, job opportunities, deadlines, and important professional communication.
- **Medium Priority:** Learning opportunities, courses, certifications, and general professional communication.
- **Low Priority:** Promotional messages, advertisements, and other low-importance emails.

The classification logic can be customized to match individual requirements.

### 2. Automated Gmail Labeling

The workflow organizes emails using priority-specific Gmail labels:

- `AI-High-Priority`
- `AI-Medium-Priority`
- `AI-Low-Priority`

These labels make it easier to identify important messages without manually reviewing the entire inbox.

### 3. AI-Powered Response Generation

The workflow integrates **Groq LLMs** to generate responses based on email context.

Potential applications include:

- Professional replies to important messages.
- Context-aware responses to general professional emails.
- Suggested actions or responses for low-priority messages.

The response-generation behavior depends on the configured AI chain and downstream Gmail actions.

### 4. Conditional Workflow Routing

An n8n Switch node routes messages according to their assigned priority.

Each branch can execute a different sequence of actions, allowing the workflow to handle important and less important emails differently.

### 5. Structured Data Processing

JavaScript Code nodes handle email extraction, classification, and data transformation.

Structured outputs help downstream nodes access classification results and other relevant email fields.

### 6. AI Integration

The workflow combines deterministic automation logic with an LLM.

- JavaScript handles classification and data processing.
- Groq provides access to language models for response generation.
- n8n coordinates the workflow and connects the different services.
- Gmail handles email retrieval, labeling, and response-related actions.

---

## Tools and Technologies

| Technology | Purpose |
|---|---|
| **n8n** | Workflow orchestration and automation |
| **Gmail** | Email triggering, labeling, and email-related actions |
| **Groq API** | LLM inference for AI-powered response generation |
| **JavaScript** | Classification logic, email processing, and data transformation |
| **n8n AI Nodes** | Connecting language models to response-generation chains |

---

## Workflow Architecture

The workflow follows a modular structure.

### 1. Gmail Trigger

Detects incoming Gmail messages and starts the automation.

### 2. Extract Email Information

Extracts relevant fields from the incoming message, such as:

- Sender information
- Email subject
- Message body or snippet
- Additional email metadata

### 3. Classify Email Priority

A JavaScript Code node evaluates the available email content and assigns a priority category.

The classification output uses the following category mapping:

| Category | Priority |
|---|---|
| `0` | High |
| `1` | Medium |
| `2` | Low |

The classification logic can be adjusted by modifying the relevant keywords and scoring rules.

### 4. Route by Priority

A Switch node directs each email to the corresponding priority branch.

This allows each category to have its own labeling and response-handling logic.

### 5. Apply Gmail Labels

The workflow applies the appropriate priority label to organize incoming messages.

### 6. Generate AI Responses

The relevant branch connects to the configured AI response-generation components.

The workflow integrates Groq with n8n's AI chain functionality to support context-aware response generation.

### 7. Parse AI Output

The response-processing stage prepares generated content for downstream actions.

Structured parsing helps ensure that the workflow can access the required response fields.

### 8. Perform Priority-Based Actions

Depending on the configured branch, the workflow can prepare a response, create a draft, or execute another Gmail action.

**Important:** Verify each branch and its Gmail action before enabling automatic email sending on a live inbox.

---

## Workflow Overview

The workflow is designed around the following sequence:

```text
Incoming Gmail Message
          |
          v
     Gmail Trigger
          |
          v
 Extract Email Information
          |
          v
 Classify Email Priority
          |
          v
   Route by Priority
          |
     +----+----+
     |    |    |
     v    v    v
   High Medium Low
     |    |    |
     v    v    v
  Apply Priority Labels
     |    |    |
     v    v    v
 AI Response Generation
     |    |    |
     v    v    v
 Parse and Process Output
          |
          v
  Priority-Based Gmail Actions
```

*The diagram illustrates the logical flow. Actual execution depends on the configured node connections and branch-specific actions.*

---

## Workflow Output

### High-Priority Emails

The high-priority branch is intended to:

- Identify important professional messages.
- Apply the high-priority Gmail label.
- Generate a context-aware response.
- Pass the response to the configured downstream Gmail action.

### Medium-Priority Emails

The medium-priority branch is intended to:

- Identify moderately important messages.
- Apply the medium-priority Gmail label.
- Generate a relevant response.
- Support draft-based handling where configured.

### Low-Priority Emails

The low-priority branch is intended to:

- Identify promotional or low-importance messages.
- Apply the low-priority Gmail label.
- Generate a suggested response or recommended action where configured.




## Getting Started

### Prerequisites

Before importing the workflow, make sure you have:

- An n8n instance, either self-hosted or hosted.
- A Gmail account.
- Gmail credentials configured in n8n.
- A Groq API key for AI-powered response generation.
- Access to the required n8n nodes.

### 1. Clone the Repository

```bash
git clone https://github.com/jobayertalha/n8n-ai-smart-email-assistant.git
```

Navigate to the project directory:

```bash
cd n8n-ai-smart-email-assistant
```

### 2. Import the Workflow

1. Open your n8n instance.
2. Open the workflow import option.
3. Import the exported workflow JSON file from this repository.
4. Review the imported nodes and connections.

**Workflow file:** `n8n-ai-smart-email-assistant.json`

*If your exported workflow uses a different filename, use that filename instead.*

### 3. Configure Gmail Credentials

1. Open the Gmail nodes in the workflow.
2. Select or create the appropriate Gmail OAuth2 credentials.
3. Authorize access to the Gmail account you intend to use.
4. Verify that the trigger and Gmail actions have the required permissions.

### 4. Configure Groq

1. Create an API key through the official Groq platform.
2. Add the key using n8n's supported credential mechanism.
3. Open the Groq Chat Model node.
4. Select the appropriate Groq model.
5. Connect the model to the relevant AI chain using the AI model connection.
6. Confirm that the chain receives the correct email content and generates the expected output.

Do not hardcode API keys into JavaScript nodes or commit credentials to GitHub.

### 5. Verify Gmail Labels

Ensure the following labels exist in Gmail or create them as needed:

- `AI-High-Priority`
- `AI-Medium-Priority`
- `AI-Low-Priority`

Check that the Gmail label nodes reference the correct labels.

### 6. Test the Workflow

Before using the workflow with real email traffic:

1. Send a test email containing an urgent or professional request.
2. Verify that the email is extracted and classified correctly.
3. Confirm that the correct Gmail label is applied.
4. Test the medium- and low-priority branches separately.
5. Inspect the Groq response and verify that the output parser handles it correctly.
6. Check each downstream Gmail action.
7. Confirm that no response is sent unexpectedly.

Start with test messages and review the results before enabling automatic sending.

---

## Project Structure

A suggested repository structure is:

```text
n8n-ai-smart-email-assistant/
│
├── n8n-ai-smart-email-assistant.json
├── README.md
└── LICENSE
```

The workflow JSON contains the exported n8n workflow. Add a `LICENSE` file only after confirming the license terms applicable to your project and any upstream material.

---

## Use Cases

This automation can be adapted for:

- **Job seekers:** Organizing recruiter emails and interview invitations.
- **Professionals:** Prioritizing work-related communication.
- **Students and learners:** Managing course, certification, and learning-related messages.
- **Small businesses:** Streamlining routine email handling.
- **Productivity workflows:** Combining rule-based classification with AI-assisted responses.

---

## Future Improvements

Possible extensions include:

- Improving priority classification with configurable rules or LLM-assisted classification.
- Adding confidence thresholds and a manual-review path.
- Supporting additional email providers.
- Adding CRM integrations.
- Logging workflow results for monitoring and debugging.
- Adding retry handling and error notifications.
- Preventing duplicate processing of the same email.
- Adding configurable rules for when replies may be sent automatically.
- Measuring classification accuracy and the time saved through automation.

These are potential enhancements, not claims about features already implemented.

---

## Security and Responsible Automation

Email workflows may process sensitive personal and professional information.

Follow these practices:

- Store API keys and OAuth credentials in n8n's credential system.
- Never commit secrets, access tokens, or private email data to GitHub.
- Test the workflow with sample messages before using a real inbox.
- Review AI-generated replies before enabling automatic sending.
- Avoid sending automatic replies to sensitive, confidential, or ambiguous messages.
- Follow the applicable Gmail, API-provider, and data-protection requirements.

---

## Author

**Talha Jobayer Zihan**

CSE Graduate | AI/ML Engineer | Automation Enthusiast

- **LinkedIn:** [linkedin.com/in/talha-jobayer](https://www.linkedin.com/in/talha-jobayer)
- **GitHub:** [github.com/jobayertalha](https://github.com/jobayertalha)

---

## Acknowledgments

This project builds on an existing email-automation workflow and adapts it to integrate n8n, Gmail, JavaScript-based priority classification, and Groq-powered AI response generation.

If you are adapting an existing public repository, credit the original author and follow the original repository's license terms. Add the source repository link here before publishing.

---

## License

Add the license that applies to your implementation after verifying the original project's license and the terms governing any reused workflow components.

---

If you find this project useful, consider giving the repository a ⭐!
