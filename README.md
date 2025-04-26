# RAG

## RAG Embedding Options (Post-chunking) in LangChain — Categorized

| Category                           | Providers / Methods                                                                 | Requires API Key | Downloads Model Locally | Notes                                                                 |
|------------------------------------|--------------------------------------------------------------------------------------|------------------|---------------------------|-----------------------------------------------------------------------|
| 🛰️ Cloud-based API Providers       | `OpenAIEmbeddings`, `CohereEmbeddings`, `AzureOpenAIEmbeddings`, `VertexAIEmbeddings`, `BedrockEmbeddings` | ✅ Yes           | ❌ No                    | Remote proprietary APIs. Fast, scalable, paid beyond free tiers.     |
| 🧠 Local Inference (Downloaded)    | `HuggingFaceEmbeddings`, `InstructorEmbedding`, `transformers` (custom), `llama-cpp` | ❌ No            | ✅ Yes                   | Fully local, private. Requires downloading models and compute.        |
| ☁️ Hosted Open-Source APIs         | `HuggingFaceInferenceAPIEmbeddings`, Together AI, Replicate (custom clients)        | ✅ Yes           | ❌ No                    | Hosted inference of open models. Slower but avoids local setup.      |
| ⚙️ Local Wrappers / CLI Simplicity | `Ollama`                                                                             | ❌ No            | ✅ Yes (on first run)    | Simplified local use. Wraps `llama.cpp`. Easy to start with.         |



**llama-cpp**: is specifically built to run models from the LLaMA family (e.g., LLaMA-2, LLaMA-7B), and is a great option for running LLMs locally on CPUs and GPUs.
Speed: Llama-cpp is optimized for low latency on CPU. It's known for providing fast local inference of LLaMA models without relying on external APIs.
Use Case: Mainly used for generating text (not embeddings) and small to medium models.

**Ollama**: is a software tool that makes it super easy to run large language models (LLMs) locally using LLaMA models or other models that Ollama supports.
It comes with an easy-to-use CLI (command-line interface) and local HTTP API, so it's far easier to interact with, especially for integrating it with applications or systems.

**Pickle files safety issue**:
When you call FAISS.load_local(), LangChain internally uses pickle to load the saved FAISS index metadata.
Pickle files can be dangerous because they can execute arbitrary Python code during loading.
For safety, LangChain forces you to explicitly allow dangerous deserialization if you trust the file you're loading.
