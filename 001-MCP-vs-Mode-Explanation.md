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

## FAQ: Using Carbon MCP Without Carbon Mode

### Question: If I don't have Carbon mode, will the Carbon MCP be used by Advanced mode properly?

**Short Answer**: Yes! Advanced mode can use Carbon MCP perfectly well.

### Detailed Explanation

**Mode vs MCP Independence**:
- **Modes** and **MCP servers** are independent systems
- Any mode that supports MCP can use ANY MCP server
- You don't need a specialized "Carbon mode" to use "Carbon MCP"

**Advanced Mode + Carbon MCP**:

```
┌──────────────────────┐
│   Advanced Mode      │
│  (MCP-enabled)       │
└──────────┬───────────┘
           │
           │ Can use ANY MCP server:
           │
    ┌──────┼──────┬──────────┬─────────┐
    ▼      ▼      ▼          ▼         ▼
  Carbon Figma  GitHub   Database  Custom
   MCP    MCP    MCP       MCP      MCP
```

**What You Get**:

| With Carbon Mode | With Advanced Mode + Carbon MCP |
|------------------|----------------------------------|
| Built-in Carbon expertise | Carbon tools via MCP |
| Optimized Carbon workflow | General coding + Carbon MCP tools |
| No MCP setup needed | Requires MCP server setup |
| Carbon-specific prompts | Use `use_mcp_tool` for Carbon features |

**Practical Example**:

**Scenario**: You want to implement a Carbon component from Figma

**Option 1 - Carbon Mode (if available)**:
```
1. Switch to Carbon React mode
2. Describe component or provide image
3. Mode uses built-in Carbon knowledge
4. Component implemented automatically
```

**Option 2 - Advanced Mode + Carbon MCP**:
```
1. Switch to Advanced mode
2. Use Carbon Figma MCP: use_mcp_tool to fetch design specs
3. Use Carbon MCP: use_mcp_tool to validate component structure
4. Implement component with MCP-provided data
5. Use Carbon MCP: use_mcp_tool to verify against standards
```

**Key Differences**:

1. **Carbon Mode**: 
   - Streamlined, specialized workflow
   - Built-in Carbon knowledge
   - No external setup required
   - Best for: Quick Carbon questions and implementations

2. **Advanced Mode + Carbon MCP**:
   - More flexible, general-purpose
   - Requires explicit MCP tool calls
   - Needs MCP server configuration
   - Best for: Complex workflows combining Carbon with other tools

**The Bottom Line**:

✅ **Yes, Advanced mode can use Carbon MCP properly**
- All MCP functionality is available
- You just need to explicitly call MCP tools
- No specialized mode required for MCP access

❌ **What you might miss without Carbon Mode**:
- Automatic Carbon context and expertise
- Streamlined Carbon-specific workflows
- Built-in Carbon component knowledge

**Recommendation**:
- If you have **Carbon MCP server** but no **Carbon mode**: Use Advanced mode and call MCP tools explicitly
- If you have **Carbon mode** but no **Carbon MCP**: Use Carbon mode for built-in expertise
- If you have **both**: Use Carbon mode for quick tasks, Advanced mode + MCP for complex integrations


---

## Conclusion

**MCP** and **Modes** serve complementary but distinct purposes:

- **MCP** extends what the AI can access and do by connecting to external services
- **Modes** define how the AI operates and what built-in capabilities are available

Together, they provide a flexible and powerful development environment that can be tailored to specific workflows and integrated with external tools as needed.
---

## Important Clarification: Carbon Mode vs Carbon MCP

### Is Carbon Mode Really Needed if You Have Carbon MCP?

**Not necessarily, but they serve different purposes and complement each other.**

### The Key Distinction

**Carbon MCP** and **Carbon Mode** are NOT the same thing and provide different value:

#### Carbon MCP (External Tools)
- **What it provides**: External tools and data access
- **Examples**: 
  - Fetch Figma design specifications
  - Query Carbon component library API
  - Validate code against design tokens
  - Access real-time Carbon documentation
- **Limitation**: Only provides tools/data, not built-in expertise

#### Carbon Mode (Built-in Expertise)
- **What it provides**: Specialized AI behavior and knowledge
- **Examples**:
  - Deep understanding of Carbon patterns and best practices
  - Optimized prompts for Carbon workflows
  - Automatic Carbon context without explicit tool calls
  - Streamlined component implementation
