# Annotated LangChain Tutorial

Annotated, hands-on walkthrough of LangChain's core patterns — LCEL chains, RAG pipelines, and tool-calling agents — built while learning LangChain as part of my path toward becoming an Applied AI/ML Engineer.

Every example is adapted from the original tutorial to run on a **free and local stack**: Gemini instead of OpenAI, and a local embedding model instead of a paid embeddings API. No OpenAI dependency anywhere in this repo.

## Stack Used

- **LLM:** Gemini (`gemini-3.5-flash-lite`) via `langchain-google-genai`
- **Embeddings:** `Qwen3-Embedding-0.6B` (local, via HuggingFace) — no API cost, runs on-device
- **Vector store:** Chroma
- **Framework:** LangChain (LCEL)

## What's Covered

- **Build 1 — Simple Chain:** `prompt | llm | parser` using LCEL, the core pipe-based composition pattern
- **Build 2 — RAG Pipeline:** Chroma vector store, retriever, manual context formatting, and the full retrieve-then-generate flow
- **Build 3 — Tool-Calling Agent:** `@tool`-decorated functions, `bind_tools()`, reading `tool_calls`, and closing the loop with `ToolMessage` for a full request → tool execution → final answer cycle
- Architecture notes on how LCEL executes under the hood (streaming, batching, the Runnable interface)
- Streaming responses, provider switching, and parallel execution with `RunnableParallel`
- Trade-off notes: LangChain vs raw SDK vs Pydantic AI, and LangChain vs LlamaIndex

## Setup

Clone the repo and install dependencies:

```
pip install langchain langchain-core langchain-google-genai langchain-chroma chromadb sentence-transformers python-dotenv
```

**API key setup:** This project uses a `.env` file to store the Gemini API key — the `.env` file itself is **not included** in this repo (it's gitignored) since it contains a private key. To run the notebooks yourself:

1. Create a file named `.env` in the project root
2. Add your Gemini API key to it:
   ```
   GOOGLE_API_KEY=your_actual_key_here
   ```
3. Get a free key from [Google AI Studio](https://aistudio.google.com/apikey)
4. The notebooks load it via `python-dotenv`:
   ```python
   from dotenv import load_dotenv
   load_dotenv()
   ```

No key is needed for the embedding model — `Qwen3-Embedding-0.6B` runs locally via HuggingFace and downloads automatically on first use.

## Related Annotated Repos

Part of a broader learning-in-public series covering the RAG and Vector DB path:

- [Annotated-HuggingFace-LLM-Course](https://github.com/rehan-ml/Annotated-HuggingFace-LLM-Course)
- [Annotated-VectorDB-ChromaDB-Course](https://github.com/rehan-ml/Annotated-VectorDB-ChromaDB-Course)
- [Annotated-LlamaIndex-Tutorial](https://github.com/rehan-ml/Annotated-LlamaIndex-Tutorial)

## Notes

Every code example includes theory-first explanations and inline comments — written to be understandable standalone, without needing the original tutorial as context.
