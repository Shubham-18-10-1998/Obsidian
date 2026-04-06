 

Google AI Studio : Build, can build many things

Moving from normal searches to natural language searches.

# Introduction

Openrouter.ai : helps know models for each category

To communicate we have three ways
- Image
	- Diffusion Models
- Text
- Audio


# Machine Learning
Lot of data from which i want the machine to learn patterns.
- Structured or unstructured data
- Prediction or classification

Mostly for structured data 

Teachable to train model for classification.

Pattern Recognition
input data -> Train -> Predict -> Output

Structured Data, Clear Input

# NLP
Attention is all you need paper.
- Letting machine understand natural language.
- Model utilised internet to learn about language.

Mostly for unstructured data.

Understanding text
Text -> Tokenization -> Model -> Labeled Output

Also can be for clustering

Deterministic text parsing


# GenAI
So far everything was using already seen data to decide. That changed with Gen-AI. So it can create things never seen before as data.

Creating new Content

Input -> LLM -> New Output

Open-ended, reasoning or creative tasks

n8n for back-end.


Memory common for all
- LLM Responder - Knowledge cutoff (LLM + prompt)
- RAGs (Connect your own data) (LLM + Prompt + Data)
	- Since fine-tuning is expensive we use RAGs where we give our data
- Agents - (RAGs + tools)
	- Connects through API or MCPs

## LLM
- Token = word fragment
	- We have a finite word set in English
	- Everything based on tokens
	- The token has an associated number to it (Mapping)
- Embedding = vector representation
	- Bring numerical 
	- Now the vector we get, its essentially its location in the space which explains it meaning to the machine by having this index. Each individual value is like an adjective or an indicator to explain the context of the word. Hence closer vector means similar meanings.
	- https://jalammar.github.io/illustrated-word2vec/ for reference.
- Attention = relevance weighting
	- This is the reason for prompt engineering as it decides the kind of output

Input -> Tokenization -> Embedding -> Attention -> Output (Prediction)

GPT is an agent

