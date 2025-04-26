# RAG

## RAG Embedding Options (Post-chunking) in LangChain — Categorized
Category | Providers / Methods | Requires API Key | Downloads Model Locally | Notes
🛰️ Cloud-based API Providers | OpenAIEmbeddings, CohereEmbeddings, AzureOpenAIEmbeddings, VertexAIEmbeddings, BedrockEmbeddings | ✅ Yes | ❌ No | Remote, proprietary APIs. Fast and scalable. Usually paid.
🧠 Local Inference (Downloaded Models) | HuggingFaceEmbeddings, InstructorEmbedding, transformers (custom), llama-cpp | ❌ No | ✅ Yes | Fully offline and private. Requires downloading and more compute resources.
☁️ Cloud-hosted Open-Source APIs | HuggingFaceInferenceAPIEmbeddings, custom HTTP clients (e.g., Together AI, Replicate) | ✅ Yes | ❌ No | Uses hosted open-source models. No local storage, slower, often has a free tier.
⚙️ Local Wrappers / Simplified Local Use | Ollama | ❌ No | ✅ Yes (on first run) | Simple CLI for local models. Wraps llama.cpp. Good for quick local testing.
