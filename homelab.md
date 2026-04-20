```mermaid

graph TD

    subgraph Physical
        Server1[Docker Host]
        AI[AI Server]
    end

    subgraph Services
        PiHole[Pi-hole]
        Paperless[Paperless-ngx]
        Immich[Immich]
        LLM[Ollama]
    end

    User --> VPN
    VPN --> Server1

    Server1 --> PiHole
    Server1 --> Paperless
    Server1 --> Immich

    AI --> LLM
    Server1 --> AI

```
