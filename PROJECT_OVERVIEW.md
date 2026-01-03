# AI-Powered Trip Planner - Project Overview

## 📋 Project Description

This is an **AI-Powered Trip Planner** application that uses multi-agent AI systems to create personalized travel itineraries. The application leverages CrewAI framework with specialized AI agents that work together to research destinations, gather travel information, and compile comprehensive travel plans based on user preferences.

### Key Features

- 🌍 **Destination Research**: Gathers information about accommodations, cost of living, visa requirements, transportation, and weather
- 🎯 **Personalized Recommendations**: Tailors attractions, food, and activities based on user interests
- 📅 **Itinerary Planning**: Creates day-by-day travel plans with time allocations and detailed activity descriptions
- 🌐 **Multi-language Support**: Automatically responds in French for French-speaking destinations
- 💾 **Export Functionality**: Allows users to download travel plans as text files

---

## 🏗️ Architecture & How It Works

The application uses a **multi-agent AI system** where three specialized agents collaborate sequentially:

1. **Location Expert Agent** (`location_expert`)
   - Researches travel logistics (accommodations, costs, visas, transportation, weather)
   - Outputs: `city_report.md`

2. **Guide Expert Agent** (`guide_expert`)
   - Provides city-specific recommendations (attractions, food, events)
   - Tailors suggestions based on user interests
   - Outputs: `guide_report.md`

3. **Planner Expert Agent** (`planner_expert`)
   - Synthesizes information from both previous agents
   - Creates a comprehensive, structured travel itinerary
   - Outputs: `travel_plan.md`

The agents work in a **sequential process** where each agent's output feeds into the next, ensuring comprehensive and cohesive travel planning.

---

## 🛠️ Technology Stack

### Core Frameworks & Libraries

#### 1. **CrewAI** (`crewai`, `crewai[tools]`)
   - **Purpose**: Multi-agent AI framework for orchestrating AI agents
   - **Usage**: 
     - Creates and manages AI agents with specific roles
     - Coordinates task execution in sequential workflow
     - Handles agent communication and output management
   - **Key Components**:
     - `Agent`: Defines specialized AI agents
     - `Task`: Defines what each agent should accomplish
     - `Crew`: Orchestrates agents and tasks
     - `Process`: Controls execution flow (sequential in this project)

#### 2. **Streamlit** (`streamlit`)
   - **Purpose**: Web application framework for creating the user interface
   - **Usage**: 
     - Provides interactive web UI for user inputs
     - Displays travel plans and results
     - Handles file downloads
   - **Features Used**:
     - Text inputs, date pickers, text areas
     - Button triggers for AI processing
     - Markdown rendering for formatted output
     - Download buttons for exporting plans

#### 3. **LangChain** (`langchain`, `langchain_ollama`, `langchain_community`)
   - **Purpose**: Framework for building LLM-powered applications
   - **Usage**:
     - Integrates with Ollama for local LLM access
     - Provides tool interfaces for web search
     - Connects AI agents with external tools

#### 4. **Ollama** (via `langchain_ollama`)
   - **Purpose**: Local Large Language Model (LLM) server
   - **Model Used**: `llama3.2`
   - **Configuration**: 
     - Base URL: `http://localhost:11434`
     - Runs locally (no API costs)
     - Provides AI reasoning capabilities for all agents

#### 5. **DuckDuckGo Search** (`duckduckgo-search`)
   - **Purpose**: Web search tool for real-time information gathering
   - **Usage**: 
     - Agents use this to search for current travel information
     - Provides up-to-date data on accommodations, events, weather, etc.
     - Integrated via `DuckDuckGoSearchResults` from LangChain

#### 6. **CrewAI Tools** (`crewai_tools`)
   - **Purpose**: Additional tools for CrewAI agents
   - **Available Tools**: WebsiteSearchTool, ScrapeWebsiteTool (commented out in current implementation)

#### 7. **SQLite** (`pysqlite3-binary`)
   - **Purpose**: Lightweight database for CrewAI's internal operations
   - **Usage**: Stores agent interactions and task outputs

---

## 📁 Project Structure

