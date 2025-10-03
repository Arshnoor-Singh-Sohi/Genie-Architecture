mermaid```
---
config:
  layout: fixed
---
flowchart TB
 subgraph Legend["📊 LEGEND: Main Flow → | Security ⛔ | Monitoring ⋯⋯"]
        L1["🔵 Phases | 🔴 Security | 🟢 Unity Catalog | 🟡 Compute | 🟣 MLOps | 🔻 Threats"]
  end
 subgraph User["👤 USER INTERFACE LAYER"]
        U1["STEP 1: User submits Natural Language Query"]
        U2["AI/BI Genie Interface"]
        U3["Databricks Assistant in Notebooks/SQL Editor"]
  end
 subgraph Phase1["📥 PHASE 1: Ingestion & Pre-processing"]
        I1["STEP 2: Query Ingestion"]
        I2["STEP 3: ai_fix_grammar Function<br>Grammar/Spelling Normalization"]
        I3["STEP 4: Input Safety Guardrail<br>Llama Guard 2"]
        I4{"STEP 5: Malicious Content<br>Detected?"}
        I5["❌ Block Request<br>Return Error"]
  end
 subgraph Phase2["🔍 PHASE 2: RAG Context Retrieval"]
        R1["STEP 6: Query Unity Catalog Metastore"]
        R2["STEP 7a: Retrieve Schema Information"]
        R3["STEP 7b: Retrieve Column Descriptions"]
        R4["STEP 7c: Retrieve Sample Queries/Examples"]
        R5["STEP 8: Apply User ACL Filtering"]
        R6{"STEP 9: User has<br>Access?"}
        R7["STEP 10: Filter Metadata by Permissions"]
        R8["STEP 11: Genie Space Configuration<br>Domain Expert Annotations"]
        R9["STEP 12: Assemble Context Payload"]
  end
 subgraph Phase3["🤖 PHASE 3: LLM Inference"]
        P1["STEP 13: Construct System Prompt<br>with Constraints"]
        P2["STEP 14: System Prompt Hardening<br>Ignore Override Attempts"]
        P3["STEP 15: Concatenate:<br>Context + System Prompt + User Query"]
        P4["STEP 16: Finalized Inference Prompt"]
        P5["STEP 17: Foundation Model API"]
        P6["STEP 18: LLM Inference<br>Llama3 8B / Azure OpenAI / Custom"]
        P7["STEP 19: Generate SQL/Python Code"]
        P8["STEP 20: Output Safety Filter<br>Llama Guard 2"]
        P9{"STEP 21: Generated Code<br>Contains Harmful<br>Content?"}
        P10["❌ Block Code<br>Return Error"]
  end
 subgraph Phase4A["✅ PHASE 4A: Validation"]
        V1["STEP 22: Security & ACL Validation"]
        V2["STEP 23: Parse Generated SQL/Python"]
        V3["STEP 24: Extract Referenced Tables/Columns"]
        V4["STEP 25: Query Unity Catalog ACLs"]
        V5{"STEP 26: User has READ<br>permission for ALL<br>referenced assets?"}
        V6["❌ Reject Execution<br>Unauthorized Access Attempt"]
        V7["STEP 27: Code Syntax Validation"]
        V8{"STEP 28: Valid SQL/<br>Python Syntax?"}
        V9["❌ Reject - Syntax Error"]
  end
 subgraph ControlPlane["🎛️ CONTROL PLANE - Databricks Managed Cloud"]
        Phase1
        Phase2
        Phase3
        Phase4A
  end
 subgraph Phase4B["⚙️ PHASE 4B: Execution"]
        E1["Serverless Compute"]
        E2["Classic Compute"]
        E3{"STEP 29: Compute<br>Type?"}
        E4["STEP 30: Execute SQL Query"]
        E5["STEP 31: Execute Python Code"]
        E6["STEP 32: Spark Cluster Processing"]
        E7["STEP 33: Access Customer Data<br>within ACL boundaries"]
        E8["STEP 34: Generate Results"]
        E9["STEP 35: Create Visualizations"]
  end
 subgraph ComputePlane["☁️ COMPUTE PLANE - Customer Cloud Account"]
        Phase4B
  end
 subgraph UnityLayer["🛡️ UNITY CATALOG - Governance Layer"]
        UC1["💾 Unity Catalog<br>Metastore"]
        UC2["Data Classification"]
        UC3["Asset Permissions"]
        UC4["Table/Column Descriptions"]
        UC5["Lineage Information"]
        UC6["Access Control Lists ACLs"]
        UC7["Audit Logs"]
  end
 subgraph SecurityFramework["🔐 DATABRICKS AI SECURITY FRAMEWORK - DASF"]
        S1["62 Technical Security Risks"]
        S2["64 Prescriptive Controls"]
        S3["Zero Data Retention ZDR"]
        S4["Model Serving Isolation"]
        S5["Mosaic AI Gateway"]
  end
 subgraph MLOps["📈 MLOps & LLMOps Framework"]
        M1["Continuous Evaluation"]
        M2["User Feedback Collection"]
        M3["Semantic Knowledge Updates"]
        M4["MLflow Experiment Tracking"]
        M5["Prompt Variation Testing"]
        M6["Performance Monitoring"]
        M7["Red Team Testing"]
        M8["Adversarial Testing"]
  end
 subgraph Threats["⚠️ Threat Vectors & Mitigations"]
        T1["Prompt Injection PI Attacks"]
        T2["Schema Inference Attacks"]
        T3["ToxicSQL Backdoors"]
        T4["Unauthorized Data Access"]
        T5["Data Manipulation DDL/DML"]
  end
 subgraph Results["📊 Results & Feedback Loop"]
        RES1["STEP 36: Return Results to User"]
        RES2["STEP 37: Display Tables/Charts"]
        RES3["STEP 38: Automated Visualizations"]
        RES4["STEP 39: Collect User Feedback"]
        RES5["STEP 40: Log Query Performance"]
        RES6["STEP 41: Update Genie Knowledge Base"]
  end
    U1 --> U2 & U3
    U2 --> I1
    U3 --> I1
    I1 --> I2
    I2 --> I3
    I3 --> I4
    I4 -- Yes --> I5
    I5 --> RES1
    I4 -- "No - Safe" --> R1
    R1 --> UC1
    UC1 --> R2 & R3 & R4 & UC2 & UC3 & UC4 & UC5 & UC6 & UC7
    R2 --> R5
    R3 --> R5
    R4 --> R5
    R5 --> R6
    R6 -- Yes --> R7
    R6 -- No --> I5
    R7 --> R8
    R8 --> R9
    R9 --> P1 & P3
    P1 --> P2
    P2 --> P3
    P3 --> P4
    P4 --> P5
    P5 --> P6
    P6 --> P7
    P7 --> P8
    P8 --> P9
    P9 -- Yes --> P10
    P10 --> RES1
    P9 -- "No - Safe" --> V1
    V1 --> V2
    V2 --> V3
    V3 --> V4
    V4 --> UC1 & V5
    V5 -- No --> V6
    V6 --> RES1
    V5 -- Yes --> V7
    V7 --> V8
    V8 -- No --> V9
    V9 --> RES1
    V8 -- Yes --> E3
    E3 -- Serverless --> E1
    E3 -- Classic --> E2
    E1 --> E4 & E5
    E2 --> E4 & E5
    E4 --> E6
    E5 --> E6
    E6 --> E7
    E7 --> E8
    E8 --> E9
    E9 --> RES1
    RES1 --> RES2
    RES2 --> RES3
    RES3 --> RES4
    RES4 --> RES5
    RES5 --> RES6
    RES6 --> M3
    S3 -. Enforces .-> P6
    S4 -. Isolates .-> E6
    S5 -. Manages .-> I3 & P8
    S1 -. Addresses .-> T1 & T2 & T3
    S2 -. Mitigates .-> T4 & T5
    M1 -. Monitors .-> P6
    M2 -. Feeds .-> M3
    M3 -. Updates .-> R8
    M4 -. Tracks .-> P5
    M5 -. Tests .-> P3
    M6 -. Observes .-> E6
    M7 -. Tests .-> I3
    M8 -. Validates .-> V1
    P2 -. Mitigates .-> T1
    I3 -. Blocks .-> T1
    P8 -. Blocks .-> T1
    R5 -. Prevents .-> T2
    V5 -. Blocks .-> T3 & T5
    V5 -. Prevents .-> T4
    UC6 -. Enforces Against .-> T2 & T4
     I3:::securityStyle
     P8:::securityStyle
     V1:::securityStyle
     V5:::securityStyle
     E1:::computeStyle
     E2:::computeStyle
     E3:::computeStyle
     E4:::computeStyle
     E5:::computeStyle
     E6:::computeStyle
     E7:::computeStyle
     UC1:::ucStyle
     UC2:::ucStyle
     UC3:::ucStyle
     UC4:::ucStyle
     UC5:::ucStyle
     UC6:::ucStyle
     UC7:::ucStyle
     S1:::securityStyle
     S2:::securityStyle
     S3:::securityStyle
     S4:::securityStyle
     S5:::securityStyle
     M1:::mlopsStyle
     M2:::mlopsStyle
     M3:::mlopsStyle
     M4:::mlopsStyle
     M5:::mlopsStyle
     M6:::mlopsStyle
     M7:::mlopsStyle
     M8:::mlopsStyle
     T1:::threatStyle
     T2:::threatStyle
     T3:::threatStyle
     T4:::threatStyle
     T5:::threatStyle
    classDef phaseStyle fill:#e1f5ff,stroke:#0066cc,stroke-width:2px
    classDef securityStyle fill:#ffe1e1,stroke:#cc0000,stroke-width:2px
    classDef ucStyle fill:#e1ffe1,stroke:#00cc00,stroke-width:2px
    classDef computeStyle fill:#fff9e1,stroke:#cc9900,stroke-width:2px
    classDef mlopsStyle fill:#f0e1ff,stroke:#9900cc,stroke-width:2px
    classDef threatStyle fill:#ff9999,stroke:#990000,stroke-width:2px
```