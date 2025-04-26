# RAG

## RAG Embedding Options (Post-chunking) in LangChain — Categorized

| Category                           | Providers / Methods                                                                 | Requires API Key | Downloads Model Locally | Notes                                                                 |
|------------------------------------|--------------------------------------------------------------------------------------|------------------|---------------------------|-----------------------------------------------------------------------|
| 🛰️ Cloud-based API Providers       | `OpenAIEmbeddings`, `CohereEmbeddings`, `AzureOpenAIEmbeddings`, `VertexAIEmbeddings`, `BedrockEmbeddings` | ✅ Yes           | ❌ No                    | Remote proprietary APIs. Fast, scalable, paid beyond free tiers.     |
| 🧠 Local Inference (Downloaded)    | `HuggingFaceEmbeddings`, `InstructorEmbedding`, `transformers` (custom), `llama-cpp` | ❌ No            | ✅ Yes                   | Fully local, private. Requires downloading models and compute.        |
| ☁️ Hosted Open-Source APIs         | `HuggingFaceInferenceAPIEmbeddings`, Together AI, Replicate (custom clients)        | ✅ Yes           | ❌ No                    | Hosted inference of open models. Slower but avoids local setup.      |
| ⚙️ Local Wrappers / CLI Simplicity | `Ollama`                                                                             | ❌ No            | ✅ Yes (on first run)    | Simplified local use. Wraps `llama.cpp`. Easy to start with.         |