- **Limitation**: May not have access to external data sources

### Comparison Matrix

| Feature | Carbon MCP Only | Carbon Mode Only | Both Together |
|---------|----------------|------------------|---------------|
| **Access Figma designs** | ✅ Yes | ❌ No | ✅ Yes |
| **Built-in Carbon expertise** | ❌ No | ✅ Yes | ✅ Yes |
| **Real-time design tokens** | ✅ Yes | ❌ No | ✅ Yes |
| **Optimized Carbon workflow** | ❌ No | ✅ Yes | ✅ Yes |
| **External API integration** | ✅ Yes | ❌ No | ✅ Yes |
| **Automatic Carbon context** | ❌ No | ✅ Yes | ✅ Yes |
| **Requires setup** | ✅ Yes | ❌ No | ✅ Yes (MCP only) |

### Real-World Scenarios

#### Scenario 1: "Implement a Carbon Button"

**With Carbon MCP Only (Advanced Mode)**:
```
You: "Implement a Carbon Button"
AI: "I need to use MCP tools to get Carbon specs..."
    → use_mcp_tool: fetch_carbon_component("Button")
    → Receives API data
    → Implements based on fetched data
Result: ✅ Works, but requires explicit MCP calls
```

**With Carbon Mode Only**:
```
You: "Implement a Carbon Button"
AI: "Based on Carbon Design System knowledge..."
    → Uses built-in Carbon expertise
    → Implements from memory/training
Result: ✅ Works, streamlined and automatic
```

**With Both**:
```
You: "Implement a Carbon Button matching this Figma design"
AI: "Using Carbon expertise and Figma data..."
    → Uses built-in Carbon knowledge
    → use_mcp_tool: fetch_figma_specs(design_id)
    → Combines both sources
Result: ✅✅ Best of both worlds
```

#### Scenario 2: "What are Carbon's accessibility guidelines?"

**With Carbon MCP Only**:
```
→ use_mcp_tool: query_carbon_docs("accessibility")
→ Returns documentation
Result: ✅ Accurate, real-time data
```

**With Carbon Mode Only**:
```
→ Uses built-in knowledge
→ Provides answer from training
Result: ✅ Fast, but may be outdated
```

**With Both**:
```
→ Uses built-in knowledge for context
→ use_mcp_tool: verify_latest_guidelines()
→ Combines expertise with current data
Result: ✅✅ Expert answer with latest info
```

### So, Do You Need Carbon Mode?

**You DON'T strictly need Carbon Mode if**:
- You're comfortable making explicit MCP tool calls
- You have comprehensive Carbon MCP tools
- You're working in Advanced mode anyway
- You prefer manual control over automatic behavior

**Carbon Mode is VALUABLE when**:
- You want streamlined, automatic Carbon workflows
- You need quick answers without MCP setup
- You prefer specialized context over general-purpose mode
- You want optimized prompts and behavior for Carbon work

**The IDEAL setup**:
- **Carbon Mode WITH Carbon MCP access** = Best experience
  - Built-in expertise + real-time data
  - Automatic workflows + external tools
  - Specialized behavior + API integration

### Analogy

Think of it like cooking:

- **Carbon MCP** = Having access to a grocery delivery service
  - You can get fresh ingredients anytime
  - Requires ordering (explicit tool calls)
  - Provides real-time, accurate data

- **Carbon Mode** = Being a trained chef specializing in Italian cuisine
  - You know recipes by heart
  - You work efficiently without looking things up
  - You understand the cuisine deeply

- **Both Together** = Expert chef with grocery delivery
  - You know what to cook AND can get fresh ingredients
  - Best possible outcome

### Final Answer

**"Is Carbon Mode really needed if we have Carbon MCP?"**

**Technical answer**: No, not strictly required. Advanced mode + Carbon MCP can do everything.

**Practical answer**: Carbon Mode adds significant value through:
1. Automatic Carbon context (no explicit tool calls needed)
2. Optimized workflows for Carbon tasks
3. Built-in expertise that complements MCP data
4. Faster, more streamlined experience

**Best practice**: Use both together when possible for optimal results.

---
