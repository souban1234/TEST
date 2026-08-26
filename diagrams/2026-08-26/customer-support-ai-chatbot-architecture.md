# Customer Support AI Chatbot - System Architecture

```mermaid
flowchart LR
  user([Customer / User]) -->|1. submits query| ui[Chat UI / Web or Mobile App]
  ui -->|2. sends message| api[Chatbot API]

  subgraph platform[AI Chatbot Platform]
    api --> orchestrator[Conversation Orchestrator]
    orchestrator -->|3. search request| retriever[Knowledge Retriever]
    retriever -->|4. query relevant content| kb[(Knowledge Base<br/>FAQs, Docs, Policies, Tickets)]
    kb -->|5. matching snippets| retriever
    retriever -->|6. retrieved context| prompt[Prompt Builder<br/>User Query + Retrieved Context]
    prompt -->|7. grounded prompt| llm[LLM Response Generator]
    llm -->|8. generated answer| orchestrator
  end

  orchestrator -->|9. final response| api
  api -->|10. return answer| ui
  ui -->|11. display answer| user

  logs[(Logs / Feedback / Analytics)]
  orchestrator -.->|optional monitoring| logs

  classDef actor fill:#fff7ed,stroke:#ea580c,stroke-width:2px,color:#111827
  classDef app fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#111827
  classDef data fill:#f0fdf4,stroke:#16a34a,stroke-width:2px,color:#111827
  classDef ai fill:#fdf4ff,stroke:#a21caf,stroke-width:2px,color:#111827
  classDef ops fill:#f1f5f9,stroke:#64748b,stroke-width:2px,color:#111827

  class user actor
  class ui,api,orchestrator,retriever,prompt app
  class kb data
  class llm ai
  class logs ops
```

## Flow

1. The customer submits a support query through the chat UI.
2. The chatbot API passes the message to the conversation orchestrator.
3. The orchestrator searches the knowledge base through a retriever component.
4. Relevant FAQ/document/ticket snippets are returned.
5. The prompt builder combines the user query with retrieved context.
6. The LLM generates a grounded customer-support response.
7. The answer is returned through the API and displayed to the customer.
