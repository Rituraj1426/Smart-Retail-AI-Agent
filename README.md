# Smart-Retail-AI-Agent
# 🛒 Smart Retail AI Agent (RAG Architecture on Azure)

Welcome to my first Generative AI project! This repository contains the architecture details, system design, and dataset used to build an Enterprise-Grade Retail AI Assistant (inspired by Flipkart/Blinkit) using **Retrieval-Augmented Generation (RAG)** on Microsoft Azure.

## 🌟 Project Overview
Generic AI models (like base GPT-4) are powerful, but they lack knowledge of proprietary business data and often hallucinate. The goal of this project was to engineer a **Specialized AI Agent** that acts as a retail assistant. By utilizing a RAG pipeline, the AI is "grounded" in a specific retail catalog, ensuring it only recommends products that actually exist in the inventory, complete with accurate pricing and descriptions.

## 🚀 Key Features
* **Hallucination-Free Responses:** Grounded entirely in a provided custom dataset.
* **Semantic Vector Search:** Users can search using natural language (e.g., "running gear" finds "sneakers") instead of relying on exact keyword matches.
* **Strict Persona Constraints:** Engineered with system prompts to politely decline non-retail questions, ensuring brand safety.

## 🛠️ Tech Stack
* **Cloud Platform:** Azure AI Foundry
* **Foundation Model:** Azure OpenAI GPT-4o
* **Embedding Model:** `text-embedding-ada-002` (for vectorizing product data)
* **Vector Database:** Azure AI Search
* **Storage:** Azure Blob Storage

## 🏗️ System Architecture

The application follows a standard enterprise RAG workflow:

```text
======================================================================
              SMART RETAIL AI AGENT - RAG ARCHITECTURE
======================================================================

PART 1: DATA INGESTION (Building the "Memory")

  [Flipkart Data]        [Azure Blob]          [Azure AI Search]
    (TXT/CSV)    ----->   (Storage)   ----->    (Vector Index)
                                                      ^
                                                      | (Creates Vectors)
                                              [Embedding Model]
                                            (text-embedding-ada-002)

----------------------------------------------------------------------

PART 2: USER CHAT FLOW (The "Brain" at Work)

                            (2) Search Query
                            +----------------> [Azure AI Search]
                            |                         |
  [User]                    |                         v (3) Top Results
  "I need     (1) Query     |                   [Product Context]
   shoes"  ---------------> |                         |
                            |                         | (4) Query + Context
  [Chat UI] <---------------+                         v
              (5) Answer    |                   [Azure OpenAI]
             "We have Nike" +-----------------     (GPT-4o)

======================================================================
