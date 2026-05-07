# MCP vs Mode: Understanding the Differences

## Overview

This document explains the key differences between **MCP (Model Context Protocol)** and **Modes** in the context of AI development tools like Carbon.

---

## MCP (Model Context Protocol)

### What is MCP?

**MCP** is a **communication protocol** that enables integration between AI assistants and external servers/tools.

### Key Characteristics

- **Purpose**: Extends AI capabilities by connecting to external services, APIs, and data sources
- **Architecture**: Client-server model where MCP servers provide tools and resources
- **Communication**: Uses standardized protocol for tool invocation and resource access
- **Invocation**: Used via `use_mcp_tool` command within compatible modes

### Types of MCP Servers

1. **Local (stdio-based)**: Servers running on your local machine
2. **Remote (SSE-based)**: Servers accessed over HTTP/HTTPS

### Example Use Cases

- Fetching component documentation from external APIs
- Accessing Figma design files via Figma MCP server
- Validating code against design system standards
- Querying external databases or knowledge bases

### MCP Architecture

```
┌─────────────────┐
│  AI Assistant   │
└────────┬────────┘
         │ MCP Protocol
         ▼
┌─────────────────┐
│   MCP Server    │
├─────────────────┤
│ • Provides Tools│
│ • Provides Data │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐ ┌──────────┐
│External│ │  Data    │
│  APIs  │ │ Sources  │
└────────┘ └──────────┘
```

---

## Modes

### What are Modes?

**Modes** are **operational contexts** that define how the AI assistant behaves and what capabilities it has.

### Key Characteristics

- **Purpose**: Tailors the AI's behavior, available tools, and file access for specific workflows
- **Scope**: Controls what the assistant can do within the current session
- **Specialization**: Each mode is optimized for specific types of tasks
- **Switching**: Can be changed based on task requirements

### Common Modes

| Mode | Icon | Purpose | Capabilities |
|------|------|---------|--------------|
| **Ask** | ❓ | Answer questions | Read-only, no file editing |
| **Code** | 💻 | Write/modify code | Code editing, no MCP/Browser |
| **Advanced** | 🛠️ | Complex tasks | Code + MCP + Browser access |
| **Plan** | 📝 | Project planning | Limited to .md files |
| **Carbon React** | ⬡🐝 | Carbon components | Carbon expertise + tools |

### Mode Restrictions

Each mode has specific limitations:

- **File Access**: Some modes restrict which file types can be edited
- **Tool Availability**: Certain tools (MCP, Browser) may be disabled
- **Workflow Focus**: Optimized for specific development tasks

### Mode Selection Flow

```
User Task
    │
    ▼
┌─────────────────┐
│  Choose Mode    │
└────────┬────────┘
         │
    ┌────┼────┬────────┬──────────┐
    ▼    ▼    ▼        ▼          ▼
  Plan Code Advanced Carbon   Ask
   │     │      │       │        │
   ▼     ▼      ▼       ▼        ▼
  .md  Code  Code+   Carbon   Read
 files only  MCP+   Expert   Only
            Browser
```

---

## Key Differences: MCP vs Mode

| Aspect | MCP | Mode |
|--------|-----|------|
| **Definition** | Communication protocol | Operational context |
| **Purpose** | Connect to external services | Define AI behavior/capabilities |
| **Scope** | Tool/resource provider | Workflow specialization |
| **Flexibility** | Can be used across compatible modes | Switched per task |
| **Implementation** | External server setup required | Built-in to AI system |
| **Access Method** | `use_mcp_tool` command | Mode switching |
| **Example** | Carbon Figma MCP server | Carbon React mode |

---

## Carbon Context: Practical Examples

### Carbon React Mode (⬡🐝)

**What it is**: A specialized **mode** for Carbon Design System work

**Capabilities**:
- Provides Carbon expertise and component knowledge
- Can implement Carbon components from descriptions/images
- Answers questions about Carbon usage and best practices
- **Does NOT** require Figma MCP access (works standalone)

**Best for**:
- "What is the Carbon Button component?"
- "How do I use DataTable?"
- "Implement a Carbon modal from this description"

### Carbon MCP (Hypothetical Example)

**What it would be**: An **MCP server** providing Carbon-specific tools

**Potential Capabilities**:
- Figma dev mode access for design-to-code workflows
- Design token validation against Carbon standards
- Component library queries and documentation
- Real-time design system updates

**Usage**: Would be invoked **within** a mode (like Advanced mode) via `use_mcp_tool`

**Example Workflow**:
```
1. Switch to Advanced mode
2. Use Carbon Figma MCP to fetch design specs
3. Implement component based on Figma data
4. Validate against Carbon standards
```

---

## Simple Analogy

Think of it this way:

- **MCP** = External toolbox you can connect to
  - Like plugging in a power tool to extend your capabilities
  - Requires setup and connection
  - Provides specialized tools and data

- **Mode** = The role/specialty you're working in
  - Like being a carpenter vs. electrician
  - Changes your available tools and approach
  - Optimized for specific types of work

---

## When to Use What?

### Use MCP When:
- You need access to external services or APIs
- You require real-time data from external sources
- You want to integrate with tools like Figma, databases, or custom APIs
- You need capabilities beyond the AI's built-in tools

### Switch Modes When:
- Your task type changes (planning → coding → reviewing)
- You need different tool access (need MCP/Browser tools)
- You want specialized expertise (Carbon components, specific frameworks)
- File editing restrictions need to change

---

## Conclusion

**MCP** and **Modes** serve complementary but distinct purposes:

- **MCP** extends what the AI can access and do by connecting to external services
- **Modes** define how the AI operates and what built-in capabilities are available

Together, they provide a flexible and powerful development environment that can be tailored to specific workflows and integrated with external tools as needed.