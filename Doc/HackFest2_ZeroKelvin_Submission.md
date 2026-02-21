# HackFest 2.0 Submission
## Intelligent Data Dictionary Agent

**Team:** Zero Kelvin  
**Track:** Intelligent Data Dictionary Agent  
**Event:** HackFest 2.0 | GDG Cloud New Delhi × Turgon  
**Date:** February 21-22, 2026

---

## Team Details

| S.No. | Team Member Name | Role | Email |
|-------|-----------------|------|-------|
| 1. | Jakaria Ahmed | Data Engineer | ahmed.ka.workmail@gmail.com |
| 2. | Arunoday Singh | Software Developer | arunodaysingh137@gmail.com |
| 3. | Zakir Ahmed | Software Developer | ahmed.jakaria080800@gmail.com |

---

## Problem Statement

### Objective

Build a software-only solution that connects to enterprise databases (Snowflake, PostgreSQL, SQL Server, etc.) and automatically generates comprehensive, AI-enhanced data dictionaries. It should extract schema metadata, analyze data quality, and produce business-friendly documentation. An interactive chat interface should allow users to query and understand the data through natural language.

### Challenge

Database documentation is often outdated, incomplete, or non-existent. Technical metadata lacks business context, making it difficult for analysts and business users to understand what data means and how to use it.

**Key Requirements:**
- Connect to multiple database types and extract complete schema metadata (tables, columns, relationships, constraints)
- Perform intelligent data quality analysis with metrics like completeness, freshness, and key health
- Mathematical statistical analysis of the data on the go would be a plus
- Use AI to generate business-friendly summaries and usage recommendations for each table
- Produce documentation in multiple formats (JSON, Markdown) and store artifacts for future reference
- Provide a conversational chat interface where users can ask natural language questions about their database schema

**Optional Features:**
- Support incremental updates when schema changes are detected
- Visualize data lineage and table relationships
- Generate SQL query suggestions based on user questions
- Provide data quality alerts and trend monitoring

### Key Focus

Accurate metadata extraction, meaningful AI-generated business context, and intuitive natural language access to database documentation.

---

## Proposed Solution

### Solution Overview

We propose an **Intelligent Data Dictionary Agent** that transforms legacy databases into searchable, self-healing knowledge bases through three core components:

### 1. Autonomous Extraction & MCP Integration

**What it does:**
- Connects to legacy and modern databases (PostgreSQL, SQL Server, Snowflake, etc.)
- Automatically "reads" entire database structures without manual intervention
- Uses **MCP (Model Context Protocol)** for DBs wherever possible to expose database schemas directly to AI
- Provides deep context needed to map complex relationships and constraints

**How it works:**
- Leverages `INFORMATION_SCHEMA` and database-specific metadata tables
- Extracts tables, columns, data types, primary keys, foreign keys, indexes, and constraints
- Builds a comprehensive schema graph representing all relationships

### 2. AI Intelligence & Health Checks

**What it does:**
- Performs real-time "health checks" using statistical analysis
- Spots issues like missing data, outdated records, outliers, and data quality problems
- Uses AI to translate cryptic technical metadata into clear business summaries
- Converts confusing technical labels into trustworthy, easy-to-understand institutional knowledge

**Statistical Analysis Features:**
- **Completeness Metrics:** Percentage of non-null values per column
- **Freshness Analysis:** Identifies stale data based on timestamps
- **Key Health:** Validates primary key uniqueness and foreign key integrity
- **Z-Scores:** Detects outliers in numerical columns
- **Shannon Entropy:** Measures data diversity and distribution quality
- **Data Type Validation:** Ensures data matches declared types

**AI Enhancement:**
- Generates business-friendly descriptions for each table and column
- Provides usage recommendations based on data patterns
- Suggests common use cases and query patterns

### 3. Agentic RAG & Chat Interface

**What it does:**
- Provides a conversational chat interface powered by Agentic RAG framework
- Users ask questions in plain English instead of writing SQL
- Finds relevant data and provides query suggestions
- Transforms the "data graveyard" into a searchable, self-healing knowledge base

**Capabilities:**
- Natural language queries: "What tables contain customer information?"
- Query generation: "Show me how to join orders with customers"
- Data discovery: "Which columns track order status?"
- Business context: "What does the 'order_status' field mean?"

### 4. Self-Healing & Documentation

**Schema Drift Detection:**
- Monitors `INFORMATION_SCHEMA` continuously
- Detects schema changes automatically (new tables, modified columns, dropped constraints)
- Triggers incremental updates to keep documentation fresh

**Documentation Generation:**
- Uses Jinja2 templating to generate documentation
- Exports in multiple formats: **Markdown** (human-readable) and **JSON** (machine-readable)
- Version-controlled artifacts for tracking changes over time
- Includes data quality metrics, business summaries, and usage examples

### 5. Data Lineage Visualization (Future Enhancement)

**Proactive Data Lineage:**
- Visualizes table relationships using Mermaid.js or D3.js
- Shows exactly how data flows through the organization
- Interactive diagrams for exploring dependencies
- Helps users understand complex database structures at a glance

---

## Technical Architecture

### Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Orchestration** | LangGraph (Python) | Agentic RAG framework for managing multi-step workflows |
| **Context Layer** | MCP (FastMCP) | Secure, standardized bridge between LLM and database schemas |
| **Quality Engine** | Pandas Profiling | Statistical metrics calculation (Z-Scores, Shannon Entropy, completeness) |
| **Frontend** | Streamlit | Natural language chat interface |
| **Database Connectors** | SQLAlchemy, psycopg2, pyodbc | Multi-database connectivity |
| **Documentation** | Jinja2 | Template-based documentation generation |
| **Visualization** | Mermaid.js / D3.js | Data lineage and relationship diagrams |
| **AI/LLM** | OpenAI GPT / Anthropic Claude | Business context generation and natural language understanding |

### System Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                    INTELLIGENT DATA DICTIONARY AGENT            │
└─────────────────────────────────────────────────────────────────┘

┌──────────────┐
│   Database   │──┐
│  (PostgreSQL)│  │
└──────────────┘  │
                  │
┌──────────────┐  │    ┌──────────────────────────────────────┐
│   Database   │──┼───>│   MCP Layer (FastMCP)                │
│  (SQL Server)│  │    │   - Schema Extraction                │
└──────────────┘  │    │   - Metadata Collection              │
                  │    └──────────────┬───────────────────────┘
┌──────────────┐  │                   │
│   Database   │──┘                   │
│  (Snowflake) │                      │
└──────────────┘                      │
                                      ▼
                    ┌──────────────────────────────────────┐
                    │   LangGraph Agentic RAG Framework    │
                    │   - Orchestrates extraction flow    │
                    │   - Manages AI interactions          │
                    └──────────────┬───────────────────────┘
                                   │
                    ┌──────────────┴───────────────────────┐
                    │                                       │
        ┌───────────▼───────────┐          ┌──────────────▼──────────┐
        │  Pandas Profiling     │          │   AI/LLM Engine         │
        │  Quality Engine       │          │   - Business summaries   │
        │  - Z-Scores           │          │   - Context generation  │
        │  - Entropy            │          │   - Query suggestions    │
        │  - Completeness       │          └──────────────────────────┘
        └───────────┬───────────┘
                    │
        ┌───────────▼───────────────────────────────────────┐
        │   Documentation Generator (Jinja2)                │
        │   - Markdown export                                │
        │   - JSON export                                    │
        │   - Version control                                │
        └───────────┬───────────────────────────────────────┘
                    │
        ┌───────────▼───────────────────────────────────────┐
        │   Streamlit Chat Interface                         │
        │   - Natural language queries                       │
        │   - Query suggestions                              │
        │   - Data discovery                                 │
        └───────────────────────────────────────────────────┘
