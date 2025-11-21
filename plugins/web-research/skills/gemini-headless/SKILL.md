---
name: gemini-headless
description: Web research and content analysis using Google Gemini CLI in headless mode. Use this skill when you need to analyze web content, process research queries, or synthesize information from multiple sources using the gemini -p flag for automation and scripting.
---

# Gemini Headless CLI

## Overview
Gemini CLI is an AI CLI that has various capabilities, but it excels at synthesizing large amounts of information from the web and from local codebase files. This skill focuses on using Gemini CLI for web research. 

- You MUST explicitly instruct Gemini CLI to "do web research", "do web search", "do deep web research", etc. else it will default to answering the questions using it's internal LLM training alone (which we don't want)
- Gemini has excellent web search capabilities, we always outsource web search as well as fetching and analyzing the search results to Gemini CLI.


## Core Usage

The `-p` or `--prompt` flag enables headless mode for non-interactive automation:

```bash
gemini -p "Your query here"
cat file.txt | gemini -p "Analyze this"
gemini -p "Query" > output.txt
gemini -p "Query" --output-format json | jq '.response'
```

## Input Methods

- **Direct prompts:** `gemini -p "Conduct web research to answer this question ..."`
- **Stdin piping:** `cat file.txt | gemini -p "Analyze"`
- **Command chains:** `curl https://example.com | gemini -p "Summarize"`
- **Multiple files:** `cat file1.txt file2.txt | gemini -p "Compare"`
- **With grep:** `grep "ERROR" log.txt | gemini -p "Identify patterns"`

## Output Formats

- **Text (default):** `gemini -p "Query"` → human-readable text
- **JSON:** `gemini -p "Query" --output-format json` → structured JSON with metadata
- **Streaming JSON:** `gemini -p "Query" --output-format stream-json` → newline-delimited JSON for long content

Parse JSON with jq:
```bash
gemini -p "Query" --output-format json | jq '.response'
```

## Resources

- [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Headless Mode Guide](https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/headless.md)
- [JSON Output Documentation](https://github.com/google-gemini/gemini-cli/docs)
