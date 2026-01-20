# T-Shirt Sizing Guide for AI Use Cases

**Context:** Solo developer environment with capacity to hire/contract, but preference for conservative approach. Goal is to deliver incremental wins to demonstrate value before committing significant resources.

**Philosophy:** Be conservative with estimates, account for dependencies, and prioritize sustainable development pace.

---

## Size Definitions

### Small (S)
**Timeline:** 2-week sprint (10 working days)

**Characteristics:**
- Can be completed solo without external help
- Can run in parallel with other small projects
- Delivers tangible, demonstrable value quickly
- Minimal or no formal specification needed
- Low technical risk

**Developer Capacity:**
- Solo developer can handle 2-3 Small projects in parallel
- Ideal for testing assumptions and proving concepts
- Good candidates for "quick wins"

**Examples:**
- Simple data extraction and formatting
- Basic alert/notification system with existing data
- Straightforward report generation with templates
- Single-vendor API integration (well-documented API)

**Success Criteria:**
- User sees immediate value
- No complex dependencies
- Clear, achievable scope

---

### Medium (M)
**Timeline:** Multiple sprints (4-8 weeks)

**Characteristics:**
- Solo-capable but requires sustained focus
- Can still run in parallel with other work (with context switching)
- Delivers meaningful ROI
- Requires light technical specification
- Moderate technical complexity
- May involve 2-3 system integrations

**Developer Capacity:**
- Solo developer can handle 1-2 Medium projects in parallel
- Requires planning and milestone tracking
- Benefits from user feedback during development

**Examples:**
- Multi-vendor data aggregation with normalization
- Interactive dashboard with moderate complexity
- Workflow automation involving 3-4 steps
- Integration of 2-3 APIs with data transformation
- Document processing with classification

**Success Criteria:**
- Light spec with key requirements documented
- Iterative development with mid-project check-ins
- Clear acceptance criteria defined upfront

---

### Large (L)
**Timeline:** Multi-month project (2-4 months)

**Characteristics:**
- At the edge of solo developer capacity
- Requires exclusive focus (minimal parallel work)
- Substantial time commitment
- Requires extensive technical specification
- Needs product review and stakeholder alignment
- May involve significant architecture decisions
- Would benefit from additional developer/contractor

**Developer Capacity:**
- Solo developer should focus on ONE Large project at a time
- Requires formal milestone structure
- Regular status reviews and course corrections needed
- Consider hiring to accelerate or de-risk

**Examples:**
- Comprehensive data warehouse integration
- Complex multi-step workflow with human-in-the-loop
- Advanced analytics or ML model integration
- System requiring multiple interdependent components
- Projects with 5+ vendor integrations

**Success Criteria:**
- Extensive tech spec with architecture review
- Defined milestones with deliverables
- Stakeholder sign-off on approach
- Regular review cycles (bi-weekly or monthly)
- Clear success metrics

**Risk Mitigation:**
- Break into phases with incremental delivery
- Consider contractor support for specific components
- Plan for iterations and refinements

---

### Extra Large (XL) and Beyond
**Timeline:** 4+ months, potentially ongoing

**Characteristics:**
- Beyond reasonable solo developer scope
- Team-sized commitment
- Likely all-consuming for solo developer
- Requires formal SDLC process
- Should be broken into smaller sub-projects
- May require specialized expertise
- High risk if attempted solo

**Developer Capacity:**
- **Not recommended for solo execution**
- Requires team or significant contractor support
- Needs project manager or technical lead
- Formal project governance required

**Examples:**
- Building a comprehensive ML pipeline from scratch
- Enterprise-scale data platform
- Complex financial modeling system
- Real-time processing infrastructure at scale
- Projects that are "businesses unto themselves"

**Recommended Approach:**
- **Partner or license** rather than build from scratch
- If building, assemble a team with specialized skills
- Break into Large/Medium phases with validation gates
- Consider if this is truly required or if simpler solution exists

**Critical Questions:**
- Can we license/partner instead of building?
- Can scope be reduced to Large or Medium?
- Do we have the specialized expertise required?
- What's the opportunity cost vs. other projects?