```

---

## Dataset Validation

https://github.com/GDG-Cloud-New-Delhi/hackfest-2.0-dataset/blob/main/Internal_Recommendation_Doc.md?utm_campaign=website&utm_medium=email&utm_source=sendgrid.com

### Primary Dataset: Brazilian E-Commerce (Olist)

**Source:** https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce  
**License:** CC BY-NC-SA 4.0

**Why this dataset:**
- **9 interlinked CSV tables** with real foreign-key relationships
- **100K+ orders** with diverse data types (timestamps, floats, categorical, text, geospatial)
- Mix of clean and messy data (nulls, inconsistent categories) - perfect for data quality analysis
- Clear business context (e-commerce) - AI summaries can be meaningfully evaluated
- Well-documented ER diagram available for validation

**Tables:**
- `orders` - Order information
- `customers` - Customer data
- `sellers` - Seller information
- `products` - Product catalog
- `order_items` - Order line items
- `payments` - Payment transactions
- `reviews` - Customer reviews
- `geolocation` - Geographic data
- `product_category_name_translation` - Category translations

### Secondary Dataset: Bike Store SQL Database

**Source:** https://www.kaggle.com/datasets/dillonmyrick/bike-store-sample-database  
**License:** CC0 (Public Domain)

**Why this dataset:**
- **9 tables** with clear schema separation (sales, production schemas)
- Pre-built SQL schema with explicit primary keys, foreign keys, and constraints
- Smaller and cleaner - useful for quick testing and demos
- Perfect for validating strict relational mapping and foreign key extraction

**Tables:**
- `sales.stores`
- `sales.staffs`
- `production.categories`
- `production.brands`
- `production.products`
- `sales.customers`
- `sales.orders`
- `sales.order_items`
- `production.stocks`

---

## Key Features

### ✅ Core Features (Implemented)

- [x] Multi-database connectivity (PostgreSQL, SQL Server, Snowflake)
- [x] Automatic schema extraction (tables, columns, relationships, constraints)
- [x] MCP integration for standardized database access
- [x] Statistical data quality analysis (completeness, freshness, Z-scores, entropy)
- [x] AI-generated business summaries and context
- [x] Natural language chat interface (Streamlit)
- [x] Documentation generation (Markdown, JSON)
- [x] Schema drift detection via INFORMATION_SCHEMA monitoring

### 🚀 Enhanced Features (In Progress)

- [ ] Incremental updates on schema changes
- [ ] Data lineage visualization (Mermaid.js/D3.js)
- [ ] SQL query generation from natural language
- [ ] Data quality alerts and trend monitoring
- [ ] Interactive relationship diagrams

---

## Use Cases

### 1. Data Discovery
**Scenario:** A new analyst joins the team and needs to understand the database structure.

**Solution:** 
- Chat interface: "What tables contain customer information?"
- System responds with relevant tables, column descriptions, and sample queries
- Provides business context: "The `customers` table tracks customer demographics and is linked to orders via `customer_id`"

### 2. Data Quality Monitoring
**Scenario:** A data engineer needs to identify data quality issues.

**Solution:**
- System automatically flags columns with >30% null values
- Detects outliers using Z-score analysis
- Alerts on stale data (e.g., orders table hasn't been updated in 7 days)
- Generates quality report with actionable recommendations

### 3. Query Assistance
**Scenario:** A business user wants to analyze sales but doesn't know SQL.

**Solution:**
- User asks: "How do I get total sales by product category?"
- System generates SQL query and explains the joins
- Provides business context for each table involved
- Suggests related queries: "You might also want to filter by date range"

### 4. Documentation Maintenance
**Scenario:** Database schema changes frequently, documentation becomes outdated.

**Solution:**
- System monitors INFORMATION_SCHEMA continuously
- Detects new tables, modified columns, dropped constraints
- Automatically regenerates documentation
- Maintains version history for tracking changes

---

## Implementation Highlights

### 1. MCP Integration
- Uses FastMCP to create standardized database connectors
- Exposes database schemas directly to LLM with proper context
- Enables deep understanding of relationships without manual mapping

### 2. Statistical Analysis Engine
- **Z-Scores:** Identifies outliers in numerical columns (values >3 standard deviations)
- **Shannon Entropy:** Measures data diversity (low entropy = repetitive data)
- **Completeness:** Calculates null percentage per column
- **Freshness:** Analyzes timestamp columns to detect stale data
- **Key Health:** Validates primary key uniqueness and foreign key referential integrity

### 3. Agentic RAG Framework
- LangGraph orchestrates multi-step workflows:
  1. User query → Intent understanding
  2. Schema search → Find relevant tables/columns
  3. Context retrieval → Gather metadata and quality metrics
  4. AI generation → Business-friendly response
  5. Query suggestion → SQL generation (optional)

### 4. Self-Healing Documentation
- Continuous monitoring of schema changes
- Automatic documentation regeneration
- Version-controlled artifacts (Git integration)
- Jinja2 templates for consistent formatting

---

## Future Enhancements

1. **Multi-language Support:** Generate documentation in multiple languages
2. **Collaborative Features:** Allow teams to add annotations and notes
3. **Integration with BI Tools:** Export metadata to Tableau, Power BI, etc.
4. **Advanced Lineage:** Track data transformations and ETL pipelines
5. **ML-based Anomaly Detection:** Use machine learning to identify unusual patterns
6. **API Access:** RESTful API for programmatic access to data dictionary
7. **Role-based Access:** Different views for analysts, engineers, and executives

---

## Demo Scenarios

### Scenario 1: New Database Onboarding
**Input:** Connect to Olist E-Commerce database  
**Output:** 
- Complete schema extraction (9 tables, relationships mapped)
- Data quality report highlighting null percentages and outliers
- Business-friendly documentation in Markdown
- Chat interface ready for queries

### Scenario 2: Natural Language Query
**User:** "What's the relationship between orders and customers?"  
**System Response:**
- Explains foreign key relationship (`orders.customer_id` → `customers.customer_id`)
- Shows sample join query
- Provides business context: "Each order belongs to one customer, but a customer can have multiple orders"
- Suggests related queries about order history

### Scenario 3: Data Quality Alert
**System:** "Alert: `order_items` table has 15% null values in `price` column"  
**Action:** System generates report with:
- Affected rows identified
- Potential impact analysis
- Recommendations for data cleaning

---

## Conclusion

Our **Intelligent Data Dictionary Agent** transforms the "data graveyard" problem into a solution that:

✅ **Automates** schema extraction and documentation  
✅ **Enhances** technical metadata with AI-generated business context  
✅ **Monitors** data quality in real-time  
✅ **Empowers** users with natural language access  
✅ **Self-heals** by detecting and updating schema changes  

By combining MCP for standardized database access, statistical analysis for quality insights, and Agentic RAG for intelligent interactions, we create a platform that makes enterprise databases accessible to everyone—from data engineers to business analysts.

---

## References

- **Problem Statement:** HackFest 2.0 - Intelligent Data Dictionary Agent Track
- **Dataset 1:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- **Dataset 2:** [Bike Store Sample Database](https://www.kaggle.com/datasets/dillonmyrick/bike-store-sample-database)
- **MCP Documentation:** [Model Context Protocol](https://modelcontextprotocol.io/)
- **LangGraph:** [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- **Pandas Profiling:** [Pandas Profiling Documentation](https://pandas-profiling.ydata.ai/)

---

**Team Zero Kelvin**  
*Transforming data graveyards into knowledge bases*

