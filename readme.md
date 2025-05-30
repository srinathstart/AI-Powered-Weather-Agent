# LangChain Agents with ReAct Framework

This project demonstrates how to create intelligent agents using LangChain that can perform multi-step reasoning and interact with external tools to answer complex queries.

## Overview

The project implements a ReAct (Reasoning and Acting) agent that can:
- Search the web for information using DuckDuckGo
- Fetch current weather data for any city
- Chain multiple actions together to solve complex problems

## Features

- **Web Search Integration**: Uses DuckDuckGo search tool for retrieving information
- **Weather API Integration**: Fetches real-time weather data using WeatherStack API
- **ReAct Agent Framework**: Implements reasoning and acting pattern for step-by-step problem solving
- **Verbose Execution**: Detailed logging of agent's thinking process and actions

## Prerequisites

- Python 3.7+
- OpenAI API Key
- WeatherStack API Key (included in the code)

## Installation

1. Install required packages:
```bash
pip install langchain-openai langchain-community langchain-core requests duckduckgo-search
```

2. Set up your OpenAI API key:
```python
import os
os.environ["OPENAI_API_KEY"] = "your-openai-api-key-here"
```

## Project Structure

```
agents_in_langchain.ipynb
├── Setup and Dependencies
├── Tool Definitions
│   ├── DuckDuckGo Search Tool
│   └── Weather Data Tool
├── Agent Configuration
│   ├── LLM Initialization
│   ├── ReAct Prompt Setup
│   └── Agent Creation
└── Example Usage
```

## Code Components

### 1. Search Tool
Uses DuckDuckGo search to find information on the web:
```python
from langchain_community.tools import DuckDuckGoSearchRun
search_tool = DuckDuckGoSearchRun()
```

### 2. Weather Tool
Custom tool to fetch weather data:
```python
@tool
def get_weather_data(city: str) -> str:
    """Fetches current weather data for a given city"""
    # Implementation using WeatherStack API
```

### 3. ReAct Agent
Creates an agent using the ReAct framework:
```python
agent = create_react_agent(
    llm=llm,
    tools=[search_tool, get_weather_data],
    prompt=prompt
)
```

## Usage Example

The notebook demonstrates a complex query that requires multiple steps:

**Query**: "Find the capital of Madhya Pradesh, then find its current weather condition"

**Agent's Process**:
1. **Thought**: Need to find capital first, then check weather
2. **Action**: Search for "capital of Madhya Pradesh"
3. **Observation**: Found that Bhopal is the capital
4. **Action**: Get weather data for Bhopal
5. **Observation**: Retrieved current weather conditions
6. **Final Answer**: Combined both pieces of information

## Sample Output

```
The capital of Madhya Pradesh is Bhopal, and the current weather condition 
in Bhopal is partly cloudy with a temperature of 40°C.
```

## Key Features of the Implementation

### ReAct Framework
- **Reasoning**: Agent thinks through the problem step by step
- **Acting**: Takes specific actions using available tools
- **Observation**: Processes results from each action
- **Iteration**: Continues until the problem is solved

### Verbose Execution
The agent provides detailed logs showing:
- Internal reasoning process
- Tool selections and inputs
- Results from each action
- Final synthesis of information

### Tool Integration
- **Web Search**: Real-time information retrieval
- **Weather API**: Current weather conditions
- **Extensible**: Easy to add more tools

## Configuration Options

### Agent Executor Settings
```python
agent_executor = AgentExecutor(
    agent=agent,
    tools=[search_tool, get_weather_data],
    verbose=True  # Shows detailed execution steps
)
```

### Available Tools
- `duckduckgo_search`: Web search functionality
- `get_weather_data`: Weather information retrieval

## API Keys and Configuration

1. **OpenAI API Key**: Required for the language model
2. **WeatherStack API Key**: Included in the code for weather data

## Error Handling

The agent includes built-in error handling for:
- API failures
- Invalid city names
- Network connectivity issues
- Malformed queries

## Extending the Project

### Adding New Tools
```python
@tool
def your_custom_tool(parameter: str) -> str:
    """Description of what your tool does"""
    # Your implementation here
    return result
```

### Modifying the Prompt
You can customize the ReAct prompt by:
- Pulling different prompts from LangChain Hub
- Creating custom prompts for specific use cases
- Adjusting the reasoning patterns

## Best Practices

1. **Tool Design**: Keep tools focused and single-purpose
2. **Error Handling**: Include proper error handling in custom tools
3. **Prompt Engineering**: Test different prompts for better performance
4. **Verbose Mode**: Use verbose mode for debugging and understanding agent behavior

## Troubleshooting

### Common Issues
- **API Key Errors**: Ensure all API keys are properly set
- **Network Issues**: Check internet connectivity for external API calls
- **Rate Limiting**: Be aware of API rate limits

### Debug Tips
- Enable verbose mode to see agent's reasoning
- Test individual tools separately
- Check API responses manually

## License

This project is for educational and demonstration purposes.

## Contributing

Feel free to extend this project by:
- Adding new tools
- Improving error handling
- Optimizing performance
- Adding new use cases

## Contact

For questions or improvements, please create an issue or submit a pull request.