---

## Sizing Modifiers: Adjusting Estimates

### Factors That Reduce Size Estimate

**Favorable API Conditions:**
- Vendor has modern REST API with comprehensive documentation
- SDK available in Python or preferred language
- OAuth 2.0 or simple API key authentication
- Active developer community and examples

**Existing Infrastructure:**
- Data warehouse or database already available
- Authentication/authorization already built
- Deployment pipeline exists
- Monitoring and logging in place

**Clear Requirements:**
- User has specific, detailed requirements
- Templates or examples exist
- Acceptance criteria well-defined
- Minimal ambiguity

**Data Availability:**
- Required data already accessible
- Data quality is good
- No complex ETL required
- APIs return structured, clean data

### Factors That Increase Size Estimate

**API/Data Challenges:**
- No public API documentation
- Requires vendor engagement for access
- Complex authentication (custom protocols)
- Data quality issues require extensive cleaning
- Rate limits require complex retry logic

**Missing Infrastructure:**
- No data storage infrastructure
- Need to build authentication from scratch
- Deployment pipeline needs creation
- No existing similar projects to reference

**Multiple Dependencies:**
- Requires 4+ vendor integrations
- Data normalization across disparate sources
- Complex cross-system workflows
- Each vendor adds 1-2 weeks

**Ambiguous Requirements:**
- Scope not well-defined
- Iterative discovery needed
- Multiple stakeholders with different needs
- Requirements may change during development

**Technical Complexity:**
- Real-time processing required
- ML/AI model training needed
- Complex calculations or algorithms
- Performance optimization critical

---

## Conservative Sizing Principles

### General Rules

1. **Add Buffer for Learning:**
   - First integration with a new vendor: +1 week
   - New technology or framework: +1-2 weeks
   - Complex domain knowledge required: +1-2 weeks

2. **Account for Integration Overhead:**
   - Each additional vendor integration: +1 week
   - Data normalization across vendors: +1 week
   - Authentication troubleshooting: +0.5 weeks

3. **Plan for Iteration:**
   - Initial implementation: 70% of time
   - Testing and refinement: 20% of time
   - User feedback and adjustments: 10% of time

4. **Consider Context Switching:**
   - Running 2 projects in parallel: add 15% to each
   - Running 3 projects in parallel: add 25% to each

### Vendor-Specific Adjustments

**Based on API Research:**

**Low Overhead (+0-1 week):**
- FactSet (modern REST, good docs, SDK available)
- Tegus via AlphaSense (GraphQL, clear docs)

**Moderate Overhead (+1-2 weeks):**
- S&P CapIQ (mnemonic learning curve, but Python SDK helps)
- BipSync (requires vendor engagement for docs)

**High Overhead (+2-3 weeks):**
- Bloomberg (enterprise setup, infrastructure requirements)
- Any vendor requiring custom scraping or complex authentication

### Infrastructure Build-Out

**If foundational infrastructure doesn't exist:**

**Document Repository & RAG System:** +4-6 weeks (Large)
- Vector database setup
- Document ingestion pipeline
- Search and retrieval system
- RAG prompt engineering

**Financial Data Warehouse:** +6-8 weeks (Large)
- Data model design
- ETL pipeline development
- Multi-vendor normalization
- Data quality checks

**Slack Integration Framework:** +2-3 weeks (Medium)
- Bot authentication
- Command parsing
- Interactive messages
- Error handling

**Impact on Dependent Projects:**
- Without infrastructure: project sizes increase by 1-2 levels
- Example: Small → Medium, Medium → Large

---

## Sizing Worksheet

When sizing a new use case, answer these questions:

### 1. Core Functionality
- [ ] What is the primary function?
- [ ] How many distinct steps or components?
- [ ] Estimated LOC or complexity?

### 2. Data Sources
- [ ] How many data sources/vendors?
- [ ] Are APIs available and documented?
- [ ] Is data clean or does it need transformation?
- [ ] List vendors: _______________

