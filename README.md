#  PillarAI API: Intelligent Agent Interaction Platform

Welcome to the PillarAI API, a sophisticated backend service designed for seamless interaction with AI agents. This comprehensive API provides robust endpoints for agent metadata retrieval and AI-powered interactions, leveraging advanced language models for intelligent responses.

##  Core Capabilities

- **Agent Management**: Comprehensive metadata handling for AI agents
- **Intelligent Interactions**: Real-time communication with AI agents
- **Local Deployment**: Flexible development environment
- **Customizable Backend**: Firebase integration for enhanced control
- **RESTful Architecture**: Clean API design for seamless integration

##  Local Development Setup

### Prerequisites

```bash
# 1. Node.js Installation
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# 2. Project Setup
git clone https://github.com/pillardotink/pillar-framework-api.git
cd api

# 3. Environment Configuration
cp .env.example .env
# Add your credentials to .env

# 4. Firebase Setup
cp serviceAccountKey.example.json serviceAccountKey.json
# Configure Firebase credentials

# 5. Install Dependencies
npm install
```

### Environment Configuration

```bash
# .env file contents
OPENAI_API_KEY=your-openai-api-key
PORT=3000
FIREBASE_PROJECT_ID=your-project-id
```

### Firebase Service Account Configuration

```json
{
  "type": "service_account",
  "project_id": "your-project-id",
  "private_key_id": "your-private-key-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\\nYOUR_PRIVATE_KEY\\n-----END PRIVATE KEY-----\\n",
  "client_email": "your-client-email@your-project-id.iam.gserviceaccount.com",
  "client_id": "your-client-id",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/your-client-email@your-project-id.iam.gserviceaccount.com"
}
```

##  API Endpoints

### Agent Metadata

```bash
# Fetch Agent Information
GET /api/agent/:name

# Example Request
curl http://localhost:3000/api/agent/Aura

# Example Response
{
  "name": "Aura",
  "description": "An intelligent agent for technical assistance.",
  "createdAt": "2025-01-01T12:00:00Z"
}
```

### Agent Interaction

```bash
# GET Method
GET /api/agent/:name/interact?message=YourMessage

# POST Method
POST /api/agent/:name/interact
Content-Type: application/json
{
  "message": "Your query here"
}

# Example POST Request
curl -X POST "http://localhost:3000/api/agent/Aura/interact" \
-H "Content-Type: application/json" \
-d '{"message": "What are the current market trends?"}'
```

##  Node.js Integration Example

```javascript
const fetch = require("node-fetch");

async function interactWithAgent(agentName, message) {
  const response = await fetch(`http://localhost:3000/api/agent/${agentName}/interact`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ message }),
  });

  if (!response.ok) {
    console.error("Failed to interact with the agent:", response.statusText);
    return;
  }

  const data = await response.json();
  console.log("Agent Response:", data.reply);
}

// Example Usage
interactWithAgent("Aura", "What are the current market trends?");
```

##  Notes

- The API uses advanced language models for intelligent responses
- All agent metadata is sourced from the local database
- Rate limiting applies to local API endpoints

##  Contributing

We welcome contributions to enhance this API! If you encounter issues or have suggestions, please:

1. Open an issue on our GitHub repository
2. Fork the repository and submit a pull request
3. Include comprehensive test cases with your changes
4. Follow our code style guidelines

The API is designed to be extensible and adaptable to various use cases. For specific implementation details or customization guidance, refer to the documentation in each component directory.