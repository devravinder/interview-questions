# AI Terms Explained (for Web Developers)

## 1. AI (Artificial Intelligence)
Software that can make decisions or predictions like a human would.  
- Example: Gmail spam filter → decides if an email is spam.  
- Even simple rules + ML models count as AI.

---

## 2. Generative AI
A type of AI that **creates new content** instead of just analyzing.  
- Examples:  
  - ChatGPT → generates text  
  - MidJourney / DALL·E → generates images  
- Think of it as **auto-complete on steroids**.

---

## 3. LLM (Large Language Model)
The **engine under the hood** of most generative AI chatbots.  
- A neural network trained on massive text data.  
- Examples: GPT-4, Claude, Gemini.  
- For developers: like a **super-powerful text API** → input = prompt, output = response.

---

## 4. RAG (Retrieval-Augmented Generation)
Technique to combine **search + LLM**.  
- Flow:  
  1. User asks a question  
  2. System searches database/knowledge base  
  3. Relevant info is passed to LLM  
  4. LLM answers based on **real data**  
- Example: A chatbot that answers using your company’s FAQs/docs.

---

## 5. MCP (Model Context Protocol)
An **open protocol** (from OpenAI) for tools, apps, and AI models to talk in a standard way.  
- Think of it like **REST for AI**.  
- Instead of custom integrations, AI can connect with GitHub, databases, or Slack consistently.

---

## 6. Agentic AI (AI Agents)
Goes beyond simple Q&A → AI can **plan and act**.  
- Capabilities:  
  - Break tasks into steps  
  - Call APIs  
  - Write & run code  
  - Remember context  
- Example: “Book me a flight, pay for it, and add details to my calendar.”  
- For devs:  
  - **LLM = function call** (input → output)  
  - **Agent = worker service** that uses tools & APIs to finish a task.

---

## ✅ Quick Summary
- **AI** → broad idea of machines acting smart  
- **Generative AI** → creates new content  
- **LLM** → the engine for text generation  
- **RAG** → search + LLM → answers from real data  
- **MCP** → protocol for AI ↔ tools integration  
- **Agentic AI** → AI that plans, uses APIs, and takes actions
