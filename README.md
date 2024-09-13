# LangGraph Data Enrichment Template

[![CI](https://github.com/langchain-ai/data-enrichment/actions/workflows/unit-tests.yml/badge.svg)](https://github.com/langchain-ai/data-enrichment/actions/workflows/unit-tests.yml)
[![Integration Tests](https://github.com/langchain-ai/data-enrichment/actions/workflows/integration-tests.yml/badge.svg)](https://github.com/langchain-ai/data-enrichment/actions/workflows/integration-tests.yml)

This is a starter project to help you get started with developing a data enrichment agent using [LangGraph](https://github.com/langchain-ai/langgraph) in [LangGraph Studio](https://github.com/langchain-ai/langgraph-studio).

![Graph view in LangGraph studio UI](./static/studio.png)

It contains an example graph exported from `src/enrichment_agent/graph.py` that implements a research assistant capable of automatically gathering information on various topics from the web.

## What it does

The enrichment agent:

1. Takes a research **topic** and requested **template_schema** as input
2. Searches the web for relevant information
3. Reads and extracts key details from websites
4. Organizes the findings into the requested structured format
5. Validates the gathered information for completeness and accuracy

By default, it's set up to gather information based on the user-provided schema passed through the `template_schema` key in the state.

## Getting Started

Assuming you have already [installed LangGraph Studio](https://github.com/langchain-ai/langgraph-studio?tab=readme-ov-file#download), to set up:

1. Create a `.env` file.

```bash
cp .env.example .env
```

2. Define required API keys in your `.env` file.

The primary [search tool](./src/enrichment_agent/tools.py) [^1] used is [Tavily](https://tavily.com/). Create an API key [here](https://app.tavily.com/sign-in).

<!--
Setup instruction auto-generated by `langgraph template lock`. DO NOT EDIT MANUALLY.
-->

Set up your LLM API keys. This repo defaults to using [Claude](https://console.anthropic.com/login).

<!--
End setup instructions
-->

3. Customize whatever you'd like in the code.
4. Open the folder LangGraph Studio!

## How to customize

1. **Customize research targets**: Provide a custom `template_schema` when calling the graph to gather different types of information.
2. **Select a different model**: We default to anthropic (sonnet-35). You can select a compatible chat model using `provider/model-name` via configuration. Example: `openai/gpt-4o-mini`.
3. **Customize the prompt**: We provide a default prompt in [prompts.py](./src/enrichment_agent/prompts.py). You can easily update this via configuration in the studio.

You can also quickly extend this template by:

- Adding new tools and API connections in [tools.py](./src/enrichment_agent/tools.py). These are just any python functions.
- Adding additional steps in [graph.py](./src/enrichment_agent/graph.py). Concerned about hallucinatio

## Development

While iterating on your graph, you can edit past state and rerun your app from past states to debug specific nodes. Local changes will be automatically applied via hot reload. Try adding an interrupt before the agent calls tools, updating the default system message in `src/enrichment_agent/utils.py` to take on a persona, or adding additional nodes and edges!

Follow up requests will be appended to the same thread. You can create an entirely new thread, clearing previous history, using the `+` button in the top right.

You can find the latest (under construction) docs on [LangGraph](https://github.com/langchain-ai/langgraph) here, including examples and other references. Using those guides can help you pick the right patterns to adapt here for your use case.

LangGraph Studio also integrates with [LangSmith](https://smith.langchain.com/) for more in-depth tracing and collaboration with teammates.

<!--
Configuration auto-generated by `langgraph template lock`. DO NOT EDIT MANUALLY.
{
  "config_schemas": {
    "agent": {
      "type": "object",
      "properties": {
        "model_name": {
          "type": "string",
          "default": "claude-3-5-sonnet-20240620"
        },
        "max_search_results": {
          "type": "integer",
          "default": 10
        },
        "max_info_tool_calls": {
          "type": "integer",
          "default": 3
        },
        "max_loops": {
          "type": "integer",
          "default": 6
        }
      }
    }
  }
}
-->

[^1]: https://python.langchain.com/v0.2/docs/concepts/#tools
