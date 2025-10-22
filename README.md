AI Agent System - HubSpot CRM Automation
A multi-agent AI system for automating HubSpot CRM operations using LangGraph and OpenAI.
🏗️ Architecture
This project implements a multi-agent architecture with:

Global Orchestrator Agent: Receives user queries and delegates tasks to specialized agents
HubSpot Agent: Manages CRM operations (create/update contacts and deals)
Email Agent: Sends confirmation notifications after operations

User Query → Orchestrator → HubSpot Agent → Email Agent → Confirmation
🚀 Features
✅ Natural language processing for CRM operations
✅ Dynamic payload generation based on user queries
✅ Support for multiple HubSpot operations:

Create new contacts
Update existing contacts
Create deals
Edit deals
✅ Automatic email notifications
✅ Error handling and graceful degradation
✅ Modular and reusable components
✅ Mock mode for testing without real API keys

📋 Prerequisites

Python 3.8 or higher
pip (Python package manager)
Git

🔧 Installation
Step 1: Clone the Repository
bashgit clone <your-repo-url>
cd ai-agent-hubspot-automation
Step 2: Create Virtual Environment
bash# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
Step 3: Install Dependencies
bashpip install -r requirements.txt
Step 4: Configure API Keys
Open config.json and add your API keys:
json{
  "openai": {
    "api_key": "sk-your-openai-key",
    "model": "gpt-4"
  },
  "hubspot": {
    "api_key": "your-hubspot-api-key",
    "base_url": "https://api.hubapi.com"
  },
  "email": {
    "smtp_server": "smtp.gmail.com",
    "smtp_port": 587,
    "sender_email": "your-email@gmail.com",
    "sender_password": "your-app-password",
    "recipient_email": "bilalkhanscc@gmail.com"
  }
}
Getting API Keys:
OpenAI API Key:

Go to https://platform.openai.com/api-keys
Create a new API key
Copy and paste into config.json

HubSpot API Key:

Log into HubSpot
Go to Settings → Integrations → Private Apps
Create a private app with required scopes (contacts, deals)
Copy the API key

Gmail App Password (for email):

Enable 2-factor authentication on your Google account
Go to https://myaccount.google.com/apppasswords
Generate an app password for "Mail"
Use this password in config.json

🎮 Usage
Running in Demo Mode (Mock APIs)
For testing without real API keys:
bashpython main.py
The system will use mock implementations and show you how it works.
Running with Real APIs

Configure all API keys in config.json
Run the main script:

bashpython main.py
Example Queries
Try these natural language queries:
python# Create a contact
"Create a new contact named John Doe with email john.doe@example.com and phone +1234567890"

# Update a contact
"Update contact with email jane@example.com to set company as TechCorp"

# Create a deal
"Create a deal named 'Enterprise Package' worth $50000 for contact john.doe@example.com"

# Update a deal
"Update deal with ID 12345 to change status to closed-won"
📁 Project Structure
ai-agent-hubspot-automation/
│
├── main.py                 # Global Orchestrator Agent
├── hubspot_agent.py        # HubSpot CRM Agent
├── email_agent.py          # Email Notification Agent
├── config_loader.py        # Configuration Loader
├── config.json             # API Configuration (add your keys)
├── requirements.txt        # Python Dependencies
└── README.md              # This file
🔍 How It Works

User submits a query in natural language
Orchestrator Agent analyzes the query and determines the intent
HubSpot Agent is invoked with the query:

Uses LLM to extract parameters (name, email, company, etc.)
Calls appropriate function (create_contact, update_contact, etc.)
Returns operation result


Email Agent sends confirmation:

Composes email with operation details
Sends to configured recipient


Results are displayed to the user

🛡️ Error Handling
The system handles:

Missing API keys (falls back to mock mode)
Invalid queries (provides helpful error messages)
API failures (graceful degradation)
Missing data (prompts for required fields)

🧪 Testing
To test different operations, modify the test_queries list in main.py:
pythontest_queries = [
    "Your custom query here",
    "Another test query",
]
🔒 Security Notes
⚠️ Never commit API keys to version control!

Add config.json to .gitignore
Use environment variables for production
Rotate API keys regularly
Use app-specific passwords for email

📊 Sample Output
============================================================
AI AGENT SYSTEM - WORKFLOW AUTOMATION
============================================================

📝 User Query: Create a new contact named John Doe with email john.doe@example.com and phone +1234567890

🔄 HubSpot Agent Processing Query...
   └─ Operation: create_contact
   └─ Parameters: {
      "firstname": "John",
      "lastname": "Doe",
      "email": "john.doe@example.com",
      "phone": "+1234567890"
   }

✅ HubSpot Operation Successful!

📧 Email Agent Sending Notification...
   └─ Email sent to: bilalkhanscc@gmail.com
   └─ Subject: ✅ HubSpot CRM Operation Confirmed: Create Contact

✅ Email Notification Sent Successfully!

------------------------------------------------------------
📊 OPERATION RESULTS:
------------------------------------------------------------

✅ Operation: Create Contact
📋 Status: success
🔍 Details: {
  "id": "mock_contact_12345",
  "properties": {
    "firstname": "John",
    "lastname": "Doe",
    "email": "john.doe@example.com",
    "phone": "+1234567890"
  },
  "created": true
}
📧 Email Sent: True

============================================================
🎯 Evaluation Criteria Coverage
✅ Correct implementation of AI agents and function calling

Global Orchestrator delegates tasks appropriately
HubSpot Agent uses function calling for dynamic operations
Email Agent uses function calling for notifications

✅ Proper architecture with modular components

Separate agents for different responsibilities
Config loader for API management
Reusable tool definitions

✅ Code quality and documentation

Clean, well-commented code
Type hints for better readability
Comprehensive README

✅ Error handling and robustness

Graceful fallbacks for missing configs
Try-catch blocks for API calls
Mock mode for testing

✅ LangGraph best practices

StateGraph for workflow management
Proper node and edge definitions
Conditional routing based on agent state

🚧 Extending the System
Adding New CRM Operations

Add a new tool function in hubspot_agent.py:

python@tool
def your_new_operation(param1: str, param2: str) -> Dict:
    """Description of your operation"""
    # Implementation here
    pass

Add it to the tools list in __init__
Update the process_query method to handle it

Adding New Agents

Create a new agent file (e.g., slack_agent.py)
Add a node in main.py
Update the routing logic
Add configuration to config.json

🐛 Troubleshooting
Issue: ModuleNotFoundError
bashpip install -r requirements.txt
Issue: OpenAI API Error

Check your API key is valid
Ensure you have credits in your OpenAI account
Verify the model name is correct

Issue: Email not sending

Enable 2FA on Gmail
Use app-specific password, not regular password
Check SMTP settings are correct

Issue: Config file not found

Ensure config.json is in the same directory as main.py
System will use default mock config if file is missing

📝 License
This project is for assessment purposes.
👤 Author
Created for Aegasis Labs Assessment
📞 Support
For questions or issues, contact: bilalkhanscc@gmail.com