```
AI Powered trip planner/
│
├── streamlit_trip_advisor_app/
│   ├── my_app_2.py          # Main Streamlit application
│   ├── TravelAgents.py      # AI agent definitions (3 agents)
│   ├── TravelTasks.py       # Task definitions for each agent
│   └── TravelTools.py       # Web search tool implementation
│
├── L-2.ipynb                # Jupyter notebook for development/testing
├── requirements.txt         # Python dependencies
├── README.md                # Basic setup instructions
│
└── Generated Outputs:
    ├── city_report.md       # Location expert's research output
    ├── guide_report.md      # Guide expert's recommendations output
    └── travel_plan.md       # Final compiled travel plan
```

---

## 🔧 Technical Implementation Details

### Agent Configuration

Each agent is configured with:
- **Role**: Specific expertise area
- **Goal**: Primary objective
- **Backstory**: Context for AI behavior
- **Tools**: Web search capability (`search_web_tool`)
- **LLM**: Ollama's llama3.2 model
- **Max Iterations**: 5 (limits agent processing cycles)
- **Verbose**: True (for debugging/logging)

### Task Flow

1. **Location Task** → Researches logistics and outputs `city_report.md`
2. **Guide Task** → Creates recommendations and outputs `guide_report.md`
3. **Planner Task** → Uses context from both previous tasks to create final `travel_plan.md`

### Web Search Integration

The `search_web_tool` function:
- Uses DuckDuckGo Search API
- Returns 10 search results per query
- Agents automatically use this tool to gather real-time information
- No API key required (free search service)

---

## 🚀 Setup & Installation

### Prerequisites

1. **Python 3.8+** installed
2. **Ollama** installed and running locally
   - Download from: https://ollama.ai
   - Pull the model: `ollama pull llama3.2`
   - Ensure Ollama is running on `http://localhost:11434`

### Installation Steps

1. **Install Python dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Verify Ollama is running**:
   ```bash
   ollama serve
   # In another terminal:
   ollama pull llama3.2
   ```

3. **Run the Streamlit application**:
   ```bash
   cd streamlit_trip_advisor_app
   streamlit run my_app_2.py
   ```

4. **Access the application**:
   - Open browser to: `http://localhost:8501`
   - Fill in travel details (from city, destination, dates, interests)
   - Click "Generate Travel Plan"
   - Wait for AI agents to process (may take a few minutes)
   - View and download your personalized travel plan

---

## 💡 Key Technologies Summary

| Technology | Purpose | Why It's Used |
|------------|---------|---------------|
| **CrewAI** | Multi-agent orchestration | Enables specialized AI agents to collaborate on complex tasks |
| **Streamlit** | Web UI | Quick, Python-based interface without frontend complexity |
| **Ollama (llama3.2)** | Local LLM | Free, private AI processing without API costs |
| **LangChain** | LLM integration | Standardized interface for connecting agents with tools |
| **DuckDuckGo Search** | Real-time data | Free web search for current travel information |
| **Python** | Core language | Main development language for all components |

---

## 🎯 Use Cases

- **Personal Travel Planning**: Create detailed itineraries for personal trips
- **Travel Agencies**: Assist in creating client travel plans
- **Tourism Research**: Gather comprehensive destination information
- **Educational**: Learn about destinations before visiting

---

## 📝 Notes

- The application requires **Ollama running locally** - ensure it's started before running the app
- Processing time depends on:
  - Number of web searches performed
  - Complexity of the destination
  - Ollama model performance
- Generated markdown files are saved in the project root directory
- The application supports **French language** output for French-speaking destinations automatically

---

## 🔮 Future Enhancements (Potential)

- Integration with booking APIs (hotels, flights)
- Multi-language support beyond French
- Budget calculation and optimization
- Interactive map integration
- Weather API integration for real-time forecasts
- User account system for saving plans
- Collaborative planning features

---

## 📄 License & Credits

This project demonstrates the use of:
- CrewAI framework for multi-agent AI systems
- Streamlit for rapid web app development
- Ollama for local LLM inference
- DuckDuckGo for privacy-focused web search

---

**Last Updated**: 2025
**Project Type**: AI-Powered Travel Planning Application
**Development Status**: Functional MVP

