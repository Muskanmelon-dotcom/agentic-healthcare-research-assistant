# agentic-healthcare-research-assistant
Multi-agent AI system for healthcare research analysis using LangChain and LangGraph
# Agentic Healthcare AI Research Assistant

A multi-agent system I built for analyzing healthcare AI research papers and generating evidence-based recommendations.

## What It Does

This system helps researchers quickly analyze healthcare AI literature by:
- Searching through research papers to find relevant evidence
- Critically evaluating study methodology and limitations
- Generating actionable deployment recommendations

I built it to help with my own literature reviews in digital pathology and genomics research, but the architecture works for any research domain.

## Architecture

The system uses three specialized agents orchestrated through LangGraph:

**Research Agent**
- Retrieves relevant papers using semantic search (RAG)
- Extracts key findings, study design, and outcomes
- Identifies the most relevant evidence

**Analysis Agent**
- Evaluates research quality (RCT vs observational, sample sizes)
- Assesses internal and external validity
- Flags limitations and potential biases

**Recommendation Agent**
- Synthesizes evidence into deployment recommendations
- Includes evaluation plans and guardrails
- Acknowledges limitations and assumptions

## Implementation

**RAG System:**
- Built from scratch using OpenAI embeddings and cosine similarity
- No heavy frameworks - just numpy and basic math
- Allows full control over retrieval logic

**Multi-Agent Workflow:**
- LangGraph state machine with conditional routing
- Agents share state and pass information between steps
- Can route differently based on confidence scores

**Document Corpus:**
- Currently contains 3 healthcare AI research summaries:
  - Deep learning for histopathology classification
  - Transformer models for splice site prediction  
  - AI-powered pathology report extraction
- Easy to expand by adding more documents

## Tech Stack

- Python
- LangChain / LangGraph
- OpenAI (gpt-4o-mini, text-embedding-3-small)
- NumPy

## Performance

Validated the system on test queries:
- Retrieval accuracy: 100% (always finds the right document)
- Factual grounding: 100% (includes key facts from sources)
- vs baseline: 83 percentage point improvement over direct LLM queries

## Why This Approach

I chose a multi-agent architecture instead of a single large prompt because:
- Each agent specializes in one task (research, analysis, recommendations)
- Easier to debug and improve individual components
- Transparent - can inspect reasoning at each step
- Modular - can swap agents or add new ones

The RAG approach ensures responses are grounded in actual research rather than LLM hallucinations.

## Usage
```python
# Ask a research question
result = ask_question("How accurate are deep learning models for cancer diagnosis?")

# Get structured output
print(result['evidence'])        # Research summary
print(result['analysis'])        # Critical evaluation  
print(result['recommendations']) # Actionable advice
```

## Running the Code

**Google Colab (easiest):**
- Open the notebook in Colab
- Add your OpenAI API key to Colab secrets
- Run all cells

**Local:**
```bash
pip install -r requirements.txt
# Set OPENAI_API_KEY environment variable
# Run the notebook
```

## Future Extensions

- Scale corpus to 1000+ papers with PDF ingestion pipeline
- Add web search for recent papers beyond corpus
- Implement conversation memory for multi-turn dialogue
- Deploy as API service with A/B testing for prompt optimization


## License

MIT
