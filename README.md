# Blueprint MCP

![Blueprint MCP](images/blueprint-mcp.png)

*Image generated using Blueprint MCP, Nano Banana Pro, and Arcade MCP server.*

Diagram generation for understanding codebases and system architecture using Nano Banana Pro.

**Works with Arcade's ecosystem:** Combine with HubSpot, Google Drive, GitHub, and other Arcade tools to extract data from your systems and visualize it as diagrams.

## Setup

### 1. Sign up for Arcade
https://arcade.dev

### 2. Install Dependencies
```bash
# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install Arcade CLI
pip install arcade-mcp
```

### 3. Login to Arcade
```bash
arcade-mcp login
```

### 4. Get Google AI Studio API Key
https://aistudio.google.com/ → Create API key

### 5. Store Secret in Arcade
```bash
arcade-mcp secret set GOOGLE_API_KEY="your_api_key_here"
```

### 6. Deploy Server
```bash
cd architect_mcp
arcade-mcp deploy
```

### 7. Create Gateway
1. Go to https://api.arcade.dev/dashboard
2. Click "Gateways" → "Create Gateway"
3. Add your deployed `architect_mcp` server to the gateway

### 8. Configure Cursor
1. In Cursor: Settings → MCP
2. Add your Arcade gateway URL
3. Restart Cursor

## Usage

### Tools

- `start_diagram_job` - Start generation, returns job ID
- `check_job_status` - Check if complete
- `download_diagram` - Download PNG as base64

### Example Prompts

**Visualize code architecture:**
```
Analyze the authentication module in src/auth/ and create an 
architecture diagram showing the components and their relationships.
```

**Document API flows:**
```
Create a sequence diagram showing the OAuth login flow based on 
the code in src/auth/oauth.py
```

**Explain processes:**
```
Generate a flowchart explaining how our payment processing works,
showing the steps from checkout to confirmation.
```

**Understand data pipelines:**
```
Create a data flow diagram for our ETL pipeline showing sources,
transformations, and destinations based on the data/ directory.
```

**Combine with other Arcade tools:**
```
Pull the latest deal from HubSpot for "Acme Corp" and create an
architecture diagram of the proposed solution.
```

```
Read the system design doc from Google Drive and generate a 
visual architecture diagram from it.
```

## How It Works

1. `start_diagram_job` → Returns job ID instantly
2. Wait 30 seconds (Nano Banana Pro generates)
3. `check_job_status` → Check if "Complete"
4. `download_diagram` → Get base64 PNG
5. Agent decodes and saves to workspace

---

## Example Diagrams

### Enterprise Architecture - Banking Use Case

**Cursor Prompt:**
```
Can you understand Arcade deeply and create an architecture diagram for someone 
who's new and wants to understand Arcade in the broader AI, LLM, and agent landscape? 
I want this architecture to fit into a realistic enterprise scenario like a bank, 
showcasing how Arcade MCP Runtime fits into their broader architecture.

https://docs.arcade.dev/llms.txt
```

*Prompt received by Blueprint MCP tool: "Create enterprise architecture diagram with 5 layers: LAYER 1 End Users (Customer Service Agents, Loan Officers, Compliance Team, IT Ops), LAYER 2 Banking AI Assistant (Cursor IDE / Custom UI), LAYER 3 AI Layer showing GPT-4/Claude and LangChain/CrewAI (Model-Agnostic), LAYER 4 Arcade MCP Runtime (large box) containing Runtime Components (MCP Gateway, Tool Registry, OAuth 2.0 Auth, Secret Management, Session Manager) AND Hosted MCP Servers section with 6 MCP servers (Salesforce, Email/Gmail, Slack, Database, Document, Custom Banking) ALL INSIDE the Arcade box, LAYER 5 Bank's Existing Infrastructure (Core Banking System, CRM Salesforce, Compliance Database, Document Repository, Communication Systems, Legacy APIs). Show data flow arrows with labels (Tool Calls, Authenticated Requests, API Calls). Use technical whiteboard style, muted colors (gray, light blue, purple, orange), monospace fonts, 16:9."*

![Enterprise Banking Architecture](images/arcade_enterprise_banking.png)

### LangGraph Architecture Learning Card

**Cursor Prompt:**
```
Help me understand the LangGraph architecture better. I have checked out the 
LangGraph codebase here:

/Users/guru/dev/nano/langgraph

Can you do a thorough analysis and help me understand the architecture? I would 
love to know details in a visual image: The key components involved, the flows, 
and can you create like one fully visual learning card sort of thing that helps 
me understand the architecture which I can print and give it to my fellow 
architects and help them learn?
```

*Prompt received by Blueprint MCP tool: "Create LangGraph architecture learning card with 6 sections: Core Components (State, Nodes, Edges with flow diagram), StateGraph Class workflow (Define → Build → Compile → Execute), Pregel-Inspired Execution showing super-steps with parallel/sequential execution examples, Checkpointing System (BaseCheckpointSaver, checkpoint-postgres/sqlite, state snapshots flow), Monorepo Structure (langgraph core, prebuilt, checkpoint libs, cli, sdk-py, sdk-js), and Capabilities (Durable execution, Human-in-the-loop, Memory, Streaming, Multi-agent, Sub-graphs). Use technical whiteboard style, muted colors (blue, gray, purple, green, orange), monospace fonts for code terms, information-dense layout, 16:9, printable quality."*

![LangGraph Architecture](images/langgraph_architecture_learning_card.png)
