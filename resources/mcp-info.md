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
- **Tool-Specific Servers**: MCP servers for tools like Semgrep (code security) and Sentry (error monitoring)

### Implementation of Phenopacket to existing API 
● Where Phenopackets Fit Into HNF1B-DB-API

  Based on the repository structure, here's where Phenopackets would integrate:

  Primary Integration Points

  1. Migration Layer (/migration/) - Data Import Enhancement

  Currently: Google Sheets → Direct PostgreSQL import
  Google Sheets → Phenopackets → Validation → PostgreSQL

  Why here?
  - Acts as standardized intermediate format
  - Validates data during import
  - The existing migrate.py orchestrator would convert sheets data to Phenopackets first

  New files needed:
  /migration/modules/
    phenopacket_builder.py  # Convert sheets data to phenopackets
    phenopacket_validator.py # Validate against GA4GH schema

  2. Models Layer (/app/models.py) - Storage Addition

  Add a new table to store complete Phenopackets alongside existing normalized tables:

  # In models.py - ADD this table
  class PhenopacketStore(Base):
      __tablename__ = "phenopacket_store"

      id: Mapped[UUID] = mapped_column(UUID, primary_key=True)
      individual_id: Mapped[str] = mapped_column(ForeignKey("individuals.individual_id"))
      phenopacket_data: Mapped[dict] = mapped_column(JSONB)  # Full phenopacket
      version: Mapped[str] = mapped_column(String(10))
      status: Mapped[str] = mapped_column(String(50))  # draft/validated/published

      # Link to existing individual
      individual: Mapped["Individual"] = relationship("Individual")

  3. API Endpoints (/app/endpoints/) - New Functionality

  A. Export Endpoints (Quick Win)

  Create /app/endpoints/phenopackets.py:
  @router.get("/individuals/{id}/phenopacket")
  async def export_as_phenopacket(id: str):
      # Gather data from existing tables
      individual = await get_individual(id)
      reports = await get_reports(individual.id)
      variants = await get_variants(individual.id)

      # Convert to phenopacket format
      return build_phenopacket(individual, reports, variants)

  B. Import/Submission Endpoints

  @router.post("/phenopackets/import")
  async def import_phenopacket(file: UploadFile):
      # Parse phenopacket
      # Extract to normalized tables
      # Store original in phenopacket_store

  @router.post("/submissions/clinical")  
  async def submit_clinical_data(form: ClinicalForm):
      # Convert form → phenopacket → database

  4. Schemas (/app/schemas.py) - Form Integration

  Add schemas for user-friendly forms that convert to Phenopackets:

  class ClinicalSubmissionForm(BaseSchema):
      # Doctor-friendly fields
      patient_dob: date
      kidney_cysts: bool
      diabetes_type: Optional[str]
      variant_description: Optional[str]  # Any format
      additional_notes: str  # Becomes extensions

  class PhenopacketResponse(BaseSchema):
      # Phenopacket export format
      phenopacket_data: dict
      validation_status: str

  5. Repository Layer (/app/repositories/) - Data Access

  Create /app/repositories/phenopacket.py:
  class PhenopacketRepository(BaseRepository):
      async def create_from_phenopacket(self, phenopacket: dict):
          # Extract and create Individual
          # Extract and create Reports  
          # Extract and create Variants
          # Store complete phenopacket

      async def export_to_phenopacket(self, individual_id: str):
          # Gather all related data
          # Build phenopacket structure
          # Add extensions for HNF1B-specific data

  Integration Architecture

  Current Flow:
  Google Sheets → Migration Scripts → PostgreSQL → API

  With Phenopackets:
                                      ↗ Normalized Tables (existing)
  Google Sheets → Phenopackets →
                                      ↘ Phenopacket Store (new JSONB)

  User Submissions:
  Web Form → Phenopacket Generation → Validation → Database

  Specific Implementation Areas

  Where Data Flows Through Phenopackets

  1. Input Sources:
    - /migration/ - Convert Google Sheets data
    - /app/endpoints/ - Handle user submissions
    - External imports from other GA4GH systems
  2. Storage Locations:
    - Keep existing normalized tables (no disruption)
    - Add phenopacket_store table for complete documents
    - Reports table already has phenotypes JSONB - compatible!
  3. Output/Exchange:
    - New export endpoints for data sharing
    - Integration with ClinVar/DECIPHER
    - Research collaboration exports

  Which Existing Code Changes

  Minimal changes needed:
  - models.py - Add one new table
  - schemas.py - Add submission forms
  - No changes to existing endpoints
  - No changes to existing repositories

  New additions:
  - /app/endpoints/phenopackets.py - New endpoints
  - /app/endpoints/submissions.py - User submissions
  - /app/services/phenopacket_builder.py - Conversion logic
  - /app/services/variant_validator.py - External API integration

  How It Leverages Existing Structure

  Your current structure is already well-suited for Phenopackets:

  1. Reports table has phenotypes JSONB → Maps directly to phenopacket's phenotypicFeatures
  2. Variants table with classifications → Maps to interpretations
  3. Individual + Report separation → Matches phenopacket's subject/clinical structure
  4. Existing authentication → Protects submission endpoints
  5. Existing validation (Pydantic) → Extends to phenopacket validation

  Recommended Implementation Phases

  Phase 1: Export Only (1-2 weeks)

  # Add to /app/endpoints/individuals.py
  @router.get("/{id}/export/phenopacket")
  async def export_phenopacket(id: str):
      # Use existing data to generate phenopacket

  Phase 2: Store Phenopackets (1 week)

  - Add phenopacket_store table
  - Store alongside existing data
  - No disruption to current system

  Phase 3: Import Capability (2-3 weeks)

  - Accept phenopacket uploads
  - Parse and populate existing tables
  - Enable data exchange with other systems

  Phase 4: User Submissions (2-3 weeks)

  - Build submission forms
  - Auto-generate phenopackets from forms
  - Add review/approval workflow

  Phase 5: Enhanced Migration (1-2 weeks)

  - Update /migration/migrate.py to use phenopackets
  - Better validation during import
  - Standardized data pipeline

  Key Benefits for Current System

  1. No Breaking Changes: Phenopackets complement, don't replace
  2. Gradual Adoption: Implement in phases
  3. Leverages JSONB: You're already using PostgreSQL JSONB effectively
  4. Enables Growth: Doctors can submit new patients
  5. Standards Compliance: Connect with global rare disease networks

  The beauty is that your current architecture (PostgreSQL + JSONB + FastAPI) is already perfectly aligned for
  Phenopacket integration. It's essentially adding a standardization layer on top of what you've built.