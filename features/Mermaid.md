[中文](./Mermaid.zh.md) | **English**

# Mermaid Diagrams

Gleaner renders [Mermaid](https://mermaid.js.org/) code blocks as diagrams, just like Obsidian and GitHub. Diagrams follow your dark/light theme automatically.

## Flowchart

```mermaid
flowchart LR
    A[Markdown File] --> B{Contains mermaid?}
    B -->|Yes| C[Render SVG]
    B -->|No| D[Normal code block]
    C --> E[Display diagram]
```

## Sequence Diagram

```mermaid
sequenceDiagram
    participant User
    participant Gleaner
    participant GitHub

    User->>Gleaner: Open file
    Gleaner->>GitHub: Fetch content
    GitHub-->>Gleaner: Markdown + mermaid
    Gleaner-->>User: Rendered diagram
```

## Class Diagram

```mermaid
classDiagram
    class MdFile {
        +string path
        +string content
        +string repoFullName
    }
    class MermaidBlock {
        +string code
        +render()
    }
    class CodeBlock {
        +ReactNode children
        +detectLanguage()
    }
    CodeBlock --> MermaidBlock : delegates mermaid
    MermaidBlock ..> MdFile : reads from
```

## State Diagram

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Syncing : User opens app
    Syncing --> Cached : Sync complete
    Cached --> Syncing : Manual refresh
    Syncing --> Error : API failure
    Error --> Syncing : Retry
```

## Gantt Chart

```mermaid
gantt
    title Gleaner Feature Roadmap
    dateFormat YYYY-MM-DD
    section Core
        MVP launch          :done, 2025-01-01, 2025-03-01
        Wikilinks           :done, 2025-03-01, 2025-04-01
    section Enhancements
        PWA support         :done, 2025-04-01, 2025-04-10
        Mermaid diagrams    :active, 2025-04-10, 2025-04-15
        Local profiles      :2025-04-15, 2025-05-01
```

## Pie Chart

```mermaid
pie title File Types in Knowledge Base
    "Markdown" : 85
    "Images" : 10
    "Config" : 5
```

## Entity Relationship Diagram

```mermaid
erDiagram
    REPO ||--o{ FILE : contains
    FILE ||--o{ LINK : has
    LINK }o--|| FILE : "points to"
    REPO {
        string fullName
        string treeSha
        string label
    }
    FILE {
        string path
        string content
        int repoId
    }
```

## Error Handling

When a mermaid block contains invalid syntax, Gleaner falls back to displaying the raw code with an error message:

```mermaid
this is not valid mermaid syntax
  --> should show error fallback
```
