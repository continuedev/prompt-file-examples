name: claude-prompt-caching
description: Talk to the Claude prompt caching docs
---
<system>
Prompt caching, which enables developers to cache frequently used context between API calls, is now available on the Anthropic API. With prompt caching, customers can provide Claude with more background knowledge and example outputs—all while reducing costs by up to 90% and latency by up to 85% for long prompts. Prompt caching is available today in public beta for Claude 3.5 Sonnet, Claude 3 Opus, and Claude 3 Haiku.

### When to use prompt caching

Prompt caching can be effective in situations where you want to send a large amount of prompt context once and then refer to that information repeatedly in subsequent requests, including:

* **Conversational agents:** Reduce cost and latency for extended conversations, especially those with long instructions or uploaded documents.
* **Coding assistants:** Improve autocomplete and codebase Q&A by keeping a summarized version of the codebase in the prompt.
* **Large document processing:** Incorporate complete long-form material including images in your prompt without increasing response latency.
* **Detailed instruction sets:** Share extensive lists of instructions, procedures, and examples to fine-tune Claude's responses. Developers often include a few examples in their prompt, but with prompt caching you can get even better performance by including dozens of diverse examples of high quality outputs.
* **Agentic search and tool use:** Enhance performance for scenarios involving multiple rounds of tool calls and iterative changes, where each step typically requires a new API call.
* **Talk to books, papers, documentation, podcast transcripts, and other long-form content:** Bring any knowledge base alive by embedding the entire document(s) into the prompt, and letting users ask it questions.

Early customers have seen substantial speed and cost improvements with prompt caching for a variety of use cases—from including a full knowledge base to 100-shot examples to including each turn of a conversation in their prompt.

| **Use case**                                                            | **Latency w/o caching (time to first token)** | **Latency w/ caching (time to first token)** | **Cost reduction** |
| ----------------------------------------------------------------------- | --------------------------------------------- | -------------------------------------------- | ------------------ |
| Chat with a book (100,000 token cached prompt) \[1\]                    | 11.5s                                         | 2.4s (-79%)                                  | \-90%              |
| Many-shot prompting (10,000 token prompt) \[1\]                         | 1.6s                                          | 1.1s (-31%)                                  | \-86%              |
| Multi-turn conversation (10-turn convo with a long system prompt) \[2\] | \~10s                                         | \~2.5s (-75%)                                | \-53%              |

### How we price cached prompts

Cached prompts are priced based on the number of input tokens you cache and how frequently you use that content. Writing to the cache costs 25% more than our base input token price for any given model, while using cached content is significantly cheaper, costing only 10% of the base input token price.

| **Claude 3.5 Sonnet**Our most intelligent model to date200K context window | **Input**$3 / MTok    | **Prompt caching**$3.75 / MTok - Cache write $0.30 / MTok - Cache read  | **Output** $15 / MTok  |
| -------------------------------------------------------------------------- | --------------------- | ----------------------------------------------------------------------- | ---------------------- |
| **Claude 3 Opus**Powerful model for complex tasks200K context window       | **Input**$15 / MTok   | **Prompt caching**$18.75 / MTok - Cache write$1.50 / MTok - Cache read  | **Output**$75 / MTok   |
| **Claude 3 Haiku**Fastest, most cost-effective model200K context window    | **Input**$0.25 / MTok | **Prompt caching**$0.30 / MTok \- Cache write $0.03 / MTok - Cache read | **Output**$1.25 / MTok |

### Customer spotlight: Notion

[Notion](https://www.notion.so/product/ai) is adding prompt caching to Claude-powered features for its AI assistant, Notion AI. With reduced costs and increased speed, Notion is able to optimize internal operations and create a more elevated and responsive user experience for their customers.

> We're excited to use prompt caching to make Notion AI faster and cheaper, all while maintaining state-of-the-art quality.

— Simon Last, Co-founder at Notion

### Get started

To start using the prompt caching public beta on the Anthropic API, explore our [documentation](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) and [pricing page](https://www.anthropic.com/pricing#anthropic-api).

#### Footnotes

\[1\] Based on using Claude 3.5 Sonnet and measured with 100-200 token dynamic instructions after the cached prompt. 

\[2\] Based on using Claude 3.5 Sonnet and measured as a 5000 token system prompt, with \~100 token user messages and \~2000 token responses from Claude. Cost reduction is measured across the whole conversation, latency reduction is reported for the median message.

URL: https://www.anthropic.com/news/prompt-caching how do i cache a prompt

==========================================================================
==========================================================================
Completion:

To cache a prompt using the Anthropic API, follow these steps:

### 1. Understand the Concepts:
- **Writing to the Cache:** This involves storing your prompt context in the cache.
- **Using Cached Content:** This involves retrieving and utilizing the cached prompt context in subsequent requests.

### 2. Setup:
Ensure you have access to the Anthropic API and appropriate credentials.

### 3. Write to the Cache:
Use the API to store frequently used prompt contexts. Here's an example of how you might do this:

```python
import anthropic

# Initialize the API client
client = anthropic.Client(api_key="your_api_key")

# Define the content to cache
prompt_context = """
# Include your large prompt context here
# For example: a long document, detailed instructions, examples, etc.
"""

# Cache the content
response = client.cache.write(content=prompt_context)

# Get the cache key from the response
cache_key = response["key"]
```

### 4. Use Cached Content:
In subsequent API calls, use the cached content by referencing the cache key.

```python
# Define your dynamic prompt part
dynamic_prompt = """
# Your current request or specific user query
"""

# Use the cached content
response = client.chat(
    model="claude-3.5-sonnet",
    cache={"key": cache_key},
    prompt=dynamic_prompt
)

# Process the response
print(response["completion"])
```

### 5. Pricing Considerations:
- **Writing Costs:** Writing to the cache costs 25% more than the base input token price.
- **Reading Costs:** Using cached content is cost-effective, costing only 10% of the base input token price.

### Example Code:

Here’s a complete example in one go:

```python
import anthropic

# Initialize the API client
client = anthropic.Client(api_key="your_api_key")

# Step 1: Write to the Cache
prompt_context = """
# Include a large prompt context here
"""

response = client.cache.write(content=prompt_context)
cache_key = response["key"]

# Step 2: Use Cached Content
dynamic_prompt = """
# Include current dynamic prompt part here
"""

response = client.chat(
    model="claude-3.5-sonnet",
    cache={"key": cache_key},
    prompt=dynamic_prompt
)

print(response["completion"])
```

### Documentation:
Refer to [Anthropic's documentation](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) for more detailed information and specific API calls.

By following these steps, you can effectively utilize prompt caching to optimize performance and costs when using the Anthropic API.
</system>

{{{ input }}}
