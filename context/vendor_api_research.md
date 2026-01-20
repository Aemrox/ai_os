# Vendor API Research & Integration Analysis

Comprehensive research on API capabilities, authentication methods, and integration complexity for key data vendors.

**Research Date:** January 2026
**Focus:** Tier 1 critical vendors for AI use case implementation

---

## Tier 1 Critical Vendors

### Bloomberg API (BLPAPI)

**Official Documentation:** [bloomberg.github.io/blpapi-docs](https://bloomberg.github.io/blpapi-docs/)

#### API Access Methods
- **Desktop API:** For applications running on Bloomberg Terminal (simplified auth)
- **Server API (SAPI):** Enterprise-grade server-side access
- **HTTP API:** Open API via HTTP and WebSockets for reference, historical, and live data

#### Authentication & Authorization
- **Desktop API:** Leverages terminal authentication (simpler)
- **Enterprise Products (B-PIPE, SAPI):** Require:
  - UUID and application name credentials
  - Opening `//blp/apiauth` service
  - Application-level authentication and authorization
  - User permissioning before distributing data

#### Supported Languages
- C/C++
- Java
- C# (.NET)
- Python (3.8, 3.9, 3.10, 3.11, 3.12 with bundled C++ API)
- Perl

#### Data Access
- Real-time market data
- Historical data
- Reference data
- Corporate actions
- News and research

#### Integration Complexity
- **Moderate to High:** Enterprise products require significant setup
- **Licensing Dependency:** Requires active Bloomberg subscription and appropriate data entitlements
- **Infrastructure:** May require dedicated Bloomberg connectivity infrastructure

#### Key Considerations
- Existing terminal access simplifies some use cases
- Desktop API easiest path for terminal-based workflows
- Server API required for automated, server-side processes
- Data permissioning adds complexity for multi-user applications

**Sources:**
- [BLPAPI Documentation](https://bloomberg.github.io/blpapi-docs/)
- [Bloomberg Core Developer Guide](https://data.bloomberglp.com/professional/sites/10/2017/03/BLPAPI-Core-Developer-Guide.pdf)
- [How to Use Bloomberg API](https://apidog.com/blog/bloomberg-api/)
- [Server API (SAPI)](https://www.bloomberg.com/professional/products/data/data-connectivity/server-api/)

---

### FactSet API

**Official Portal:** [developer.factset.com](https://developer.factset.com/)

#### API Architecture
- **RESTful APIs:** Modern REST architecture
- **Enterprise SDK:** Auto-generated client libraries
- **Trading API:** Separate trading-focused API
- **Formula API:** FactSet formula integration

#### Authentication Methods
- **OAuth 2.0 (Recommended):** ConfidentialClient with configuration from Developer Portal
- **API Key:** Alternative authentication method
- **Basic Authentication:** Username-serial and API-KEY credentials

#### Authentication Setup
All authentication must be configured through the **FactSet Developer Portal**:
- Production environment allows direct API key generation
- OAuth client setup available through portal
- [Authentication Documentation](https://developer.factset.com/authentication)

#### SDK Support
- **Auto-generated Libraries:** Using OpenAPI Generator
- **Languages:** .NET, Java, Python, TypeScript/JavaScript
- **GitHub:** [factset/enterprise-sdk](https://github.com/factset/enterprise-sdk)

#### API Catalog
Comprehensive API offerings including:
- **PA Engine API:** Portfolio analysis
- **Entity API:** Entity data and relationships
- **Formula API:** FactSet formula integration
- **Publisher API:** Data publishing capabilities
- **Trading API:** Order management and execution

#### Integration Complexity
- **Low to Moderate:** Well-documented REST APIs
- **Modern Architecture:** OAuth 2.0 and REST make integration straightforward
- **SDK Support:** Pre-built client libraries reduce development time
- **Active Subscription Required:** API access tied to FactSet subscription level

#### Key Advantages
- Comprehensive developer portal with catalog of all APIs
- Modern authentication (OAuth 2.0)
- Auto-generated SDKs in multiple languages
- Clear, structured documentation

**Sources:**
- [FactSet Developer Portal](https://developer.factset.com/)
- [FactSet API Catalog](https://developer.factset.com/api-catalog)
- [FactSet Trading API Developer Guide](https://assets.ctfassets.net/lmz2w5z92b9u/2Vb7JAVSxkBIZsFagkEzAt/372da67a3ade43724a642e6e94865ec8/FactSet_Trading_API_Developer_Guide_v0.5.0.pdf)
- [API Tracker: FactSet](https://apitracker.io/a/factset)

---

### S&P Capital IQ (S&P Global Market Intelligence)

**API Portal:** [S&P Global Marketplace](https://www.marketplace.spglobal.com/)

#### API Architecture
- **On-Demand Access:** REST API for data retrieval
- **Python SDK (SPGMICIQ):** Official Python package available on PyPI
- **LLM-Ready API (Kensho):** Natural language query interface

#### API Access Methods
- **Traditional REST API:** Direct API calls with mnemonic-based queries
- **Python SDK:** Pandas DataFrame integration, Jupyter-friendly
- **Kensho LLM-Ready API:** Natural language interface for LLM integration

#### Available Data Services
- **Fundamental Data:** Income statements, balance sheets, cash flows
- **Valuations & Pricing:** Historical and current pricing
- **Business Entity Cross Reference:** Link multiple identifiers
- **Global Instruments Cross Reference:** Identify instrument relationships
- **Industry Cross Reference:** Industry classification linkages
- **S&P Global Credit Ratings:** Credit ratings and research
- **Reference & Terms:** Terms and conditions data
- **Segment Data:** Company segment information

#### Authentication & Access
- **API Catalog:** Centralized portal for API exploration
- **Swagger Integration:** Previously standalone, now integrated into API Catalog
- **Documentation:** Available through Marketplace support site

#### Integration Complexity
- **Moderate:** Comprehensive data requires understanding of mnemonic system
- **Python SDK Advantage:** Simplifies integration for Python workflows
- **Pandas Integration:** Seamless DataFrame support reduces data transformation needs
- **LLM-Ready API:** New natural language interface may simplify future integrations

#### Key Innovations
- **Kensho LLM-Ready API:** Natural language queries to S&P datasets
  - S&P Capital IQ Financials
  - Market Data
  - Business Relationships
  - Earnings Call Transcripts
  - Company Intelligence
  - M&A Transactions

#### Considerations
- Mnemonic-based queries require learning CapIQ data structure
- Python SDK significantly reduces integration complexity
- LLM-Ready API may be ideal for AI-driven use cases
- Comprehensive coverage requires appropriate subscription packages

**Sources:**
- [S&P Capital IQ API Documentation](https://api-ciq.marketintelligence.spglobal.com/gds/swagger/index.html)
- [SPGMICIQ Python Package](https://pypi.org/project/SPGMICIQ/)
- [S&P Global Marketplace API Solutions](https://www.marketplace.spglobal.com/en/solutions/api-solutions-(61953ac7-ea64-4fac-926a-feb7f846c2be))
- [API Developer's Guide](https://www.support.marketplace.spglobal.com/content/dam/spglobal/mi/en/documents/marketplace/api/guides/spglobalapidevelopersguide.pdf)
- [Kensho LLM-Ready API Overview](https://docs.kensho.com/llmreadyapi/overview)

---

### BipSync (Research Management System)

**Website:** [bipsync.com](https://bipsync.com/)

#### API Capabilities
- **Comprehensive API:** Described as "secret weapon" used internally
- **REST-like API:** Managing individual items of content
- **GraphQL API:** Fetch properties and follow references in single requests
- **Custom Scripting System:** Client-crafted integrations on demand or scheduled

#### Integration Features
- **Data Import/Export:** Bidirectional data flow
- **Customized Backups:** Trigger automated backups
- **Custom Reports:** Generate reports via API
- **Third-Party Integration:** API used for proprietary system integration

#### Known Integrations
- **Canoe Intelligence:** Document transfer via API integration
- **Addepar:** Portfolio management integration
- **Microsoft Exchange:** Email integration
- **Bloomberg Terminal:** Terminal integration

#### API Architecture
- **Flexible Design:** Used for data migrations, backups, ad-hoc integrations
- **Client Accessible:** Heavily used by BipSync clients
- **Open-Source Infrastructure:** Seamless integration for partners

#### Integration Complexity
- **Moderate:** API exists but documentation not publicly available
- **Client-Specific:** Likely requires direct engagement with BipSync for API access
- **Well-Supported:** Active internal use suggests mature API
- **Custom Scripting:** Flexibility for tailored integrations

#### Critical for Use Cases
BipSync API access is **CRITICAL** for:
- IR-01: Earnings Preview Generator (internal expectations)
- IR-03: Research Document Q&A Bot (internal research)
- IR-08: Investment Memo First Draft (internal views)
- Multiple other use cases requiring access to internal research notes

#### Key Considerations
- API documentation requires client access/direct engagement
- GraphQL support enables efficient data fetching
- Custom scripting allows tailored workflows
- Integration likely requires BipSync support involvement

#### Action Required
- **Contact BipSync** to obtain API documentation and access credentials
- **Clarify Data Access:** Confirm available endpoints for research notes, analyst views
- **Understand Limits:** Rate limits, data permissions, authentication requirements

**Sources:**
- [Bipsync Research Management Software](https://bipsync.com/)
- [API Expansion: RMS 129](https://bipsync.com/blog/api-expansion-enhanced-widgets-rms-129/)
- [Bipsync Resources](https://bipsync.com/resources/)
- [2024 Bipsync RMS Technology Overview](https://bipsync.com/blog/bipsync-rms-technology-overview/)
- [Canoe-Bipsync Integration](https://canoeintelligence.com/canoe-and-bipsync-integration-gains-traction-with-30-client-wins/)

---

### Tegus (Transcripts & Expert Network)

**Primary Access:** Via AlphaSense API
**Website:** [tegus.com](https://www.tegus.com/)

#### API Access Method
- **AlphaSense API Integration:** Primary programmatic access
- **Expert Transcripts API:** JSON format access
- **AlphaSense Developer Portal:** [developer.alpha-sense.com](https://developer.alpha-sense.com/)

#### Content Coverage
- **200,000+ transcripts** covering 25,000+ companies
- **Public Companies:** SEC filings, earnings call transcripts
- **Private Companies:** Expert call transcripts (compliance-approved 1:1)
- **Coverage:** Every major sector

#### API Endpoint
- **Base URL:** `https://api.alpha-sense.com/gql`
- **Format:** GraphQL API
- **Data Format:** JSON transcripts

#### Authentication
- AlphaSense authentication required
- API access tied to AlphaSense/Tegus subscription

#### Integration Complexity
- **Low to Moderate:** Access via AlphaSense API
- **GraphQL:** Single query can fetch comprehensive transcript data
- **Well-Documented:** Sample use cases available in AlphaSense developer docs
- **Direct Tegus API:** Not publicly available; access through AlphaSense

#### Key Capabilities
- Pull latest expert transcripts programmatically
- Search and filter transcripts
- Extract transcript content in structured JSON
- Access metadata (date, company, expert type)

#### Use Case Applications
- IR-04: Automated Research Digest (transcript summaries)
- IR-07: Expert Call Insight Extractor (primary data source)
- MI-07: Management Commentary Tracker (earnings call tracking)

#### Considerations
- Requires both Tegus and AlphaSense subscriptions for API access
- API access may be add-on to standard subscription
- GraphQL enables efficient querying
- Transcript content subject to compliance restrictions

#### Action Required
- **Verify AlphaSense API Access:** Confirm current subscription includes API
- **Test API Endpoint:** Validate authentication and data access
- **Understand Limits:** Confirm rate limits and usage restrictions

**Sources:**
- [Tegus Transcript Library](https://www.tegus.com/transcript-library)
- [API Tracker: Tegus](https://apitracker.io/a/tegus)
- [AlphaSense: Pulling Expert Transcripts](https://developer.alpha-sense.com/api/next/getting-started/sample-use-cases/etl)
- [Tegus Expert Transcript Library Introduction](https://help.alpha-sense.com/hc/en-us/articles/43785894151699-Introduction-to-Tegus-Expert-Transcript-Library)

---

## Summary: Integration Complexity Assessment

### Low Complexity (Easier Integration)
1. **FactSet:** Modern REST APIs, OAuth 2.0, comprehensive SDKs, excellent documentation
2. **Tegus (via AlphaSense):** GraphQL API, clear documentation, JSON format

### Moderate Complexity (Standard Integration)
1. **S&P CapIQ:** Mnemonic system learning curve, but Python SDK helps significantly
2. **BipSync:** API exists but requires client engagement for documentation

### High Complexity (Significant Setup)
1. **Bloomberg:** Enterprise setup, authentication complexity, infrastructure requirements

---

## Critical Action Items

### Immediate Actions
1. **BipSync API Access:**
   - Contact BipSync to obtain API documentation
   - Request developer credentials and authentication details
   - Clarify available endpoints for internal research notes

2. **Verify AlphaSense API:**
   - Confirm current subscription includes API access
   - Obtain API credentials
   - Test transcript data access

3. **Assess Bloomberg Options:**
   - Confirm current terminal licenses
   - Evaluate Desktop API vs. Server API needs
   - Determine if enterprise SAPI is required

### Documentation Needed
1. **FactSet:** Access developer portal, generate API keys or OAuth credentials
2. **S&P CapIQ:** Access Marketplace, review mnemonic documentation
3. **BipSync:** Obtain client-specific API documentation
4. **AlphaSense/Tegus:** Review developer portal and sample code

### Licensing Verification
- Confirm all vendor subscriptions include programmatic API access
- Identify any upgrade requirements for API usage
- Clarify data entitlements and usage restrictions

---

## Recommendations for Use Case Sizing

### Favorable API Conditions (Reduce Size Estimate)
- FactSet, Tegus/AlphaSense have modern, well-documented APIs
- Python SDK availability (FactSet, S&P CapIQ) simplifies integration
- OAuth 2.0 authentication is straightforward

### Challenges to Consider (Increase Size Estimate)
- BipSync requires direct engagement for API access
- Bloomberg may require significant infrastructure setup
- Multiple vendor integration compounds authentication complexity
- Data normalization across vendors adds development time

### Conservative Sizing Principle
Given solo developer context, assume:
- 1-2 weeks for each new vendor API integration (learning, auth setup, testing)
- Additional 1 week for data normalization across multiple vendors
- Authentication troubleshooting buffer (OAuth, API keys, permissions)

---

## Next Steps: Tier 2 Vendor Research

After completing use case analysis with Tier 1 vendors, research:
1. **AlphaSense:** Search and intelligence API (beyond Tegus transcripts)
2. **Enfusion:** Tax lot and position data API
3. **Expert Networks:** API access for AlphaSights, Dialectica, Guidepoint
4. **Visible Alpha:** Granular estimate data API
5. **Daloopa:** Model extraction API
