```mermaid
graph TD
    Remote[Remote User]
    IoT[IoT Devices]
    Admin[Admin Workstation]

    subgraph Edge[Access Point / Router]
        WG[WireGuard VPN]
    end

    subgraph DockerHost[Ubuntu Linux Server (Docker Host)]
        PiHole[Pi-hole DNS]
        NPM[Nginx Proxy Manager]
        Paperless[Paperless-ngx]
        Immich[Immich]
        Mosquitto[Mosquitto MQTT]
        TasmotaSaver[Tasmota Power Saver]
        LLMPower[LocalLLM Power Manager - WOL + SSH + Shutdown]
    end

    subgraph AIHost[Debian GPU Local AI Machine]
        Ollama[Ollama]
        Jupyter[Jupyter]
    end

    Remote -->|VPN tunnel| WG
    WG -->|LAN access| NPM
    WG -->|DNS via Pi-hole| PiHole

    PiHole -->|DNS resolution| NPM
    NPM -->|Reverse proxy| Paperless
    NPM -->|Reverse proxy| Immich

    IoT -->|MQTT| Mosquitto
    Mosquitto --> TasmotaSaver

    LLMPower -->|Wake on LAN| AIHost
    LLMPower -->|Remote power control| AIHost

    Admin -->|Direct admin access| Ollama
    Admin -->|Direct admin access| Jupyter

    classDef edge fill:#ECFEFF,stroke:#0891B2,stroke-width:1.5px,color:#0F172A;
    classDef docker fill:#EEF2FF,stroke:#4338CA,stroke-width:1.5px,color:#0F172A;
    classDef ai fill:#ECFCCB,stroke:#4D7C0F,stroke-width:1.5px,color:#0F172A;
    classDef user fill:#FFF7ED,stroke:#C2410C,stroke-width:1.5px,color:#0F172A;

    class WG edge;
    class PiHole,NPM,Paperless,Immich,Mosquitto,TasmotaSaver,LLMPower docker;
    class Ollama,Jupyter ai;
    class Remote,IoT,Admin user;
```
