### Modern Context Protocols (MCPs)

## Definition 
- Open Protocol standardising how applications provide context to LLMs
- Standardised way to connect AI models to different data sources and tools. 

## What do MCPs provide?
- **Growing list of pre-built integrations** LLM can directly plug into 
- Standardised way to build custom integrations for AI applications
- **Open protocol** free to implement and use 
- **Flexibility to change** between different apps whilst taking the context with you. 

## Concepts of MCP
- **The MCP Server**: Think of this as a **waiter** in a restaurant. The waiter's job is to know what the kitchen (the data or tool) can offer. They **present a menu of options** (a standardized list of what the AI can do) to the customer. In the digital world, the "server" is a program that exposes data, tools, or functions for the AI to use.
- **The MCP Client** This is the **AI model**, which is like the **customer** in the restaurant. The AI (the "client") looks at the menu and makes a request to the waiter (the "server").
- **The Communication** The client and server talk to each other using a **standardized set of commands, much like how a customer orders from a menu. This standardized communication is the core of MCP. It ensures that any "customer" (AI client) can talk to any "waiter" (MCP server) without needing a special translator.

## Reference Implementations 
Foundational servers showcasing core capabilities of the protocol:
- **Filesystem**: Allows the AI to securely read and write files on a local system.
- **Git**: Enables the AI to interact with Git repositories (like cloning, reading files, etc.).
- **Fetch**: Gives the AI the ability to access and process content from web pages.
- **Memory**: Provides the AI with a knowledge graph for persistent memory.
- **Time**: Offers time and timezone conversion functions.

## Official and Community Integrations 
Servers connecting AI to popular third-party services:
- **Cloud Services**: Servers for AWS, Azure, and Google Cloud that allow the AI to manage cloud resources.
- **Development Tools**: Integrations for services like GitHub, GitLab, and Sentry for managing code and tracking issues.
- **Productivity and Communication**: Servers for tools like Slack and Google Drive to manage conversations and files.
- **Databases**: Servers for PostgreSQL and SQLite that enable the AI to query and interact with databases.

## Available Services 
- **Context7**: free service to make AI coding assistants & LLMs more accurate 
    - Solves problem of AI models having been trained on outdated information 
    - Continously indexes latest documentation of software libraries 
    - Extracts clean, ready to use code snippets from the documentation 
    - makes up to date info searchable for developers to feed directly to their AI tools 
- **VisionCraft MCP**: competitor of Context7; providing real-time knowledge from code repositories 
    - Special emphasis on computer vision & generative AI
- **Bright Data MCP**: Focuses on scraping web data to feed into an LLM 
    - Useful for gathering real-time info from the web to be used as context
- **Custom MCP Servers**: Developers can build their own MCP servers
    - Open source projects available to serve context from provate GitHub repositories or internal documentation 

## Specialised MCP Servers 
Specialised servers for specific needs; curated list found under **awesome-mcp-servers** GitHub repository. Some examples:
- **Database Connectors**: Servers for databases such as ClickHouse, Couchbase, Milvus
- **API-Specific Servers**: Many services (i.e. Chargebee, CircleCI, Supabase) offer own MCP servers
- **Tool-Specific Severs**: MCP servers for tools like Semgrep (code security) and Sentry (error monitoring)