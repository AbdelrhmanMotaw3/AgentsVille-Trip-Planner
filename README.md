# AgentsVille Trip Planner

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

> An intelligent multi-agent travel planning system powered by advanced LLM reasoning techniques. This project demonstrates production-ready AI agent architecture with role-based prompting, Chain-of-Thought reasoning, ReAct prompting, and iterative feedback loops.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Technical Details](#technical-details)
- [Key Achievements](#key-achievements)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

## Overview

The **AgentsVille Trip Planner** is a sophisticated AI-powered travel planning system that generates personalized, weather-aware itineraries for travelers. Built as part of the Udacity Agentic AI Nanodegree program, this project showcases enterprise-level AI engineering practices including:

- **Multi-Agent Architecture**: Specialized agents for planning and refinement
- **Advanced Prompting Techniques**: Chain-of-Thought and ReAct methodologies
- **Structured Output Validation**: Pydantic-based schema validation
- **Comprehensive Evaluation System**: Multi-criteria quality assurance
- **Iterative Refinement**: Self-correcting feedback loops

## Features

### 🎯 Core Capabilities

- **Intelligent Itinerary Generation**: Creates day-by-day travel plans using Chain-of-Thought reasoning
- **Weather-Aware Planning**: Automatically adjusts activities based on weather conditions
- **Budget Optimization**: Ensures cost-effective planning within specified constraints
- **Interest Matching**: Personalizes recommendations based on traveler preferences
- **Iterative Refinement**: ReAct-based agent continuously improves plans through feedback loops

### 🔧 Technical Features

- **Pydantic Data Validation**: Type-safe data models with automatic validation
- **Tool Integration**: Calculator, activity retrieval, and evaluation tools
- **Structured JSON Output**: Consistent, validated response formats
- **Error Recovery**: Automatic detection and correction of calculation errors
- **Comprehensive Evaluation**: Multi-criteria assessment ensuring quality and compliance

## Architecture

### System Components

#### 1. **Itinerary Agent**
- **Purpose**: Initial itinerary generation
- **Technique**: Chain-of-Thought prompting
- **Output**: Structured travel plan with day-by-day activities

#### 2. **Revision Agent**
- **Purpose**: Iterative plan refinement
- **Technique**: ReAct (Reasoning + Acting) prompting
- **Process**: THOUGHT → ACTION → OBSERVATION cycles

#### 3. **Evaluation System**
- **Criteria**: Date matching, cost accuracy, budget compliance, activity validation, weather compatibility
- **Implementation**: LLM-powered assessment with rule-based validation

### Data Models

| Model | Purpose |
|-------|---------|
| `VacationInfo` | Traveler details, dates, budget, and constraints |
| `TravelPlan` | Complete itinerary structure with validation |
| `Activity` | Individual activity details and metadata |
| `ActivityRecommendation` | Activities with reasoning and recommendations |

### Tools

- **`calculator_tool`**: Mathematical calculations for cost optimization
- **`get_activities_by_date_tool`**: Activity retrieval by date
- **`run_evals_tool`**: Comprehensive evaluation execution
- **`final_answer_tool`**: Structured final output delivery

## Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- OpenAI API key (optional, for real LLM calls)

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <https://github.com/AbdelrhmanMotaw3/AgentsVille-Trip-Planner.git>
   cd AgentsVille-Trip-Planner
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

4. **Open the notebook**
   - Navigate to `AgentsVille_Trip_Planner_Solution_v2.ipynb`
   - Follow the instructions in the notebook

## Usage

### Mock Mode (Default)

The system runs with mock data by default, making it perfect for testing and demonstration without API costs.

### Real API Mode

1. Configure your API key in the notebook:
   ```python
   client = OpenAI(
       base_url="https://openai.vocareum.com/v1",
       api_key="YOUR_API_KEY_HERE"
   )
   ```

2. Run the notebook cells sequentially to generate a personalized itinerary.

### Example Workflow

```python
# Define vacation details
vacation_info = VacationInfo(
    city="AgentsVille",
    start_date="2025-06-10",
    end_date="2025-06-12",
    travelers=["Alice", "Bob"],
    interests=[Interest.TECHNOLOGY, Interest.ART],
    budget=200
)

# Generate initial itinerary
itinerary = generate_itinerary(vacation_info, client, model)

# Refine based on feedback
refined_itinerary = refine_itinerary(itinerary, feedback, client, model)
```

## Project Structure

```
AgentsVille Trip Planner/
├── AgentsVille_Trip_Planner_Solution_v2.ipynb  # Main implementation notebook
├── project_lib.py                              # Core utilities and data models
├── requirements.txt                            # Python dependencies
├── README.md                                   # Project documentation
├── LICENSE                                     # MIT License
└── .gitignore                                  # Git ignore rules
```

## Technical Details

### Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `openai` | 1.74.0 | OpenAI API client |
| `pydantic` | 2.11.7 | Data validation and modeling |
| `pandas` | 2.3.0 | Data manipulation |
| `json-repair` | 0.47.1 | JSON parsing and repair |
| `numexpr` | 2.11.0 | Mathematical expression evaluation |
| `python-dotenv` | 1.1.0 | Environment variable management |
| `jupyter` | ≥1.0.0 | Notebook environment |

### System Prompts

- **`ITINERARY_AGENT_SYSTEM_PROMPT`**: Chain-of-Thought planning with structured output
- **`ACTIVITY_AND_WEATHER_ARE_COMPATIBLE_SYSTEM_PROMPT`**: Weather compatibility assessment
- **`ITINERARY_REVISION_AGENT_SYSTEM_PROMPT`**: ReAct implementation with tool usage

### Example Output

The system generates structured JSON itineraries:

```json
{
  "city": "AgentsVille",
  "start_date": "2025-06-10",
  "end_date": "2025-06-12",
  "total_cost": 113,
  "itinerary_days": [
    {
      "date": "2025-06-10",
      "weather": {
        "temperature": 31.0,
        "condition": "clear"
      },
      "activity_recommendations": [
        {
          "activity": {
            "name": "FutureTech Breakfast Meet-Up",
            "price": 20,
            "related_interests": ["technology"]
          },
          "reasons_for_recommendation": [
            "Matches traveler interests",
            "Indoor event"
          ]
        }
      ]
    }
  ]
}
```

## Key Achievements

### ✅ Implementation Completeness

- [x] Pydantic models for type-safe data validation
- [x] Chain-of-Thought prompting for structured itinerary generation
- [x] Complete ReAct agent with THOUGHT → ACTION → OBSERVATION cycle
- [x] Comprehensive evaluation system with multiple criteria
- [x] Enhanced weather-activity compatibility assessment (14+ examples)
- [x] Automatic cost optimization and budget compliance
- [x] Traveler feedback integration (minimum 2 activities per day)
- [x] Structured JSON output validation with Pydantic schemas

### 🎯 Performance Metrics

- **100% Evaluation Pass Rate**: All evaluation functions pass successfully
- **Automatic Cost Optimization**: Reduces costs while maintaining quality
- **Weather-Aware Planning**: Intelligent indoor/outdoor activity selection
- **Interest Matching**: Activities tailored to specific traveler preferences
- **Iterative Refinement**: Multi-step ReAct loop with tool usage
- **Error Recovery**: System handles and fixes calculation errors automatically

### 🔄 Version 2 Improvements

#### Complete ReAct Cycle Implementation
- **Enhancement**: Added detailed OBSERVATION processing in the revision agent
- **Impact**: Agent now properly analyzes tool results to inform subsequent decisions

#### Enhanced Weather Compatibility
- **Enhancement**: Expanded examples from 7 to 14 comprehensive scenarios
- **Impact**: More accurate weather compatibility decisions with improved LLM guidance

#### TravelPlan Schema Integration
- **Enhancement**: Integrated Pydantic model schemas in system prompts
- **Impact**: Better structured output generation with proper JSON validation

## Contributing

This project was developed as part of an academic program. For suggestions or improvements, please open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Abdelrhman Motawea**

This project was developed as part of the **Udacity Agentic AI Nanodegree** program, demonstrating advanced LLM reasoning techniques and production-ready AI agent architecture.

---

**Note**: This project showcases enterprise-level AI engineering practices including multi-agent systems, advanced prompting techniques, and comprehensive evaluation frameworks. The AgentsVille Trip Planner represents a complete, production-ready AI travel planning system.