### 3. Dependencies
- [ ] Does required infrastructure exist?
- [ ] List infrastructure needs: _______________
- [ ] Are there blocking dependencies on other projects?

### 4. Output & Delivery
- [ ] What is the output format?
- [ ] Where is output delivered? (Slack, email, dashboard)
- [ ] Is human-in-the-loop required?

### 5. Integration Overhead
- [ ] New vendor integrations: ___ (count)
- [ ] Auth complexity: Low / Medium / High
- [ ] Data normalization: Yes / No

### 6. Requirements Clarity
- [ ] Are requirements specific and clear?
- [ ] Do templates or examples exist?
- [ ] Is scope well-bounded?

### 7. Initial Estimate
- Base estimate: _______________
- Vendor overhead: +___ weeks
- Infrastructure overhead: +___ weeks
- Learning curve: +___ weeks
- Buffer (10-20%): +___ weeks
- **TOTAL: ___ weeks → Size: ___**

---

## Examples: Applying the Guide

### Example 1: Automated Research Digest (IR-04)

**Analysis:**
- Core: Aggregate and summarize research (2-3 components)
- Data: 2-3 sources (email, vendor feeds)
- Output: Daily email digest
- Infrastructure: Needs document repository if doesn't exist

**Estimate:**
- Base: 2 weeks (straightforward aggregation)
- Vendor integration (2 sources): +1 week
- If no document repository: +6 weeks
- **Without infrastructure: Large (2+ months)**
- **With infrastructure: Small to Medium (2-4 weeks)**

### Example 2: Portfolio Scenario Analyzer (IR-11)

**Analysis:**
- Core: Complex financial modeling and scenario analysis
- Data: Comprehensive portfolio, market, factor data
- ML: Requires production ML pipeline
- Expertise: Beyond typical LLM application scope

**Estimate:**
- Base: 8-12 weeks (ML engineering project)
- Data infrastructure: +6-8 weeks
- Model validation: +4 weeks
- Reporting system: +2 weeks
- **TOTAL: 20-26 weeks → Extra Large (XL)**
- **Recommendation: Partner/license instead of build**

### Example 3: Expert Call Insight Extractor (IR-07)

**Analysis:**
- Core: Extract insights from transcripts (single function)
- Data: 1 source (Tegus via AlphaSense API)
- Output: Structured summary
- Infrastructure: Minimal (API call + LLM processing)

**Estimate:**
- Base: 1 week (API + prompt engineering)
- Tegus/AlphaSense integration: +0.5 weeks
- Testing and refinement: +0.5 weeks
- **TOTAL: 2 weeks → Small**

---

## Size Distribution Goals

For a portfolio of 60 use cases:

**Ideal Distribution:**
- Small (S): 20-30% (12-18 projects) - Quick wins
- Medium (M): 40-50% (24-30 projects) - Core functionality
- Large (L): 15-25% (9-15 projects) - Strategic investments
- Extra Large (XL+): 5-10% (3-6 projects) - Consider alternatives

**Red Flags:**
- Too many Large or XL projects → infeasible for solo dev
- Too many Small projects → may indicate under-scoping
- All similar size → lacks strategic prioritization

---

## Decision Framework: Build vs. Buy/Partner

For Large and XL projects, strongly consider alternatives:

### Build If:
- [ ] Core to competitive advantage
- [ ] Requirements are unique to organization
- [ ] No suitable vendors exist
- [ ] Cost of licensing is prohibitive
- [ ] In-house expertise exists

### Buy/Partner If:
- [ ] Commodity functionality (available in market)
- [ ] Requires specialized expertise you lack
- [ ] Time-to-market is critical
- [ ] Vendor solution is mature and proven
- [ ] TCO of licensing < TCO of building

**Examples from Use Cases:**
- **Build:** Document repository, internal research tools
- **Buy/Partner:** Portfolio scenario analysis, backtesting systems, compliance monitoring

---

## Revision History

**v1.0 - January 2026**
- Initial sizing definitions based on solo developer context
- Vendor-specific adjustments from Tier 1 API research
- Conservative principles for sustainable development pace
