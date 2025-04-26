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


<--------------------------------------------------------------------------------------------------------------------------------------------------------------------->


# Advanced RAG
* use filter to get relevant document
* use bm25 for hybrid search
* use reranking
* HPT chunksize and chunkoverlapp and chunking method





## for llama ccp
## installation issue can be overcome by manually donwloading c++ compiler

**1. Use torch_dtype=torch.float16 (if supported)** 
Even on CPU, using float16 instead of float32:

✅ Halves memory usage
✅ Speeds up inference
from transformers import pipeline, AutoModelForSeq2SeqLM, AutoTokenizer
model_name = "google/flan-t5-base"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSeq2SeqLM.from_pretrained(
    model_name,
    torch_dtype="auto",  # Will pick float16 or float32 automatically
    device_map="auto"    # CPU or GPU automatically
)
pipe = pipeline(
    "text2text-generation",
    model=model,
    tokenizer=tokenizer,
    max_length=1024,
    temperature=0.3,
    device=-1,  # Force CPU
)


**2. Enable torch.compile() (PyTorch 2.0+ only)**
If you have PyTorch 2.0+, you can just-in-time compile your model for better performance.
import torch
model = torch.compile(model)
✅ This can give 10–30% speed boost on CPU.

**3. Set torch.set_num_threads()**
Use all CPU cores smartly:
import torch
torch.set_num_threads(8)

**4. Use max_new_tokens instead of max_length**
⚡ Safer to control how much output is generated:
pipe = pipeline(
    "text2text-generation",
    model=model,
    tokenizer=tokenizer,
    max_new_tokens=256,  # Instead of max_length=1024
    temperature=0.3,
    device=-1,
)
max_length = input + output tokens

max_new_tokens = only output tokens ✅ Faster and less memory needed
