# AI Infrastructure and Strategic Roadmap
## Comprehensive Analysis of 60 AI Use Cases for Financial Services Firm

---

## 1. Introduction

This document provides a comprehensive infrastructure analysis across all 60 AI use cases identified for the firm, spanning Investment Research, Market Intelligence, Private Markets, Operations & Finance, Legal & Compliance, Investor Relations, Corporate Access, and Administrative functions.

### Purpose
- **Identify shared dependencies**: Determine which infrastructure components enable multiple use cases
- **Define foundational building blocks**: Establish Tier 1, 2, and 3 infrastructure priorities
- **Create strategic roadmap**: Phase implementation to maximize early ROI while building sustainable foundation
- **Highlight quick wins**: Identify small projects that validate infrastructure and deliver immediate value
- **Inform build vs. buy decisions**: Consolidate vendor evaluation opportunities across all sections

### Document Organization
This document extracts all "Shared Infrastructure" sections from the detailed use case analysis (AI_use_cases_v2.md), then synthesizes cross-cutting insights to create:
- Master building block analysis (Tier 1/2/3 infrastructure)
- Strategic implementation roadmap (4 phases)
- Quick wins analysis (small projects grouped by dependency)
- Build vs. buy recommendations (consolidated vendor opportunities)
- Project overlap and consolidation opportunities

---

## 2. Section Infrastructure Analysis (Extracted from AI_use_cases_v2.md)

### 2.1 Investment Research & Analysis — Shared Infrastructure

#### Critical Shared Dependencies

**1. Financial Data Warehouse**
- **Required for:** IR-01, IR-05, IR-06, IR-08, IR-09, IR-11, IR-12, IR-13
- **Components:** Consensus estimates, historical financials, forward estimates, company fundamentals
- **Impact:** This is the single most critical dependency. Without comprehensive financial data infrastructure, 8 of 13 IR projects have dramatically increased scope.

**2. Trading/Market Data Infrastructure**
- **Required for:** IR-05, IR-06, IR-09, IR-11, IR-12, IR-13
- **Components:** Real-time and historical pricing, trading multiples, portfolio positions, returns data
- **Impact:** 6 projects require reliable access to market data and trading information.

**3. Document Repository & RAG System**
- **Required for:** IR-02, IR-03, IR-04, IR-07, IR-08, IR-10
- **Components:** Research documents, investment memos, expert transcripts, broker research, earnings call transcripts, company filings
- **Impact:** A centralized, searchable document repository with semantic search is foundational for 6 projects.

**4. Slack Integration Framework**
- **Required for:** IR-01, IR-02, IR-03, IR-06
- **Components:** Bot authentication, channel posting, interactive commands, file uploads
- **Impact:** 4 projects require Slack integration. Building a solid Slackbot framework early reduces duplicate effort.

**5. Internal Knowledge Base (BipSync/Notes)**
- **Required for:** IR-01, IR-03, IR-08
- **Components:** Internal research notes, analyst views, proprietary analysis
- **Impact:** Connecting to internal notes system enables comparison of internal vs. Street views.

**6. Event & Calendar Feed**
- **Required for:** IR-01, IR-10
- **Components:** Earnings calendar, macro event monitoring
- **Impact:** Reliable event detection and scheduling triggers.

#### Recommended Implementation Sequence

**Phase 1 — Foundation (High ROI, enables other projects):**
1. Document Repository & RAG System → Enables IR-02, IR-03, IR-04, IR-07, IR-08
2. Financial Data Warehouse → Enables IR-01, IR-05, IR-08, IR-09, IR-12
3. Slack Integration Framework → Reduces overhead for IR-01, IR-03, IR-06

**Phase 2 — Pilot Projects (Test infrastructure):**
1. IR-01: Earnings Preview Generator (tests financial data + Slack + internal notes)
2. IR-07: Expert Call Insight Extractor (straightforward, tests document processing)
3. IR-04: Automated Research Digest (tests document repository, delivers immediate value)

**Phase 3 — Advanced Capabilities:**
1. IR-08: Investment Memo First Draft (requires mature document repository)
2. IR-05: Company Comps Generator (requires financial + trading data)
3. IR-03: Research Document Q&A Bot (aggregates learnings from prior projects)

**Avoid Until Infrastructure Matures:**
- IR-11: Portfolio Scenario Analyzer (partner/license instead of build)
- IR-13: Trading Strategy Back-tester (partner/license instead of build)
- IR-06: Consensus Estimate Change Monitor (significant real-time infrastructure if not hourly/daily)

---

### 2.2 Market Intelligence — Shared Infrastructure

#### Critical Shared Dependencies

**1. News & Research Feeds (Bloomberg, FactSet, AlphaSense)**
- **Required for:** MI-01, MI-02, MI-03
- **Components:** News APIs, feed normalization, deduplication
- **Impact:** Foundation for all news-based monitoring. Same as IR-04 dependency.
- **Cross-reference:** IR section infrastructure #3 (Document Repository) overlaps here

**2. Transcript Access (Tegus/AlphaSense)**
- **Required for:** MI-07
- **Components:** Transcript API, parsing, storage
- **Impact:** Same dependency as IR-07
- **Cross-reference:** IR section infrastructure #3

**3. SEC Filing Access**
- **Required for:** MI-02, MI-04
- **Components:** Filing feeds (Bloomberg/FactSet/Tegus), parsing logic
- **Impact:** Medium complexity if vendor-provided, High if building EDGAR scraper

**4. Alternative Data Integration**
- **Required for:** MI-06 (Revealera for hiring data)
- **Components:** Alt data vendor APIs, data normalization
- **Impact:** Each new alt data source adds integration overhead

**5. Sentiment/Social Data**
- **Required for:** MI-05
- **Components:** Social platform APIs or sentiment vendor integration
- **Impact:** **CRITICAL BUILD VS BUY DECISION** - don't build from scratch

#### Cross-Section Dependencies

- **Document Repository (from IR):** MI-07 needs same storage as IR-07
- **Slack Integration (from IR):** If alerts preferred, reuse IR Slackbot framework
- **Output Delivery:** Email digest vs Slack vs dashboard affects all MI projects

#### Key Observations

**Aggregation Strategy Wins:**
- All projects sized assuming we aggregate existing feeds, not build monitoring
- This keeps Small projects at 2 weeks, Medium at 4-8 weeks, Large at 2-4 months
- Building from scratch would push everything to XL+ (not feasible solo)

**Real-Time Consideration:**
- None of these projects sized for true real-time (sub-hour latency)
- Recommend hourly or daily batches for V1
- If real-time truly required, infrastructure costs increase dramatically

**Data Source Dependencies:**
- Most projects depend on vendor APIs being accessible and usable
- Each "if data source doesn't exist" adds 1-2 size levels
- Verify vendor API access before committing to timeline

**Critical Questions for All MI Projects:**
1. What's the actual latency requirement? (Real-time vs hourly vs daily)
2. Output delivery preference? (Email < Slack < Dashboard)
3. Approximately how many portfolio companies? (15-50 range estimated)
4. Verify all assumed vendor data sources are accessible via API/export

#### Recommended Implementation Sequence

**Quick Wins (if data sources exist):**
1. **MI-04: SEC Filing Monitor** (Small-Medium) - likely vendor feeds exist
2. **MI-06: Hiring Pattern Intelligence** (Small) - Revealera on vendor list

**Medium Complexity (after quick wins):**
3. **MI-01: Portfolio Company News Monitor** (Medium) - foundation for other news projects
4. **MI-07: Management Commentary Tracker** (Large, or Medium if scope limited) - similar to IR-07

**Higher Complexity (later phases):**
5. **MI-03: Industry News Synthesizer** (Large) - hub project, builds on MI-01
6. **MI-02: Competitor Intelligence Tracker** (Large) - aggregates MI-01, MI-04, MI-06

**Evaluate Separately:**
7. **MI-05: Social Sentiment** (XL+) - requires buy vs build analysis before proceeding

---

### 2.3 Private Markets — Shared Infrastructure

#### Critical Shared Dependencies

**1. Document Processing Infrastructure**
- **Required for:** PM-01, PM-02, PM-03, PM-04
- **Components:** PDF/Excel/Word parsing, OCR for scanned docs, structured data extraction
- **Impact:** Foundation for all document-based PM projects. High variability in document formats increases complexity.

**2. Egnyte Integration**
- **Required for:** PM-01, PM-02
- **Components:** Folder monitoring, file upload triggers, document access API
- **Impact:** Enables automated triggers when new documents arrive

**3. Financial Data Access (from IR section)**
- **Required for:** PM-01 (public comps comparison)
- **Components:** FactSet/CapIQ for public company metrics
- **Impact:** Cross-reference to IR Financial Data Warehouse
- **Cross-section dependency:** IR infrastructure #1

**4. Corporate Document Archive**
- **Required for:** PM-01, PM-03
- **Components:** Historical deal documents, term sheets, investment agreements, CIMs
- **Impact:** Critical for comparison features. If not structured, adds 4-6 weeks to projects requiring this data.
- **Key question:** Does structured archive exist or need to be built?

**5. Private Company Data (PitchBook/Preqin)**
- **Required for:** PM-01, PM-03
- **Components:** Market deal terms, valuation benchmarks, historical private transactions
- **Impact:** Enables market comparison features

**6. Data Standardization Pipeline**
- **Required for:** PM-04 (builds this), PM-05 (depends on this)
- **Components:** Metric extraction, template population, variance tracking, time-series storage
- **Impact:** PM-04 creates this infrastructure; PM-05 leverages it

**7. RAG Infrastructure (from IR section)**
- **Required for:** PM-05
- **Components:** Vector database, semantic search, Q&A interface
- **Impact:** PM-05 is essentially IR-03 for private markets
- **Cross-section dependency:** IR infrastructure #3

#### Cross-Section Dependencies

- **Document Repository (IR):** PM projects need similar doc processing as IR section
- **RAG System (IR):** PM-05 directly depends on IR-03 infrastructure
- **Financial Data (IR):** PM-01 needs public market data for comps

#### Key Observations

**Build vs Buy Considerations:**
- **PM-03 (Deal Terms):** Strong candidate for partnering with platforms like Harvey. High hallucination risk with serious consequences.
- **PM-02 (Data Room):** Consider if existing due diligence platforms offer better solutions
- Recommend narrow scope pilots before full builds

**Sequencing Matters:**
- **PM-04 enables PM-05:** Data standardization pipeline in PM-04 makes PM-05 significantly easier
- **PM-05 may be feature of IR-03:** Not standalone project, but extension of Research Q&A Bot to private markets data
- **Corporate document archive is critical:** If doesn't exist, multiple projects (PM-01, PM-03) become significantly more complex

**Document Variability Risk:**
- Private markets documents (CIMs, data rooms, updates) have high format variability
- Each format variation adds development time
- OCR quality for scanned documents can be poor
- Budget extra time for parsing edge cases

**Critical Questions for All PM Projects:**
1. How many private deals/portfolio companies? (Affects ROI calculation)
2. Does structured corporate document archive exist?
3. What format consistency exists in CIMs, data rooms, portfolio company reports?
4. Is there existing diligence checklist/workflow we can follow?

#### Recommended Implementation Sequence

**Foundation First:**
1. **Corporate Document Archive** — If doesn't exist, building this unlocks PM-01 and PM-03. Could be Large project itself.
2. **Document Processing Infrastructure** — Shared across all PM projects

**Quick Win (if data available):**
3. **PM-04: Update Processor** (Medium) — Builds data standardization pipeline, enables PM-05

**Medium Complexity:**
4. **PM-01: CIM Analyzer** (Medium-Large) — Start without comparisons (Medium), add comparisons phase 2
5. **PM-05: Q&A Bot** (Medium) — After PM-04, consider as feature of IR-03

**Higher Complexity:**
6. **PM-02: Data Room Processor** (Large) — Complex due to document volume and variety

**Evaluate Separately:**
7. **PM-03: Deal Terms** (Medium-Large) — Build vs buy decision, high hallucination risk. Consider Harvey or similar platform.

#### Strategic Notes

**PM Section Maturity:**
- Private markets projects depend heavily on whether corporate document infrastructure exists
- If starting from scratch, recommend building document archive as Phase 1 (potentially Large project)
- Many PM projects are document processing variations - shared infrastructure has high ROI

**Integration with IR Section:**
- PM-05 should likely be integrated with IR-03 rather than separate bot
- Financial data needs for PM-01 already covered by IR infrastructure
- Document processing patterns similar to IR use cases

---

### 2.4 Operations & Finance — Shared Infrastructure

#### Critical Shared Dependencies

**1. Enfusion Data Infrastructure**
- **Required for:** OF-07 (critical), OF-08 (possibly), OF-10 (possibly)
- **Components:** Regular API access, scheduled data pulls, structured storage, data warehouse
- **Impact:** This is a FOUNDATIONAL project that unlocks multiple OF use cases
- **Recommendation:** Build as standalone infrastructure project first
- **Size estimate:** Medium to Large standalone project

**2. Accounting System Integration (QuickBooks + others)**
- **Required for:** OF-02, OF-03, OF-04, OF-05, OF-06, OF-08, OF-09
- **Components:** API access, journal entry posting, data extraction, budget access
- **Impact:** 7 of 11 OF projects depend on accounting system access
- **QuickBooks mentioned for Mgmt Co** - need to confirm other systems for funds

**3. Fund Administration System Access**
- **Required for:** OF-09, OF-05, OF-06
- **Components:** Investor records, transaction data, NAV/AUM data, side letter terms
- **Impact:** Critical for fee calculations and capital flows reporting

**4. Internal Trade Tracking System**
- **Required for:** OF-10 (makes easier)
- **Components:** Trade capture, position tracking, settlement tracking
- **Impact:** If built robustly, OF-10 becomes additional feature rather than standalone project

**5. Slack Integration (from IR/MI sections)**
- **Required for:** OF-10
- **Components:** Bot framework, channel posting, alerts
- **Cross-reference:** IR/MI Slack infrastructure can be reused

#### Cross-Section Dependencies

- **Document Repository:** Not heavily used in OF, but OF-11 needs document storage
- **Slack Integration:** OF-10 uses same infrastructure as IR/MI sections

#### Key Observations

**Many Projects Are NOT AI:**
- **Traditional scripting/calculation:** OF-05, OF-06, OF-08, OF-09, OF-10 are deterministic logic
- **LLMs bad at math:** Fee calculations (OF-05, OF-06) should not use LLMs for computation
- **Actual AI opportunities:** OF-02 anomaly detection, OF-10 suggested resolutions, OF-11 document extraction

**Workflow Observation Required:**
- **OF-01, OF-03, OF-04, OF-08:** Need to observe existing workflows before sizing definitively
- **Better approach:** Identify specific pain points, build targeted tools vs full automation
- **Risk:** Building without understanding current process leads to unused features

**Build vs Buy Considerations:**
- **OF-01 (Expense Reports):** Modern platforms (Brex, Airbase) likely already solve this
- **OF-03 (Month-End Close):** Existing accounting software may have better automation
- **OF-04 (Budget Prep):** Budgeting software may be better investment than custom build
- **OF-11 (Statement Recon):** Specialized reconciliation tools may exist

**High-Risk, High-Accuracy Projects:**
- **OF-05, OF-06 (Fee Calculations):** Errors have serious investor relations consequences
- **OF-10, OF-11 (Reconciliation):** Financial accuracy critical
- **Recommendation:** Human review mandatory before production use
- **Audit trails required** for compliance

**Sequencing Matters:**
- **Enfusion infrastructure unlocks:** OF-07, potentially OF-08, OF-10
- **OF-03 infrastructure enables:** OF-04 (budget prep leverages close data)
- **OF-05 patterns reused in:** OF-06 (management fee logic → incentive fee)
- **Internal trade tracking enables:** OF-10 as feature vs standalone

#### Critical Questions for All OF Projects

1. **Observe workflows first:** What are current pain points and time-intensive steps?
2. **What accounting/fund admin systems are used?** API access availability?
3. **Is Enfusion data currently accessible?** Export format, API, update frequency?
4. **How many funds/accounts/investors?** Volume affects infrastructure needs
5. **What existing tools are in place?** Can they be leveraged better vs building from scratch?

#### Recommended Implementation Sequence

**Foundation First (enables multiple projects):**
1. **Enfusion Data Infrastructure** (Medium-Large) - Unlocks OF-07, OF-08, OF-10
2. **Accounting System Integration** (Medium) - Enables OF-02, OF-03, OF-04, OF-05, OF-06, OF-08, OF-09

**Quick Wins (if workflows observed):**
3. **OF-08: Cash Position Summary** (Small) - If workflow is straightforward
4. **OF-09: Capital Flows Report** (Small-Medium) - If fund admin API exists

**Medium Complexity:**
5. **OF-02: Spend Analytics** (Medium) - Basic analytics first, consolidation features later
6. **OF-05: Management Fee Calculator** (Small-Medium) - Traditional script, not AI
7. **OF-06: Incentive Fee Calculator** (Medium) - Builds on OF-05 patterns
8. **OF-07: Tax Lot Processor** (Small-Medium) - After Enfusion infrastructure

**Workflow-Dependent (observe first):**
9. **OF-01: Expense Reports** (Medium-XL) - Clarify gap vs existing platforms
10. **OF-03: Month-End Close** (TBD) - Observe workflow, build targeted tools
11. **OF-04: Budget Prep** (Medium or Large) - Depends on OF-03, observe workflow

**Complex/Risky:**
12. **OF-10: Reconciliation Monitor** (Medium) - After trade tracking infrastructure
13. **OF-11: Statement Reconciliation** (Medium) - LLM extraction from limited set of well-structured PDFs (6-7 counterparty formats) with DataFrame comparison

#### Strategic Notes

**OF Section Reality Check:**
- This section has more "non-AI" projects than others (scripting, calculation, data aggregation)
- Many projects need workflow observation before accurate sizing
- Build vs buy decisions are critical - existing fintech tools may be better investments
- Enfusion data infrastructure is THE foundational dependency

**Adjacency to Core Expertise:**
- Some projects (OF-03, OF-04) are somewhat adjacent to core AI/LLM expertise
- Consider if building custom solutions is strategic vs leveraging existing accounting/finance software
- Focus AI resources on problems where LLMs add unique value

**Risk Management:**
- Financial calculations have serious consequences for errors
- All automated financial processes need human review loops
- Audit trails and data lineage are not optional
- Start with read-only reporting before building posting/writing capabilities

---

### 2.5 Legal & Compliance — Shared Infrastructure

#### Critical Shared Dependencies

**1. Document Repository & RAG System (from IR section)**
- **Required for:** LC-03, LC-06
- **Components:** Vector database, semantic search, document processing
- **Impact:** LC-03 and LC-06 are essentially IR-03 for legal documents
- **Cross-section dependency:** IR infrastructure #3
- **Recommendation:** Integrate legal document Q&A into IR-03 rather than building separate systems

**2. Legal Document Processing**
- **Required for:** LC-02, LC-03, LC-04, LC-06
- **Components:** PDF extraction, clause identification, term extraction, comparison logic
- **Impact:** Specialized for legal documents (contracts, side letters, NDAs, fund docs)
- **Hallucination risk:** Legal documents require high accuracy. Errors have serious consequences.
- **Harvey likely covers this:** If using Harvey for contract review, can leverage for other legal doc processing

**3. Trade Data & Compliance Context**
- **Required for:** LC-01
- **Components:** Internal trade data, restricted list, calendar/meeting data, expert call records
- **Impact:** Cross-references trades with compliance constraints and MNPI context
- **Cross-section dependencies:** Operations (trade data), Corporate Access (meetings)

**4. Regulatory Intelligence Feed**
- **Required for:** LC-07
- **Components:** Regulatory updates, SEC/FINRA guidance, compliance deadlines
- **Impact:** Foundation for policy monitoring
- **Build vs buy:** Strong candidate for external subscription service (RIA in a Box, MyComplianceOffice, etc.)

**5. Historical Document Archives**
- **Required for:** LC-02, LC-03, LC-04, LC-05, LC-06
- **Components:** Contracts, side letters, NDAs, fund documents, amendments, prior marketing content with approved disclaimers
- **Impact:** Precedent matching and approved language requires searchable historical corpus
- **Critical for LC-05:** History of marketing disclaimers significantly reduces implementation complexity

#### Cross-Section Dependencies

- **Document Repository (IR):** LC projects heavily depend on IR-03 infrastructure
- **Trade Data (OF):** LC-01 needs trade tracking from OF section
- **Meeting/Calendar Data (CA):** LC-01 cross-references corporate access events for MNPI context

#### Key Observations

**Build vs Buy Is The Theme:**
- **LC-02 (Contract Review):** Harvey already being evaluated by team - strong buy recommendation
- **LC-01 (Trade Surveillance):** Compliance-specific AI tools (Behavox, Smarsh, ComplyAdvantage) likely better than custom build
- **LC-07 (Policy Monitoring):** Regulatory intelligence services already exist
- **LC-04 (NDA Processing):** Entry-level Harvey workflow
- **Theme of this section:** Evaluating products rather than building from scratch
- **Hybrid approach:** Can build integration tools (MCP tools, data feeds) on top of purchased platforms

**Hallucination Risk High:**
- All legal document analysis projects (LC-02, LC-03, LC-04, LC-06) have high stakes
- LLM errors in legal context = liability risk
- Human legal review mandatory before any automated output is used
- Extensive evaluation frameworks required
- **Outside core competency:** Legal/compliance is specialized domain

**Document Repository Overlap:**
- **LC-03 overlaps with InvRel-06** (Side Letter Query Bot) - same or different?
- **LC-03, LC-06 should be features of IR-03** rather than standalone projects
- Consider unified document Q&A system covering: research, side letters, fund documents, contracts
- Building 3+ separate RAG systems is inefficient
- Harvey may already provide unified legal document search

**Non-Engineering Work Significant:**
- **LC-05 (Marketing Footnotes):** Requires compiling history, creating full disclaimer list, documenting approved language
- This prep work makes implementation significantly easier
- 80/20 approach works well - focus on most common cases first

**Small Win Opportunities:**
- **LC-01:** Narrow scope (restricted list check only) = Small
- **LC-05:** Start with performance claims only (most common 80%) = Small to Medium
- **LC-04:** If high volume + standard templates = Small (but likely covered by Harvey)

#### Critical Questions for All LC Projects

1. **What's the Harvey evaluation status?** Many LC projects may already be covered
2. **What compliance-specific AI tools exist?** Beyond Charles River/Bloomberg (e.g., Behavox, Smarsh, ComplyAdvantage)
3. **Do legal document archives exist?** Structured and searchable, or need to be built?
4. **Volume questions:** NDAs per day/week/month? Marketing content frequency? Contract volume?
5. **Can LC projects be features of purchased platforms?** Rather than custom builds

#### Recommended Implementation Sequence

**Evaluate First (Build vs Buy decisions):**
1. **Harvey evaluation** — May cover LC-02, LC-03, LC-04, LC-06
2. **Compliance AI tools** — For LC-01 (trade surveillance)
3. **Regulatory intelligence services** — For LC-07 (policy monitoring)

**Small Win (if not covered by Harvey):**
4. **LC-01: Trade Surveillance** (Small for narrow scope) — Restricted list check only

**After Product Evaluation:**
5. **Build integration tools** (Small-Medium) — MCP tools to connect internal data to purchased platforms
6. **LC-05: Marketing Footnotes** (Small-Medium) — Start with performance claims, requires non-engineering prep work
7. **LC-03/LC-06: Legal Document Q&A** (Medium) — If not using Harvey, integrate into IR-03 infrastructure

**Strategic Notes:**
- **This section is about product evaluation, not building** — Legal/compliance has mature AI solutions
- **Hybrid approach wins:** Buy platforms, build integration/enhancement tools
- **Outside core competency:** Legal document analysis is specialized domain
- **Regulatory risk:** Human review always required, regardless of automation level

---

### 2.6 Investor Relations — Shared Infrastructure

#### Critical Shared Dependencies

**1. Investor Data Warehouse (InvRel-07)**
- **Required for:** InvRel-01, InvRel-02, InvRel-03, InvRel-04, InvRel-05
- **Components:** Investor records, relationship history, transaction history, balances, allocations, meeting notes, DDQ responses
- **Impact:** InvRel-07 is FOUNDATIONAL infrastructure that unlocks most other InvRel projects
- **Size:** Large project itself (data reconciliation, warehousing, dashboard)
- **Critical for success:** Backfilling historical data is essential for usefulness
- **This should be built first** before other InvRel projects

**2. Performance & Attribution Data (from IR section)**
- **Required for:** InvRel-03, InvRel-05
- **Components:** Fund performance, attribution, AUM trends, top contributors/detractors, exposure breakdowns
- **Cross-section dependency:** IR Financial Data Warehouse
- **Impact:** Investor letters and cheat sheets require same performance infrastructure as IR projects

**3. Document Repository & RAG System (from IR section)**
- **Required for:** InvRel-06 (Side Letter Query Bot)
- **Components:** Side letter corpus, semantic search, Q&A interface
- **Cross-section dependency:** IR infrastructure #3
- **Overlap:** InvRel-06 is the SAME as LC-03 - should be one project, not two

**4. Fund Administration System Access**
- **Required for:** InvRel-03, InvRel-04, InvRel-05, InvRel-07
- **Components:** NAV data, investor balances, transaction records, capital flows
- **Impact:** Most InvRel projects need fund admin data

**5. Dashboard Infrastructure**
- **Required for:** InvRel-07
- **Components:** Dashboard framework, reporting tools, data visualization
- **Build vs buy:** Tools like Retool, Sigma Computing, or data warehouse-native tools vs custom build
- **Impact:** Significantly affects InvRel-07 complexity

#### Cross-Section Dependencies

- **Performance Data (IR):** InvRel-03, InvRel-05 need same infrastructure as IR-12
- **RAG System (IR):** InvRel-06 should be part of IR-03 unified document Q&A
- **Side Letters (LC):** InvRel-06 = LC-03, should not be duplicated

#### Key Observations

**InvRel-07 Is Foundational:**
- Large project but unlocks 5+ other InvRel projects
- Data reconciliation, warehousing, and historical backfill are critical
- Dashboard requirement adds significant complexity
- **Recommendation:** Build InvRel-07 first, enables rest of section
- Consider dashboard tooling (Retool, Sigma) vs custom build

**Workflow Integration Complexity:**
- **InvRel-01:** Email integration (Outlook plugin, Chrome extension) is complex
- **Simple approach:** MCP tool or separate interface where user copies draft
- Complex integration can balloon Small project to Large
- **Recommendation:** Start simple (MCP tool), add integration later if needed

**High-Risk Projects:**
- **InvRel-04 (DDQ Response):** Wrong/outdated information = serious consequences with prospective LPs
- Requires response versioning, invalidation tracking, evaluation framework
- Human review mandatory before submission

**Data Dependency Theme:**
- Almost all InvRel projects depend on investor data being accessible
- If data scattered across multiple systems: projects become significantly harder
- Investing in InvRel-07 (data aggregation) has high ROI for entire section

**Not Really AI:**
- **InvRel-07:** Traditional data engineering and ETL, not LLM work
- **InvRel-01, InvRel-03:** Document drafting (straightforward LLM application)
- **InvRel-04:** Q&A matching with versioning logic (hybrid)

#### Critical Questions for All InvRel Projects

1. **Where is investor relationship data currently stored?** (CRM, email, meeting notes, scattered)
2. **How far back does historical data need to go?** Can we backfill?
3. **Fund administration system and API access?**
4. **How many LPs across all funds?**
5. **What's the volume?** (LP meetings, DDQs, communications per month)
6. **Dashboard tooling preference?** (Retool, Sigma, custom, data warehouse-native)

#### Recommended Implementation Sequence

**Foundation First (Large but unlocks others):**
1. **InvRel-07: Investor Data Aggregator** (Large) — Build investor data warehouse, enables InvRel-01, InvRel-02, InvRel-04
   - Evaluate dashboard tooling options (Retool, Sigma, etc.)
   - Focus on historical data backfill
   - Data reconciliation framework

**After InvRel-07 Infrastructure:**
2. **InvRel-01: LP Communication Drafter** (Small with simple workflow) — MCP tool approach first
3. **InvRel-04: DDQ Response** (Medium) — Build response versioning system, evaluation framework
4. **InvRel-02: Meeting Prep Generator** (Medium) — Leverages InvRel-07 data

**After Performance Infrastructure (from IR section):**
5. **InvRel-05: Quarterly Cheat Sheet** (Medium) — Requires performance/attribution data
6. **InvRel-03: Investor Letter Draft** (Medium-Large) — Comprehensive performance data needed

**After IR-03 RAG Infrastructure:**
7. **InvRel-06: Side Letter Query Bot** (Medium) — Add side letters to IR-03, not standalone project
   - **Critical:** Confirm this isn't duplicate of LC-03

#### Overlap Alert: Duplicate Projects

**InvRel-06 = LC-03:**
- Both are "Side Letter Query Bot" / "Side Letter Term Repository"
- Should be ONE project, not two separate entries
- Recommend consolidating in final analysis

**InvRel-02 similar to AD-01:**
- InvRel-02: Investor Meeting Prep (specialized for LPs)
- AD-01: Meeting Prep Automator (general purpose)
- Consider if InvRel-02 is specialized version of AD-01

#### Strategic Notes

**This Section is Data-Heavy:**
- Success hinges on quality of investor data aggregation (InvRel-07)
- Most projects are straightforward once data infrastructure exists
- Without InvRel-07, projects range Medium to Large. With it: Small to Medium

**Dashboard Tooling Decision is Critical:**
- InvRel-07 dashboard requirement is significant complexity driver
- Evaluate tools (Retool, Sigma Computing, Looker, Tableau) before committing to custom build
- Tool choice affects multiple projects across sections (IR-12, OF-02, AD-04)

**Low AI Complexity, High Data Engineering:**
- Most InvRel projects are document drafting or data aggregation
- Real complexity is data engineering (InvRel-07), not AI/LLM
- Focus on data infrastructure first, LLM applications are straightforward

---

### 2.7 Corporate Access — Shared Infrastructure

#### Critical Shared Dependencies

**1. Structured Event Database (CA-01)**
- **Required for:** CA-02, CA-03, CA-04, CA-05
- **Components:** Event records (company, date, location, bank, format), analyst assignments, attendance tracking, RSVP status
- **Impact:** CA-01 is FOUNDATIONAL - all other CA projects depend on structured event data
- **Can use intermediate source:** Outlook calendar as structured data store for MVP simplifies database requirement
- **Historical data important:** CA-03 forecasting requires historical backlog
- **Workflow observation:** CA-05 reporting can help define ideal data model for CA-01

**2. Calendar Integration**
- **Required for:** CA-01, CA-02
- **Components:** Calendar API access (Outlook, Google), multi-user calendar management, conflict detection
- **Impact:** CA-01 creates events, CA-02 manages routing and conflicts
- **Complexity driver:** Managing conflicts is outside core competency (calendar management logic)

**3. Analyst Coverage Mapping**
- **Required for:** CA-01, CA-02
- **Components:** Industry and company lists per analyst, coverage assignments
- **Impact:** Enables automated analyst matching for events
- **Can be simple:** Spreadsheet or basic database sufficient for MVP

**4. Broker Relationship Data**
- **Required for:** CA-04, CA-05
- **Components:** Commission spend tracking, event requests/allocations, research consumption metrics
- **Impact:** Enables broker ROI analysis
- **Existing tool:** CorpAxe (Finiato) on vendor list - broker management may already be tracked
- **Question:** What's already in CorpAxe vs needs to be built?

**5. Email Integration**
- **Required for:** CA-01
- **Components:** Email parsing, event extraction
- **Simple approach:** Specific email address that gets copied on corporate access messages (avoids complex inbox API)

#### Cross-Section Dependencies

- **Calendar Integration:** Similar needs to InvRel-01, InvRel-02 (meeting scheduling)
- **Research Consumption Tracking:** CA-04 needs to know which broker research is being read

#### Key Observations

**CA-01 Is Foundational:**
- Small project but unlocks all other CA projects
- Structured event database enables reporting, forecasting, analytics
- **Workflow observation for CA-05 can inform CA-01 data model** - consider building CA-01 after observing current workflow
- Historical data backlog important for CA-03 forecasting

**Mostly Not AI:**
- **CA-01:** Email parsing (AI), but event extraction fairly straightforward
- **CA-02:** Calendar management (traditional automation)
- **CA-03:** Forecasting/pattern detection (adjacent to core competency)
- **CA-04:** Data aggregation and analytics (traditional BI)
- **CA-05:** Reporting (traditional BI)
- Real AI opportunities are limited in this section

**Workflow Observation Important:**
- **CA-05:** Observe existing reporting workflow to identify:
  - Basic non-AI automations that save time
  - What reports are actually valuable
  - What data model CA-01 should use
- Don't build reports that won't be used

**Adjacent to Core Competency:**
- **CA-02:** Managing calendar conflicts is outside main expertise
- **CA-03:** Forecasting/predictive analytics not core AI/LLM work
- Both are more calendar management / analytics than AI

**Build vs Buy Considerations:**
- **CA-03:** Corporate access management platforms may offer forecasting
- **CA-04/CA-05:** CorpAxe (Finiato) already in use - does it cover broker analytics?
- Research existing tools before building

**Overlap Alert:**
- **CA-04 and CA-05:** Both generate broker/corporate access analytics
- Consider if these should be consolidated into single reporting project
- CA-04 more broker-focused, CA-05 more event-focused, but significant overlap

#### Critical Questions for All CA Projects

1. **What's already in CorpAxe (Finiato)?** Broker management platform on vendor list - what functionality exists?
2. **Observe workflow first:** What corporate access reports are currently generated manually?
3. **How many corporate access emails per week/month?** Volume affects ROI
4. **Historical event data:** How far back? Currently structured or scattered?
5. **Calendar system and multi-user permissions?**
6. **Should CA-04 and CA-05 be consolidated?** Significant overlap in analytics

#### Recommended Implementation Sequence

**Foundation + Observation:**
1. **Observe current CA workflow** (CA-05 focus) — Understand reporting needs, inform CA-01 data model
2. **CA-01: Event Identifier and Tracker** (Small) — Build structured event database
   - Use email forwarding (not complex inbox API)
   - Start simple: Outlook calendar as data store for MVP
   - Analyst matching via simple coverage lists

**After CA-01:**
3. **CA-02: Calendar Sync and Routing** (Small) — Add events to calendars
   - Keep simple: routing + conflict alerts (not intelligent conflict management)

4. **CA-05: Corporate Access Reporting** (Small-Medium) — Basic reporting after observing workflow
   - Leverage CA-01 structured data
   - Focus on automating existing manual reports

**Evaluate First:**
5. **CA-04: Broker Utilization Analyzer** (Medium) — Check CorpAxe capabilities first
   - If CorpAxe doesn't cover: build analytics layer
   - Consider consolidating with CA-05

**Question ROI:**
6. **CA-03: Corporate Access Forecaster** (Small-Medium) — Adjacent to core competency
   - If building: start very simple (recurring conference alerts only)
   - Research existing corporate access management platforms first
   - May not be worth building beyond basic alerts

#### Strategic Notes

**Limited AI Opportunities:**
- This section is mostly calendar management, data aggregation, and reporting
- True AI/LLM work limited to email parsing (CA-01)
- Consider if resources better spent on higher-AI-value projects

**CorpAxe Already Exists:**
- Finiato (CorpAxe) on vendor list for broker management
- Research existing capabilities before building CA-04/CA-05
- May already have reporting that covers these needs

**CA-01 Is Quick Win:**
- Small project with immediate value (automated event tracking)
- Enables rest of section
- Good candidate for early implementation

**Observe Before Building:**
- CA-05 workflow observation can inform entire CA section
- Understand what reports/analytics are actually valuable
- Identify non-AI automations that save time

---

### 2.8 Administrative & Cross-Functional — Shared Infrastructure

#### Critical Shared Dependencies

**1. Document Repository & RAG System (from IR section)**
- **Required for:** AD-02, AD-03
- **Components:** Vector database, semantic search, document indexing, classification
- **Cross-section dependency:** IR infrastructure #3
- **Impact:** AD-02 is essentially IR-03 with broader document scope, AD-03 feeds into document repository
- **AD-03 as starting point:** Egnyte integration provides tangible win while building broader document infrastructure

**2. Meeting Notes and Relationship Data**
- **Required for:** AD-01
- **Components:** Prior meeting notes, participant information, relationship history
- **Similar to InvRel-02:** AD-01 is general-purpose version of investor meeting prep
- **Impact:** Meeting prep depends on structured meeting history

**3. Calendar Integration (from IR/CA sections)**
- **Required for:** AD-01
- **Components:** Calendar API access, meeting detection, participant extraction
- **Cross-section dependency:** InvRel-01, InvRel-02, CA-01, CA-02 use similar calendar integration
- **Impact:** Shared infrastructure across multiple sections

**4. Comprehensive Data Warehouse**
- **Required for:** AD-04
- **Components:** All data sources across all sections (positions, performance, investor data, private investments, operations, etc.)
- **Impact:** AD-04 is aggregation of everything - requires foundational infrastructure from ALL sections
- **This is the most dependent project in entire analysis**

**5. Dashboard Infrastructure**
- **Required for:** AD-04
- **Components:** Dashboard framework, data visualization, web interface, query routing
- **Cross-section dependency:** InvRel-07 also needs dashboard
- **Build vs buy:** Retool, Sigma Computing, Looker, Tableau vs custom build
- **Impact:** Dashboard tooling decision affects multiple projects across sections

**6. Graph Database & Communication Access**
- **Required for:** AD-05
- **Components:** Neo4j or similar, email/calendar/CRM access, relationship strength algorithms
- **Impact:** Unique to AD-05, substantial infrastructure need
- **Privacy considerations:** Accessing communication patterns across firm

#### Cross-Section Dependencies

**AD-02 = IR-03 extension:**
- Same RAG infrastructure
- Broader document scope (all Egnyte, not just research)
- Should be feature of IR-03, not standalone

**AD-03 = Part of IR-03 infrastructure:**
- Document tagging/classification feeds into document repository
- First milestone of broader document repository project

**AD-01 similar to InvRel-02:**
- General meeting prep vs investor meeting prep
- Consider shared infrastructure

**AD-04 depends on EVERYTHING:**
- Requires data from IR, MI, PM, OF, LC, InvRel, CA sections
- Should be built LAST after foundational data infrastructure exists

#### Key Observations

**Many Projects Are Extensions of IR-03:**
- **AD-02:** Enterprise search is IR-03 for all documents
- **AD-03:** Document tagger is infrastructure feeding IR-03
- **Recommendation:** Don't build 3 separate systems, integrate into unified document repository

**AD-04 Is Massive in Scope:**
- Large to XL project aggregating all data sources
- Requires virtually every other foundational project to be complete first
- **Break into phases:** Basic dashboard → domain-specific chatbot → cross-functional synthesis
- Dashboard tooling decision (Retool vs custom) critically affects scope
- **Build LAST** in implementation sequence

**AD-05 Is Standalone and Speculative:**
- Large to XL project with unique infrastructure needs (graph database)
- Privacy and data access challenges significant
- Could be fun and unique value-add, but question ROI
- Good isolatable project for contractors if pursued
- **Build only if strong ROI case**

**Calendar Integration Shared:**
- AD-01 uses same calendar integration as InvRel-01, InvRel-02, CA-01, CA-02
- Opportunity for shared infrastructure across sections

**Dashboard Tooling Is Critical Decision:**
- Affects AD-04, InvRel-07, potentially OF-02
- Evaluate Retool, Sigma Computing, Looker, Tableau before committing to custom build
- Tool choice significantly impacts development time and maintenance

#### Critical Questions for All AD Projects

1. **Document scope for AD-02/AD-03:** What documents in Egnyte should be included?
2. **Dashboard tooling decision:** Custom build or leverage existing tools?
3. **AD-05 ROI:** Is relationship mapping valuable enough to justify Large/XL investment?
4. **Privacy policies:** What communication data can be accessed for AD-05?
5. **AD-04 phasing:** What's the MVP? (Focus on specific executive queries first)

#### Recommended Implementation Sequence

**Foundation (Part of IR-03 Document Repository):**
1. **AD-03: Document Tagger** (Small-Medium) — First milestone of document repository
   - Start with Egnyte uploads
   - Build classification and tagging infrastructure
   - Feeds into IR-03 RAG system

**After IR-03 RAG Infrastructure:**
2. **AD-02: Enterprise Search** (Medium) — Extend IR-03 to all documents
   - Not standalone, feature of IR-03
   - Broader document corpus beyond research

**After Meeting Data Infrastructure:**
3. **AD-01: Meeting Prep Automator** (Medium) — General meeting prep
   - Consider sharing infrastructure with InvRel-02
   - Requires structured meeting notes

**Much Later (After Most Other Projects):**
4. **AD-04: Executive Dashboard** (Large-XL) — Requires all foundational data infrastructure
   - Build in phases: basic dashboard → domain chatbot → cross-functional
   - Evaluate dashboard tooling options first
   - **Build LAST** when data infrastructure mature

**Question ROI First:**
5. **AD-05: Relationship Mapper** (Large-XL) — Speculative, unique value proposition
   - Assess ROI before committing
   - Data access and privacy challenges significant
   - Could be good contractor project if pursued

#### Strategic Notes

**This Section Is About Integration:**
- AD projects are cross-functional by nature
- Most are extensions or aggregations of other sections' infrastructure
- AD-02/AD-03 should be part of IR-03, not separate
- AD-04 aggregates everything

**AD-04 Is The Ultimate Dashboard:**
- Requires virtually all other infrastructure to be valuable
- Don't build early - wait until foundational data exists
- Consider if simpler domain-specific dashboards provide more value
- Dashboard tooling decision affects multiple projects

**AD-05 Is High-Risk, High-Reward:**
- Relationship mapping could be unique differentiator
- Large/XL scope with data access challenges
- Privacy considerations significant
- Only build if strong ROI case can be made

**Document Repository Is Central:**
- AD-02 and AD-03 both relate to document management
- Should be integrated with IR-03 document repository
- Don't duplicate infrastructure

**Calendar Integration Opportunities:**
- Multiple sections need calendar integration (AD-01, InvRel-01/02, CA-01/02)
- Build shared calendar framework once, reuse across sections

---

## 3. Master Building Block Analysis

### Tier 1: Foundational Infrastructure (Required by 5+ use cases)

#### 1. Document Repository & RAG System (IR-03 Core)
**Description:** Centralized document repository with semantic search, vector embeddings, and Q&A interface. Handles research documents, transcripts, legal documents, side letters, fund documents, and general enterprise documents.

**Required by:**
- IR-02, IR-03, IR-04, IR-07, IR-08, IR-10 (Investment Research)
- MI-07 (Market Intelligence)
- PM-05 (Private Markets)
- LC-03, LC-06 (Legal & Compliance)
- InvRel-06 (Investor Relations)
- AD-02, AD-03 (Administrative)

**Project Count:** 13 projects

**Why Foundational:**
- Enables semantic search and Q&A across all document types
- RAG infrastructure is reusable for multiple domains (research, legal, private markets)
- Single investment unlocks entire category of use cases
- Several "separate" projects (LC-03, InvRel-06, AD-02) should be features of this core system, not standalone builds

**Implementation Notes:**
- Start with research documents (IR-03)
- Expand to legal documents (LC-03/06, InvRel-06)
- Extend to all enterprise documents (AD-02)
- AD-03 (Document Tagger) feeds into this system

---

#### 2. Financial Data Warehouse
**Description:** Comprehensive financial data infrastructure including consensus estimates, historical financials, forward estimates, company fundamentals, trading multiples, and portfolio positions.

**Required by:**
- IR-01, IR-05, IR-06, IR-08, IR-09, IR-11, IR-12, IR-13 (Investment Research)
- PM-01 (Private Markets - for public comps)
- InvRel-03, InvRel-05 (Investor Relations - performance/attribution data)

**Project Count:** 10 projects

**Why Foundational:**
- Single most critical dependency for Investment Research section (8 of 13 projects)
- Enables financial analysis, comps generation, performance tracking
- Without this, 10 projects have dramatically increased scope
- Supports both public market analysis and private market comparisons

**Implementation Notes:**
- Build as standalone infrastructure project first
- Include consensus estimates, fundamentals, trading data
- Add performance/attribution layer for investor relations needs

---

#### 3. Investor Data Warehouse (InvRel-07)
**Description:** Unified investor data warehouse aggregating records from fund administration, CRM, meeting notes, DDQ responses, transaction history, and relationship data. Includes dashboard for investor-specific reporting.

**Required by:**
- InvRel-01, InvRel-02, InvRel-03, InvRel-04, InvRel-05 (Investor Relations)

**Project Count:** 5 projects

**Why Foundational:**
- InvRel-07 itself is a Large project that unlocks 5 other InvRel projects
- Data reconciliation and historical backfill are critical
- Without this, InvRel projects range Medium to Large. With it: Small to Medium
- Dashboard infrastructure benefits other sections (AD-04, potentially OF-02)

**Implementation Notes:**
- Build InvRel-07 first before other InvRel projects
- Evaluate dashboard tooling (Retool, Sigma) vs custom build
- Historical data backfill essential for usefulness
- Data reconciliation framework required

---

#### 4. Enfusion Data Infrastructure
**Description:** Regular API access to Enfusion, scheduled data pulls, structured storage, and data warehouse for portfolio management system data.

**Required by:**
- OF-07 (critical), OF-08, OF-10 (Operations & Finance)

**Project Count:** 3 projects directly, but unlocks entire OF section

**Why Foundational:**
- THE foundational dependency for Operations & Finance section
- Medium to Large standalone project
- Without this, many OF projects become significantly more complex
- Enables trade tracking, position tracking, cash reporting, reconciliation

**Implementation Notes:**
- Build as standalone infrastructure project first
- Assess API access, export formats, update frequency
- Critical for OF section to function

---

#### 5. Accounting System Integration
**Description:** API access to accounting systems (QuickBooks for management company, other systems for funds), journal entry posting, data extraction, budget access.

**Required by:**
- OF-02, OF-03, OF-04, OF-05, OF-06, OF-08, OF-09 (Operations & Finance)

**Project Count:** 7 projects

**Why Foundational:**
- 7 of 11 OF projects depend on accounting system access
- Enables spend analytics, fee calculations, month-end close, budget prep, capital flows reporting
- Critical for financial automation

**Implementation Notes:**
- Identify all accounting systems in use (QuickBooks for mgmt co, others for funds)
- Assess API access availability
- Start with read-only access before building posting capabilities
- Build as Medium complexity project

---

#### 6. Trading/Market Data Infrastructure
**Description:** Real-time and historical pricing data, trading multiples, portfolio positions, returns data from market data vendors.

**Required by:**
- IR-05, IR-06, IR-09, IR-11, IR-12, IR-13 (Investment Research)

**Project Count:** 6 projects

**Why Foundational:**
- 6 IR projects require reliable access to market data and trading information
- Enables comps generation, portfolio analysis, scenario modeling, performance tracking
- May already partially exist via existing Bloomberg/FactSet subscriptions

**Implementation Notes:**
- Assess existing market data subscriptions and access
- Build integration layer to structured data warehouse
- Include real-time and historical components

---

#### 7. Slack Integration Framework
**Description:** Reusable Slackbot framework with authentication, channel posting, interactive commands, file uploads, and alert mechanisms.

**Required by:**
- IR-01, IR-02, IR-03, IR-06 (Investment Research)
- MI projects (if alert delivery via Slack)
- OF-10 (Operations & Finance)

**Project Count:** 4+ projects explicitly, many more optionally

**Why Foundational:**
- 4 IR projects require Slack integration
- Many other sections can benefit from Slack delivery (MI alerts, OF reconciliation alerts)
- Building solid framework once reduces duplicate effort
- Relatively small investment, high reusability

**Implementation Notes:**
- Build as Small project early
- Create reusable components: authentication, posting, commands, file uploads
- Used by multiple sections, not just IR

---

### Tier 2: Functional Infrastructure (Required by 3-4 use cases)

#### 8. Fund Administration System Access
**Description:** API access to fund administration systems for NAV data, investor balances, transaction records, capital flows, side letter terms.

**Required by:**
- OF-09, OF-05, OF-06 (Operations & Finance - fee calculations, capital flows)
- InvRel-03, InvRel-04, InvRel-05, InvRel-07 (Investor Relations)

**Project Count:** 7 projects across two sections

**Implementation Notes:**
- Critical for fee calculations and investor relations
- Assess fund admin API access and capabilities
- May be part of InvRel-07 data aggregation effort

---

#### 9. Calendar Integration Framework
**Description:** Calendar API access (Outlook, Google), meeting detection, conflict detection, multi-user calendar management, participant extraction.

**Required by:**
- IR-01, IR-10 (Investment Research - earnings calendar)
- CA-01, CA-02 (Corporate Access)
- InvRel-01, InvRel-02 (Investor Relations)
- AD-01 (Administrative)

**Project Count:** 7 projects across four sections

**Implementation Notes:**
- Shared infrastructure opportunity across multiple sections
- Build once, reuse for multiple calendar-based projects
- Managing conflicts is complexity driver (keep simple initially)

---

#### 10. News & Research Feeds
**Description:** Integration with news and research APIs (Bloomberg, FactSet, AlphaSense), feed normalization, deduplication.

**Required by:**
- IR-04 (Investment Research - research digest)
- MI-01, MI-02, MI-03 (Market Intelligence)

**Project Count:** 4 projects

**Implementation Notes:**
- Foundation for all news-based monitoring
- Overlap with Document Repository (news articles as documents)
- Verify vendor API access before committing

---

#### 11. Corporate Document Archive
**Description:** Historical archive of deal documents, term sheets, investment agreements, CIMs, side letters, contracts, fund documents.

**Required by:**
- PM-01, PM-03 (Private Markets)
- LC-02, LC-03, LC-04, LC-05, LC-06 (Legal & Compliance)

**Project Count:** 7 projects across two sections

**Implementation Notes:**
- If doesn't exist, building this could be Large project itself
- Critical for precedent matching and comparison features
- Without structured archive, PM and LC projects add 4-6 weeks each
- Key question: Does structured archive exist or need to be built?

---

#### 12. Dashboard Infrastructure
**Description:** Dashboard framework, data visualization tools, web interface, reporting capabilities.

**Required by:**
- InvRel-07 (Investor Relations)
- AD-04 (Administrative - executive dashboard)
- Potentially OF-02 (Operations - spend analytics)

**Project Count:** 3 major projects, but affects entire firm

**Implementation Notes:**
- **CRITICAL BUILD VS BUY DECISION**
- Evaluate: Retool, Sigma Computing, Looker, Tableau vs custom build
- Decision significantly impacts development time and maintenance
- Consider data warehouse-native tools
- Build this as shared infrastructure, not per-project

---

### Tier 3: Specialized Tools (1-2 use cases)

#### 13. SEC Filing Access
**Description:** SEC filing feeds (Bloomberg/FactSet/Tegus), parsing logic for 10-K, 10-Q, 8-K, proxy statements.

**Required by:** MI-02, MI-04 (Market Intelligence)
**Project Count:** 2 projects
**Notes:** Medium complexity if vendor-provided, High if building EDGAR scraper

---

#### 14. Transcript Access Infrastructure
**Description:** Earnings call and expert call transcript APIs (Tegus/AlphaSense), parsing, storage.

**Required by:** IR-07, MI-07
**Project Count:** 2 projects
**Notes:** Part of Document Repository infrastructure

---

#### 15. Private Company Data (PitchBook/Preqin)
**Description:** Market deal terms, valuation benchmarks, historical private transactions.

**Required by:** PM-01, PM-03 (Private Markets)
**Project Count:** 2 projects
**Notes:** Enables market comparison features for private investments

---

#### 16. Egnyte Integration
**Description:** Folder monitoring, file upload triggers, document access API.

**Required by:** PM-01, PM-02, AD-03 (Private Markets + Administrative)
**Project Count:** 3 projects
**Notes:** Enables automated triggers when new documents arrive

---

#### 17. Alternative Data Integration
**Description:** Integration framework for alternative data vendors (Revealera for hiring, social sentiment, web traffic, etc.)

**Required by:** MI-06 (hiring data), MI-05 (social sentiment)
**Project Count:** 2 projects
**Notes:** Each new alt data source adds integration overhead

---

#### 18. Trade Data & Compliance Context
**Description:** Internal trade data, restricted list, calendar/meeting data for MNPI context, expert call records.

**Required by:** LC-01 (Legal & Compliance - trade surveillance)
**Project Count:** 1 project
**Notes:** Cross-references trades with compliance constraints and MNPI context

---

#### 19. Regulatory Intelligence Feed
**Description:** Regulatory updates, SEC/FINRA guidance, compliance deadlines.

**Required by:** LC-07 (Legal & Compliance)
**Project Count:** 1 project
**Notes:** **BUILD VS BUY** - Strong candidate for external subscription (RIA in a Box, MyComplianceOffice)

---

#### 20. Graph Database & Relationship Data
**Description:** Neo4j or similar graph database, relationship strength algorithms, communication pattern analysis.

**Required by:** AD-05 (Administrative - Relationship Mapper)
**Project Count:** 1 project
**Notes:** Unique infrastructure need, Large/XL scope, privacy considerations, speculative ROI

---

### Dependency Matrix

| Infrastructure Component | Required By (Project IDs) | Project Count | Priority |
|---|---|---|---|
| Document Repository & RAG System | IR-02, IR-03, IR-04, IR-07, IR-08, IR-10, MI-07, PM-05, LC-03, LC-06, InvRel-06, AD-02, AD-03 | 13 | **Tier 1** |
| Financial Data Warehouse | IR-01, IR-05, IR-06, IR-08, IR-09, IR-11, IR-12, IR-13, PM-01, InvRel-03, InvRel-05 | 11 | **Tier 1** |
| Accounting System Integration | OF-02, OF-03, OF-04, OF-05, OF-06, OF-08, OF-09 | 7 | **Tier 1** |
| Fund Administration System Access | OF-05, OF-06, OF-09, InvRel-03, InvRel-04, InvRel-05, InvRel-07 | 7 | **Tier 2** |
| Calendar Integration Framework | IR-01, IR-10, CA-01, CA-02, InvRel-01, InvRel-02, AD-01 | 7 | **Tier 2** |
| Corporate Document Archive | PM-01, PM-03, LC-02, LC-03, LC-04, LC-05, LC-06 | 7 | **Tier 2** |
| Trading/Market Data Infrastructure | IR-05, IR-06, IR-09, IR-11, IR-12, IR-13 | 6 | **Tier 1** |
| Slack Integration Framework | IR-01, IR-02, IR-03, IR-06, OF-10, plus MI alerts | 5+ | **Tier 1** |
| Investor Data Warehouse (InvRel-07) | InvRel-01, InvRel-02, InvRel-03, InvRel-04, InvRel-05 | 5 | **Tier 1** |
| News & Research Feeds | IR-04, MI-01, MI-02, MI-03 | 4 | **Tier 2** |
| Dashboard Infrastructure | InvRel-07, AD-04, OF-02 | 3 | **Tier 2** |
| Egnyte Integration | PM-01, PM-02, AD-03 | 3 | **Tier 3** |
| Enfusion Data Infrastructure | OF-07, OF-08, OF-10 | 3 | **Tier 1** |
| SEC Filing Access | MI-02, MI-04 | 2 | **Tier 3** |
| Transcript Access | IR-07, MI-07 | 2 | **Tier 3** |
| Private Company Data | PM-01, PM-03 | 2 | **Tier 3** |
| Alternative Data Integration | MI-05, MI-06 | 2 | **Tier 3** |
| Trade Data & Compliance Context | LC-01 | 1 | **Tier 3** |
| Regulatory Intelligence Feed | LC-07 | 1 | **Tier 3** |
| Graph Database | AD-05 | 1 | **Tier 3** |

---

## 4. Strategic Implementation Roadmap

### Phase 1 (Months 0-3): Foundation & Quick Wins

**Objective:** Build core Tier 1 infrastructure while delivering 2-3 small wins to validate approach and demonstrate value.

#### Tier 1 Infrastructure Projects
1. **Document Repository & RAG System (IR-03)** - Medium to Large
   - Vector database (Pinecone, Weaviate, or self-hosted)
   - Document ingestion pipeline
   - Semantic search and Q&A interface
   - Start with research documents
   - **This enables 13 projects across all sections**

2. **Slack Integration Framework** - Small
   - Reusable Slackbot components
   - Authentication, posting, commands, file uploads
   - **Quick to build, high reusability**

3. **Financial Data Warehouse (Phase 1)** - Medium
   - Consensus estimates and fundamentals
   - Historical financials
   - Integration with existing FactSet/Bloomberg access
   - **Enables 11 IR and InvRel projects**

#### Quick Win Projects (Validate Infrastructure)
4. **IR-07: Expert Call Insight Extractor** - Small
   - Tests document processing pipeline
   - Straightforward extraction use case
   - Immediate value for analysts
   - **2 weeks, validates IR-03 infrastructure**

5. **IR-04: Automated Research Digest** - Small to Medium
   - Tests news feed integration and document repository
   - Daily/weekly digest of relevant research
   - High visibility, immediate value
   - **2-4 weeks**

6. **IR-01: Earnings Preview Generator** - Medium
   - Tests financial data + Slack + internal notes integration
   - Automated briefing before earnings calls
   - **4-6 weeks after financial data warehouse**

**Phase 1 Deliverables:**
- Core IR-03 RAG infrastructure operational
- Slack integration framework reusable
- Financial data warehouse (basic version)
- 3 small projects delivering immediate value
- Validated approach for document processing and LLM applications

---

### Phase 2 (Months 3-6): Expand Infrastructure & Pilot Projects

**Objective:** Complete remaining Tier 1 infrastructure, pilot medium-complexity projects, begin build vs. buy evaluations.

#### Tier 1 Infrastructure Projects (Continued)
1. **Enfusion Data Infrastructure** - Medium to Large
   - API access to Enfusion
   - Scheduled data pulls
   - Data warehouse for portfolio data
   - **Unlocks entire OF section**

2. **Accounting System Integration** - Medium
   - QuickBooks integration for management company
   - Other accounting systems for funds
   - Read-only access initially
   - **Enables 7 OF projects**

3. **Investor Data Warehouse (InvRel-07)** - Large
   - Data aggregation from fund admin, CRM, meeting notes
   - Historical backfill
   - Dashboard (evaluate Retool/Sigma vs custom)
   - **Unlocks 5 InvRel projects**

#### Tier 2 Infrastructure
4. **Calendar Integration Framework** - Small to Medium
   - Outlook/Google Calendar API access
   - Meeting detection and participant extraction
   - **Enables 7 projects across IR, CA, InvRel, AD**

5. **Fund Administration System Access** - Medium
   - API integration with fund admin
   - NAV data, investor balances, transactions
   - **Required for OF and InvRel projects**

#### Medium Complexity Pilot Projects
6. **CA-01: Event Identifier and Tracker** - Small
   - Email parsing for corporate access events
   - Structured event database
   - Tests email integration and event tracking
   - **Unlocks entire CA section**

7. **OF-08: Cash Position Summary** - Small
   - Tests Enfusion data infrastructure
   - Straightforward aggregation use case
   - **2 weeks after Enfusion infrastructure**

8. **MI-04: SEC Filing Monitor** - Small to Medium
   - Tests SEC filing access and alerting
   - Monitors portfolio company filings
   - **Likely vendor feeds exist**

9. **InvRel-01: LP Communication Drafter** - Small
   - Tests InvRel-07 data warehouse
   - MCP tool approach (simple workflow)
   - **After InvRel-07 complete**

#### Build vs. Buy Evaluations
- **Harvey evaluation** for legal document processing (LC-02, LC-03, LC-04, LC-06)
- **Compliance AI tools** (Behavox, Smarsh) for LC-01
- **Regulatory intelligence services** for LC-07
- **Dashboard tooling** (Retool, Sigma, Looker) for InvRel-07 and AD-04
- **Corporate access platforms** for CA-03 forecasting
- **Expense management platforms** (Brex, Airbase) for OF-01

**Phase 2 Deliverables:**
- All Tier 1 infrastructure complete
- Key Tier 2 infrastructure operational
- 4 additional small/medium projects delivering value
- Build vs. buy decisions documented for Legal, Compliance, Operations
- Calendar and fund admin integrations reusable across sections

---

### Phase 3 (Months 6-12): Expanding Capabilities & Section Buildouts

**Objective:** Build on mature infrastructure to deliver medium/large projects across sections. Focus on high-ROI projects with infrastructure dependencies now satisfied.

#### Investment Research Buildout
1. **IR-05: Company Comps Generator** - Medium
   - Requires financial + trading data (now available)
   - Automated comparable company analysis
   - **4-6 weeks**

2. **IR-08: Investment Memo First Draft** - Large
   - Requires mature document repository
   - Generates first draft from research notes
   - **8-12 weeks**

3. **IR-03 Expansion: Research Document Q&A Bot** - Medium
   - Full Q&A interface on top of document repository
   - Slackbot or web interface
   - **Already have infrastructure, add interface**

#### Market Intelligence Projects
4. **MI-01: Portfolio Company News Monitor** - Medium
   - Foundation for other news projects
   - Uses news feeds + document repository
   - **4-6 weeks**

5. **MI-07: Management Commentary Tracker** - Medium to Large
   - Similar to IR-07 but broader scope
   - Transcript analysis across earnings calls
   - **6-10 weeks**

#### Operations & Finance Projects
6. **OF-05: Management Fee Calculator** - Small to Medium
   - Traditional script, not AI
   - Uses fund admin data
   - **2-4 weeks**

7. **OF-06: Incentive Fee Calculator** - Medium
   - Builds on OF-05 patterns
   - More complex calculation logic
   - **4-6 weeks**

8. **OF-09: Capital Flows Report** - Small to Medium
   - Uses fund admin API
   - Automated investor capital activity report
   - **2-4 weeks**

9. **OF-02: Spend Analytics** - Medium
   - Uses accounting system integration
   - Basic analytics first, consolidation later
   - **4-6 weeks**

#### Investor Relations Projects
10. **InvRel-04: DDQ Response** - Medium
    - After InvRel-07 data warehouse complete
    - Response versioning and matching system
    - **6-8 weeks**

11. **InvRel-05: Quarterly Cheat Sheet** - Medium
    - Requires performance/attribution data
    - Visual fund summary for LPs
    - **4-6 weeks**

12. **InvRel-02: Meeting Prep Generator** - Medium
    - Uses InvRel-07 data and calendar integration
    - Investor meeting briefing documents
    - **4-6 weeks**

#### Private Markets Projects
13. **PM-04: Update Processor** - Medium
    - Builds data standardization pipeline
    - Portfolio company update extraction
    - **Enables PM-05**

14. **PM-01: CIM Analyzer** - Medium to Large
    - Start without market comparisons (Medium)
    - CIM parsing and summarization
    - **6-10 weeks**

#### Corporate Access Projects
15. **CA-02: Calendar Sync and Routing** - Small
    - After CA-01 complete
    - Automated calendar management
    - **2 weeks**

16. **CA-05: Corporate Access Reporting** - Small to Medium
    - Uses CA-01 structured event data
    - Automate existing manual reports
    - **2-4 weeks**

#### Administrative Projects
17. **AD-03: Document Tagger** - Small to Medium
    - First milestone of broader document repository
    - Egnyte integration
    - **Feeds into IR-03**

18. **AD-01: Meeting Prep Automator** - Medium
    - General meeting prep (not just investors)
    - Similar to InvRel-02 infrastructure
    - **4-6 weeks**

**Phase 3 Deliverables:**
- 18 additional projects across all sections
- Strong presence across IR, MI, OF, InvRel sections
- Begin PM and AD buildouts
- Tier 2 infrastructure mature and reusable
- Majority of small/medium projects complete

---

### Phase 4 (Year 2+): Advanced Features & Strategic Projects

**Objective:** Tackle large/XL strategic projects, complete remaining section buildouts, cross-functional integration.

#### Large Strategic Projects

1. **InvRel-03: Investor Letter First Draft** - Medium to Large
   - Comprehensive performance data required
   - Quarterly letter generation
   - **8-12 weeks**

2. **MI-03: Industry News Synthesizer** - Large
   - Hub project building on MI-01
   - Cross-company industry analysis
   - **8-12 weeks**

3. **MI-02: Competitor Intelligence Tracker** - Large
   - Aggregates MI-01, MI-04, MI-06
   - Comprehensive competitor monitoring
   - **8-12 weeks**

4. **PM-02: Data Room Processor** - Large
   - Complex due to document volume/variety
   - Due diligence automation
   - **Consider build vs. buy first**

5. **AD-02: Enterprise Search (IR-03 Extension)** - Medium
   - Extend IR-03 to all enterprise documents
   - Unified search across all document types
   - **Feature of IR-03, not standalone**

6. **IR-12: Portfolio Performance Dashboard** - Medium to Large
   - Comprehensive performance tracking
   - Attribution analysis
   - **8-12 weeks**

7. **OF-03: Month-End Close Automation** - TBD
   - Observe workflow first
   - Build targeted tools for specific pain points
   - **Highly dependent on existing process**

8. **OF-04: Budget Prep Automation** - Medium to Large
   - Depends on OF-03 infrastructure
   - Budget templates and forecasting
   - **6-10 weeks**

#### Cross-Functional Integration

9. **AD-04: Executive Dashboard / Knowledge Bot** - Large to XL
   - **Build LAST after all data infrastructure mature**
   - Aggregates data from all sections
   - Break into phases:
     - Phase 1: Basic dashboard with key metrics (Medium-Large)
     - Phase 2: Domain-specific chatbot (Medium)
     - Phase 3: Cross-functional synthesis (Large)
   - **Evaluate dashboard tooling critical**
   - **12-20+ weeks across phases**

#### Legal & Compliance (Build vs. Buy Driven)

10. **LC-03/InvRel-06: Side Letter Query Bot** - Medium
    - **Consolidate duplicate projects**
    - Add side letters to IR-03 infrastructure
    - **If not using Harvey: 6-8 weeks**

11. **LC-05: Marketing Footnotes Assistant** - Small to Medium
    - Start with performance claims only
    - Requires non-engineering prep work
    - **3-6 weeks**

12. **LC-01: Trade Surveillance (narrow scope)** - Small
    - Restricted list check only
    - **If not using compliance AI platform**

#### Speculative / Optional Projects

13. **PM-03: Deal Terms Extraction** - Medium to Large
    - **Strong build vs. buy candidate (Harvey)**
    - High hallucination risk
    - Only if not covered by purchased platform
    - **8-12 weeks if building**

14. **PM-05: Private Markets Q&A Bot** - Medium
    - After PM-04 data standardization
    - Consider as feature of IR-03
    - **4-6 weeks**

15. **AD-05: Relationship Mapper** - Large to XL
    - **Question ROI first**
    - Graph database, communication access
    - Privacy considerations
    - **Good contractor project if pursued**
    - **12-20 weeks**

16. **OF-10: Reconciliation Monitor** - Medium
    - After trade tracking infrastructure
    - Automated trade reconciliation alerts
    - **6-8 weeks**

17. **OF-11: Statement Reconciliation** - Medium
    - LLM extraction from well-structured PDFs (6-7 counterparty formats)
    - Two-stage approach: LLM extraction → DataFrame comparison
    - **Consider specialized reconciliation tools first**
    - **6-10 weeks if building**

#### Avoid Building (Partner/License Instead)

18. **IR-11: Portfolio Scenario Analyzer** - XL+
    - Partner/license instead of build
    - Beyond scope of in-house development

19. **IR-13: Trading Strategy Back-tester** - XL+
    - Partner/license instead of build
    - Specialized domain requiring significant infrastructure

20. **MI-05: Social Sentiment Tracker** - XL+
    - **CRITICAL BUILD VS BUY DECISION**
    - Don't build from scratch
    - Evaluate sentiment data vendors

**Phase 4 Deliverables:**
- All high-value large projects complete
- Executive dashboard operational (AD-04)
- Cross-functional data integration mature
- Final section buildouts complete (PM, LC, remaining OF)
- Strategic build vs. buy decisions finalized
- 50+ of 60 use cases addressed (10 may be vendor/partner solutions)

---

## 5. Quick Wins Analysis

Quick wins are Small-sized projects (2-4 weeks) that can deliver immediate value while validating infrastructure. Grouped by infrastructure dependency:

### Group A: Document Repository Dependent (After IR-03 Infrastructure)

**IR-07: Expert Call Insight Extractor** - Small (2 weeks)
- **Infrastructure needed:** Document Repository & RAG System
- **Why quick win:** Straightforward extraction use case, tests document processing
- **Immediate value:** Analysts get summarized insights from expert calls

**IR-04: Automated Research Digest** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** Document Repository, News Feeds
- **Why quick win:** Aggregates existing content, high visibility
- **Immediate value:** Daily/weekly digest of relevant research

**AD-03: Document Tagger** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** Egnyte API (simpler than full IR-03)
- **Why quick win:** Can be first milestone of document repository, tangible organization benefit
- **Immediate value:** Automated document classification and organization

### Group B: Calendar/Event Dependent (Minimal Infrastructure)

**CA-01: Event Identifier and Tracker** - Small (2 weeks)
- **Infrastructure needed:** Email forwarding, calendar API (lightweight)
- **Why quick win:** Email parsing straightforward, can use calendar as storage
- **Immediate value:** Automated corporate access event tracking
- **Unlocks:** Entire CA section (CA-02, CA-03, CA-04, CA-05)

**CA-02: Calendar Sync and Routing** - Small (2 weeks)
- **Infrastructure needed:** CA-01 + calendar API
- **Why quick win:** Adding events to calendar straightforward
- **Immediate value:** Automated analyst calendar management

### Group C: Vendor Data Dependent (If APIs Exist)

**MI-04: SEC Filing Monitor** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** SEC filing feeds (likely from Bloomberg/FactSet)
- **Why quick win:** Vendor feeds likely exist, straightforward alerting
- **Immediate value:** Automated notifications for portfolio company filings
- **Dependency:** Verify vendor API access first

**MI-06: Hiring Pattern Intelligence** - Small (2 weeks)
- **Infrastructure needed:** Revealera integration (on vendor list)
- **Why quick win:** If Revealera access exists, straightforward extraction
- **Immediate value:** Early signals of company growth/contraction
- **Dependency:** Confirm Revealera on approved vendor list and accessible

### Group D: After Enfusion Infrastructure

**OF-08: Cash Position Summary** - Small (2 weeks)
- **Infrastructure needed:** Enfusion Data Infrastructure
- **Why quick win:** Straightforward aggregation, tests Enfusion integration
- **Immediate value:** Daily cash position visibility

**OF-07: Tax Lot Processor** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** Enfusion Data Infrastructure
- **Why quick win:** After Enfusion infrastructure, tax lot extraction straightforward
- **Immediate value:** Automated tax lot tracking for year-end

### Group E: After Financial Data Warehouse

**IR-01: Earnings Preview Generator** - Medium (4-6 weeks)
- **Infrastructure needed:** Financial Data Warehouse, Slack Integration, Internal Notes
- **Why relatively quick:** Tests multiple infrastructure components together
- **Immediate value:** Automated earnings prep for analysts
- **Note:** Slightly larger than others, but high value pilot

### Group F: After Investor Data Warehouse (InvRel-07)

**InvRel-01: LP Communication Drafter** - Small (2 weeks)
- **Infrastructure needed:** InvRel-07 data warehouse
- **Why quick win:** MCP tool approach (simple workflow), straightforward drafting
- **Immediate value:** Faster LP communication with relationship context

**OF-09: Capital Flows Report** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** Fund Admin API
- **Why quick win:** Straightforward reporting if API accessible
- **Immediate value:** Automated investor capital activity tracking

### Group G: Independent / Workflow Observation Required

**LC-01: Trade Surveillance (narrow scope)** - Small (2-3 weeks)
- **Infrastructure needed:** Restricted list, basic trade data
- **Why quick win:** Narrow scope (restricted list check only)
- **Immediate value:** Automated pre-trade compliance check
- **Note:** Evaluate compliance AI tools first (build vs. buy)

**LC-05: Marketing Footnotes Assistant** - Small to Medium (3-6 weeks)
- **Infrastructure needed:** Historical marketing materials corpus
- **Why quick win:** Start with performance claims only (80% of use case)
- **Immediate value:** Automated compliance footnotes for marketing
- **Note:** Requires non-engineering prep work (compiling approved language)

**CA-05: Corporate Access Reporting** - Small to Medium (2-4 weeks)
- **Infrastructure needed:** CA-01 structured event data
- **Why quick win:** Automates existing manual reports
- **Immediate value:** Time savings on monthly/quarterly reporting
- **Note:** Observe workflow first to ensure reports are valuable

### Quick Win Implementation Sequence

**Month 1-2 (Immediate):**
1. CA-01: Event Tracker (Small - 2 weeks) - Minimal dependencies
2. CA-02: Calendar Routing (Small - 2 weeks) - After CA-01

**Month 2-3 (After IR-03 Initial Build):**
3. IR-07: Expert Call Insights (Small - 2 weeks) - Validates document processing
4. IR-04: Research Digest (Small-Medium - 3 weeks) - High visibility value

**Month 3-4 (After Financial Data Warehouse):**
5. IR-01: Earnings Preview (Medium - 6 weeks) - Validates financial data + Slack

**Month 4-5 (After Enfusion Infrastructure):**
6. OF-08: Cash Position (Small - 2 weeks) - Validates Enfusion integration
7. OF-07: Tax Lot Processor (Small-Medium - 3 weeks)

**Month 5-6 (If Vendor APIs Exist):**
8. MI-04: SEC Filing Monitor (Small-Medium - 3 weeks) - Verify vendor access
9. MI-06: Hiring Intelligence (Small - 2 weeks) - If Revealera accessible

**Month 6+ (After InvRel-07):**
10. InvRel-01: LP Communication (Small - 2 weeks) - After data warehouse
11. OF-09: Capital Flows (Small-Medium - 3 weeks) - If fund admin API exists

**Total Quick Wins:** 11 projects, 30-40 weeks of development time spread across 6+ months
**Total Infrastructure Validated:** Document Repository, Calendar Integration, Financial Data, Enfusion, Vendor APIs, Investor Data Warehouse

---

## 6. Build vs. Buy Recommendations

### High Confidence "Buy" Recommendations

#### Legal & Compliance Section

**LC-02: Contract Review (Harvey)**
- **Vendor:** Harvey AI
- **Why Buy:** Harvey already being evaluated by team for contract review
- **Projects Covered:** LC-02 (Contract Review), potentially LC-04 (NDA Processing)
- **Rationale:** Legal document analysis is specialized domain with high hallucination risk. Harvey designed specifically for legal work with appropriate safeguards.
- **Recommendation:** **Strong buy** - Proceed with Harvey evaluation for LC-02 and LC-04

**LC-03/LC-06: Side Letter & Legal Document Q&A (Harvey)**
- **Vendor:** Harvey AI
- **Why Buy:** Harvey may already provide unified legal document search
- **Projects Covered:** LC-03 (Side Letter Repository), LC-06 (Fund Document Query)
- **Rationale:** If Harvey evaluation proceeds, assess whether legal document Q&A is included functionality
- **Recommendation:** **Buy if Harvey includes this** - Otherwise, integrate into IR-03 RAG infrastructure (build)

**LC-01: Trade Surveillance (Compliance AI Platforms)**
- **Vendors:** Behavox, Smarsh, ComplyAdvantage, existing Charles River/Bloomberg capabilities
- **Why Buy:** Compliance-specific AI tools likely better than custom build
- **Projects Covered:** LC-01 (Anomaly Detection for Trade Surveillance)
- **Rationale:** Compliance surveillance is specialized domain with regulatory requirements. Mature vendor solutions exist.
- **Recommendation:** **Evaluate compliance AI tools** before building. If narrowly scoped (restricted list check only), could build in-house as Small project.

**LC-07: Regulatory Policy Monitoring (Regulatory Intelligence Services)**
- **Vendors:** RIA in a Box, MyComplianceOffice, other regulatory intelligence services
- **Why Buy:** Regulatory intelligence feeds already exist as subscription services
- **Projects Covered:** LC-07 (Regulatory Policy Update Monitor)
- **Rationale:** Regulatory monitoring requires subject matter expertise and continuous updates. Not core competency.
- **Recommendation:** **Strong buy** - Subscribe to regulatory intelligence service rather than building

---

#### Operations & Finance Section

**OF-01: Expense Report Automation (Modern Expense Platforms)**
- **Vendors:** Brex, Airbase, Expensify, Ramp
- **Why Buy:** Modern expense management platforms likely solve this better than custom build
- **Projects Covered:** OF-01 (Expense Report Processor & Validator)
- **Rationale:** Expense management is mature SaaS category with OCR, approval workflows, accounting integration
- **Recommendation:** **Evaluate modern expense platforms** - Likely better ROI than building. Only build if gap is clearly identified and narrow.

**OF-03: Month-End Close Automation (Accounting Software Features)**
- **Vendors:** Existing accounting software features, specialized close management tools
- **Why Buy:** Existing accounting software may have better automation features
- **Projects Covered:** OF-03 (Month-End Close Workflow Assistant)
- **Rationale:** Month-end close is workflow-heavy and specific to accounting systems in use
- **Recommendation:** **Observe workflow first**, then evaluate accounting software capabilities before committing to build

**OF-04: Budget Prep Automation (Budgeting Software)**
- **Vendors:** Adaptive Insights (Workday), Anaplan, Planful, or accounting software budgeting modules
- **Why Buy:** Budgeting software may be better investment than custom build
- **Projects Covered:** OF-04 (Budget Preparation Assistant)
- **Rationale:** Budgeting involves collaboration, templates, approval workflows - mature category
- **Recommendation:** **Evaluate budgeting software** before building. Depends heavily on OF-03 workflow observations.

**OF-11: Statement Reconciliation (Specialized Reconciliation Tools)**
- **Vendors:** BlackLine, Trintech, ReconArt, or bank reconciliation software
- **Why Buy:** Specialized reconciliation tools may already solve this
- **Projects Covered:** OF-11 (Bank Statement Reconciliation)
- **Rationale:** Medium complexity - LLM extraction from limited set of well-structured PDFs (6-7 counterparty formats) with DataFrame comparison. No OCR needed. Mature reconciliation tools exist that may be more robust.
- **Recommendation:** **Evaluate reconciliation software first** - Only build if very specific gap identified or counterparty formats require custom extraction

---

#### Market Intelligence Section

**MI-05: Social Sentiment Tracker (Sentiment Data Vendors)**
- **Vendors:** Sentifi, Amenity Analytics, RavenPack, StockTwits, social sentiment platforms
- **Why Buy:** **CRITICAL BUILD VS BUY DECISION** - Don't build from scratch
- **Projects Covered:** MI-05 (Social Sentiment & Narrative Tracker)
- **Rationale:** XL+ complexity if building from scratch. Social platform APIs, sentiment analysis, narrative detection all complex. Mature vendor solutions exist.
- **Recommendation:** **Strong buy** - Evaluate sentiment data vendors. Building from scratch is XL+ scope and beyond core competency.

---

#### Private Markets Section

**PM-03: Deal Terms Extraction (Harvey or Legal AI Platforms)**
- **Vendors:** Harvey AI, or specialized contract intelligence platforms
- **Why Buy:** High hallucination risk with serious consequences, specialized legal domain
- **Projects Covered:** PM-03 (Deal Terms & Covenant Extractor)
- **Rationale:** Extracting legal terms from investment documents has high accuracy requirements. Errors could impact investment decisions. Legal AI platforms designed for this.
- **Recommendation:** **Strong buy candidate** - Evaluate Harvey or specialized platforms. Consider narrow scope pilot before committing to full build.

**PM-02: Data Room Processor (Due Diligence Platforms)**
- **Vendors:** Existing due diligence platforms, document intelligence tools
- **Why Buy:** Consider if existing due diligence platforms offer better solutions
- **Projects Covered:** PM-02 (Data Room Summarizer & Flagging System)
- **Rationale:** Large complexity due to document volume and variety. May overlap with existing DD platforms.
- **Recommendation:** **Evaluate before building** - Research existing due diligence platforms and document intelligence tools first

---

#### Corporate Access Section

**CA-03: Corporate Access Forecasting (Corporate Access Management Platforms)**
- **Vendors:** Existing corporate access management platforms
- **Why Buy:** Corporate access management platforms may already offer forecasting
- **Projects Covered:** CA-03 (Corporate Access Forecaster)
- **Rationale:** Forecasting/predictive analytics adjacent to core competency. Check if CorpAxe (Finiato, already in use) or other platforms cover this.
- **Recommendation:** **Evaluate existing platforms first** - If building, start very simple (recurring conference alerts only)

**CA-04/CA-05: Broker Analytics (CorpAxe/Finiato Existing Features)**
- **Vendor:** CorpAxe (Finiato) - already on vendor list for broker management
- **Why Buy:** CorpAxe may already cover broker utilization and reporting
- **Projects Covered:** CA-04 (Broker Utilization Analyzer), CA-05 (Corporate Access Reporting)
- **Rationale:** Broker management platform already in use. Research existing capabilities before building analytics layer.
- **Recommendation:** **Evaluate CorpAxe first** - Understand existing reporting features before committing to build

---

#### Investment Research Section

**IR-11: Portfolio Scenario Analyzer (Partner/License)**
- **Vendors:** Existing portfolio management/risk platforms
- **Why Buy:** Beyond scope of in-house development
- **Projects Covered:** IR-11 (Portfolio Scenario & Sensitivity Analyzer)
- **Rationale:** XL+ complexity, requires comprehensive risk modeling infrastructure, not core competency
- **Recommendation:** **Partner/license** - Don't build in-house

**IR-13: Trading Strategy Back-tester (Partner/License)**
- **Vendors:** Existing backtesting platforms
- **Why Buy:** Specialized domain requiring significant infrastructure
- **Projects Covered:** IR-13 (Trading Strategy Back-tester)
- **Rationale:** XL+ complexity, specialized domain, significant infrastructure requirements
- **Recommendation:** **Partner/license** - Don't build in-house

---

#### Administrative Section

**AD-04: Executive Dashboard (Dashboard Tooling Platforms)**
- **Vendors:** Retool, Sigma Computing, Looker, Tableau, or data warehouse-native tools
- **Why Buy:** Dashboard frameworks significantly reduce development time
- **Projects Covered:** AD-04 (Executive Dashboard / Knowledge Bot), InvRel-07 dashboard component
- **Rationale:** Building custom dashboard framework is Large project itself. Mature tools exist with connectors, visualization libraries, deployment infrastructure.
- **Recommendation:** **Strong buy** - Evaluate Retool, Sigma, or data warehouse-native tools. Building custom dashboard framework only if very specific requirements not met by existing tools.
- **Impact:** Affects multiple projects across sections (AD-04, InvRel-07, potentially OF-02)

---

### Hybrid Approach: Buy Platform + Build Integration

Several projects benefit from buying platforms but building integration tools (MCP tools, data feeds, custom connectors):

**Legal & Compliance:**
- Buy Harvey for contract review
- Build MCP tools to connect internal data (trade data, meeting data, restricted lists) to Harvey workflows
- Build connectors to feed internal documents to Harvey for analysis

**Operations & Finance:**
- Buy modern expense platform (Brex/Airbase)
- Build integrations to accounting system for automated posting
- Build approval workflow customizations specific to firm

**Market Intelligence:**
- Buy sentiment data vendor feeds
- Build aggregation layer to combine with portfolio holdings
- Build alerting system specific to portfolio companies

**Dashboard Infrastructure:**
- Buy dashboard platform (Retool/Sigma)
- Build custom connectors to internal data sources
- Build domain-specific views and queries

---

### Summary Table: Build vs. Buy Recommendations

| Project ID | Project Name | Recommendation | Vendor/Tool | Confidence | Impact |
|---|---|---|---|---|---|
| LC-02 | Contract Review | **Buy** | Harvey AI | High | Strong |
| LC-04 | NDA Processing | **Buy** | Harvey AI | High | Medium |
| LC-03, LC-06 | Legal Doc Q&A | **Buy if included** | Harvey AI | Medium | Medium |
| LC-01 | Trade Surveillance | **Evaluate/Buy** | Behavox, Smarsh, ComplyAdvantage | Medium | Strong |
| LC-07 | Policy Monitoring | **Buy** | RIA in a Box, MyComplianceOffice | High | Strong |
| OF-01 | Expense Reports | **Evaluate/Buy** | Brex, Airbase, Expensify | High | Medium |
| OF-03 | Month-End Close | **Evaluate First** | Accounting software features | Medium | TBD |
| OF-04 | Budget Prep | **Evaluate/Buy** | Adaptive Insights, Anaplan | Medium | Medium |
| OF-11 | Reconciliation | **Evaluate/Buy** | BlackLine, Trintech | High | Medium |
| MI-05 | Social Sentiment | **Buy** | Sentifi, Amenity Analytics, RavenPack | High | Strong |
| PM-03 | Deal Terms | **Buy** | Harvey AI, contract intelligence | High | Strong |
| PM-02 | Data Room | **Evaluate First** | DD platforms | Medium | Medium |
| CA-03 | CA Forecasting | **Evaluate/Buy** | Corporate access platforms | Medium | Low |
| CA-04, CA-05 | Broker Analytics | **Evaluate CorpAxe** | CorpAxe (Finiato) | High | Medium |
| IR-11 | Scenario Analyzer | **Partner** | Risk platforms | High | N/A |
| IR-13 | Back-tester | **Partner** | Backtesting platforms | High | N/A |
| AD-04, InvRel-07 | Dashboards | **Buy tooling** | Retool, Sigma, Looker | High | Strong |

**Build vs. Buy Decision Impact:**
- **High confidence "Buy":** 9 projects (LC-02, LC-07, OF-01, MI-05, PM-03, IR-11, IR-13, dashboard tooling)
- **Evaluate before deciding:** 8 projects (LC-01, LC-03/06, OF-03, OF-04, OF-11, PM-02, CA-03, CA-04/05)
- **Total projects potentially bought:** 15-20 of 60 use cases
- **Remaining to build:** 40-45 projects

**Strategic Implications:**
- Focus in-house development on core competencies (document processing, RAG, financial analysis)
- Buy specialized domains (legal, compliance, sentiment analysis, reconciliation)
- Hybrid approach for platforms: buy tools, build integrations
- Significant cost savings by leveraging existing solutions vs. building everything

---

## 7. Project Overlap & Consolidation Opportunities

### Critical Overlaps (Must Consolidate)

#### 1. InvRel-06 = LC-03 (Side Letter Query Bot)
**Project IDs:** InvRel-06, LC-03
**Overlap Description:**
- InvRel-06: "Side Letter Query Bot" - Query side letter repository for investor-specific terms
- LC-03: "Side Letter Term Repository" - Searchable database of side letter provisions with Q&A

**Analysis:** These are the SAME project described in two sections. Both provide semantic search and Q&A over side letter corpus.

**Consolidation Recommendation:**
- **Single project:** "Side Letter Query Bot" (classify as InvRel-06 or LC-03, not both)
- **T-shirt size:** Medium (if RAG infrastructure exists), Large (if building from scratch)
- **Infrastructure:** Part of Document Repository & RAG System (IR-03)
- **Approach:** Add side letters to IR-03 document corpus as new document type
- **Users:** Both investor relations team and legal/compliance team use same system
- **Alternative:** If Harvey is purchased, this may already be included in Harvey's legal document search

**Impact:** Eliminates duplicate project, saves Medium to Large project effort (6-12 weeks)

---

#### 2. AD-02 = IR-03 Extension (Enterprise Search)
**Project IDs:** AD-02, IR-03
**Overlap Description:**
- AD-02: "Enterprise Search and Retrieval Bot" - Natural language search across all Egnyte documents
- IR-03: "Research Document Q&A Bot" - Semantic search and Q&A over research documents

**Analysis:** AD-02 is IR-03 with broader document scope. Same RAG infrastructure, same semantic search capability, just expanded corpus.

**Consolidation Recommendation:**
- **Not separate project:** AD-02 is a milestone/expansion of IR-03
- **Approach:**
  1. Build IR-03 with research documents first
  2. Phase 2: Expand to legal documents (LC-03, InvRel-06)
  3. Phase 3: Expand to all enterprise documents (AD-02)
- **Single infrastructure:** Don't build separate RAG systems for research vs. all documents
- **T-shirt size:** IR-03 is Large project including all document types. AD-02 "expansion" is Small-Medium (2-4 weeks to add document types)

**Impact:** Avoids building duplicate RAG infrastructure, saves Medium to Large project effort (6-12 weeks). IR-03 becomes comprehensive document repository vs. narrow research-only system.

---

#### 3. AD-03 = Part of IR-03 Infrastructure (Document Tagger)
**Project IDs:** AD-03, IR-03
**Overlap Description:**
- AD-03: "Document Tagger and Organizer" - Classifies documents, suggests folders, applies metadata
- IR-03: "Research Document Q&A Bot" - Requires document ingestion, classification, metadata

**Analysis:** AD-03 is the document ingestion and classification pipeline that feeds IR-03. Not a separate user-facing project, but infrastructure component.

**Consolidation Recommendation:**
- **AD-03 is first milestone of IR-03:** Build document processing pipeline first, then add Q&A layer
- **Approach:**
  1. Phase 1 (AD-03): Egnyte integration, document classification, tagging, metadata
  2. Phase 2: Add vector embeddings and semantic search
  3. Phase 3: Add Q&A interface (Slack or web)
- **Tangible win:** AD-03 provides immediate value (organized Egnyte) while building toward full IR-03
- **T-shirt size:** AD-03 as standalone is Small-Medium (2-4 weeks). As part of IR-03, it's the first 2-4 weeks of the Large project.

**Impact:** Reframes AD-03 as starting point for IR-03, not separate project. Provides early value while building toward full RAG system. Clarifies dependency relationship.

---

### Significant Overlaps (Consider Consolidation)

#### 4. InvRel-02 vs. AD-01 (Meeting Prep Variations)
**Project IDs:** InvRel-02, AD-01
**Overlap Description:**
- InvRel-02: "Investor Meeting Prep Generator" - Specialized for LP meetings, includes relationship history, portfolio allocation, prior meeting notes
- AD-01: "Meeting Prep Automator" - General-purpose meeting prep for all meetings, includes participant backgrounds, prior interactions, recent news

**Analysis:** Both generate meeting prep documents by aggregating relationship/interaction data. InvRel-02 is specialized version for LP meetings with investor-specific data.

**Consolidation Recommendation:**
- **Shared infrastructure:** Both use calendar integration, meeting notes archive, relationship data
- **Options:**
  1. Build AD-01 as general framework, InvRel-02 as specialized extension
  2. Build InvRel-02 first (higher priority), then generalize to AD-01
  3. Build single "Meeting Prep" system with templates for different meeting types (investors, corporates, internal)
- **Recommendation:** Build InvRel-02 first (after InvRel-07 data warehouse), then assess if generalization to AD-01 is valuable
- **T-shirt size:** If building both: InvRel-02 (Medium, 4-6 weeks) + AD-01 (Medium, 4-6 weeks). If shared: Medium + Small extension (2-3 weeks)

**Impact:** Could save Small to Medium effort (2-6 weeks) if built as single system with meeting type templates vs. separate projects.

---

#### 5. CA-04 and CA-05 (Broker Analytics Overlap)
**Project IDs:** CA-04, CA-05
**Overlap Description:**
- CA-04: "Broker Utilization Analyzer" - Commission spend vs. value received, event allocation, research consumption, ROI ranking
- CA-05: "Corporate Access Reporting" - Event attendance by analyst/sector, allocation rates by bank, coverage gaps, utilization trends

**Analysis:** Both generate broker and corporate access analytics. CA-04 more broker-focused (ROI), CA-05 more event-focused (attendance), but significant overlap in data sources and outputs.

**Consolidation Recommendation:**
- **Single reporting project:** "Corporate Access & Broker Analytics"
- **Approach:** Build unified reporting system with multiple views:
  1. Broker utilization and ROI (CA-04 focus)
  2. Event attendance and allocation (CA-05 focus)
  3. Coverage gaps and planning recommendations
- **Dependency:** Both require CA-01 structured event data, broker relationship data
- **T-shirt size:** If separate: CA-04 (Medium, 6 weeks) + CA-05 (Small-Medium, 3 weeks). If consolidated: Medium (6-8 weeks total)
- **First step:** Observe CA-05 workflow to understand what reports are actually valuable

**Impact:** Eliminates duplicate analytics infrastructure, saves Small effort (2-4 weeks). Single system easier to maintain than two separate reports.

---

#### 6. PM-05 vs. IR-03 (Private Markets Q&A)
**Project IDs:** PM-05, IR-03
**Overlap Description:**
- PM-05: "Portfolio Company Q&A Bot" - Q&A over private company updates, CIMs, investment memos
- IR-03: "Research Document Q&A Bot" - Q&A over research documents, investment memos, company filings

**Analysis:** Both are RAG-based Q&A systems over investment documents. PM-05 focuses on private markets documents, but infrastructure is identical to IR-03.

**Consolidation Recommendation:**
- **PM-05 should be feature of IR-03, not standalone project**
- **Approach:**
  1. Build IR-03 with public market research documents
  2. Add private markets documents as additional document type
  3. Single Q&A interface queries across both public and private investment documents
- **Dependency:** PM-04 (Update Processor) builds data standardization for private company updates, which then feed into IR-03
- **T-shirt size:** If building separate PM-05: Medium (6 weeks). If adding to IR-03: Small extension (2-3 weeks to add private docs)

**Impact:** Saves Medium effort (4-6 weeks) by extending IR-03 vs. building separate RAG system. Unified search across all investment documents (public and private) more valuable than separate systems.

---

#### 7. Multiple Performance/Attribution Dependencies
**Project IDs:** IR-12, InvRel-03, InvRel-05
**Overlap Description:**
- IR-12: "Portfolio Performance Dashboard" - Portfolio-level performance tracking, attribution analysis
- InvRel-03: "Investor Letter First Draft" - Performance summary, top contributors/detractors
- InvRel-05: "Quarterly Cheat Sheet" - Performance chart, top contributors/detractors

**Analysis:** All three require performance and attribution data infrastructure. IR-12 builds comprehensive performance dashboard, InvRel-03/05 consume that data for investor communications.

**Consolidation Recommendation:**
- **Not truly separate projects, but clear dependency chain:**
  1. Build performance/attribution data infrastructure first (part of Financial Data Warehouse)
  2. Build IR-12 dashboard as primary performance interface
  3. InvRel-03 and InvRel-05 consume IR-12 data via API
- **Avoid:** Building separate performance data pipelines for IR vs. InvRel projects
- **Approach:** InvRel-03/05 should not re-implement attribution logic, but query IR-12 data
- **T-shirt size:** IR-12 (Medium-Large, includes data infrastructure). InvRel-03/05 become easier (Medium vs. Large) if they consume IR-12 data.

**Impact:** Ensures single source of truth for performance data. InvRel projects become simpler if IR-12 infrastructure exists first.

---

### Minor Overlaps (Shared Infrastructure, Not Duplicate Projects)

#### 8. All Slack Integration Projects
**Projects:** IR-01, IR-02, IR-03, IR-06, OF-10, plus MI alerts
**Shared Infrastructure:** Slack Integration Framework (Tier 1 infrastructure)

**Recommendation:** Build Slackbot framework once as Small foundational project, reuse across all Slack-based projects. Not duplicate projects, but clear infrastructure dependency.

---

#### 9. All Calendar Integration Projects
**Projects:** IR-01, IR-10, CA-01, CA-02, InvRel-01, InvRel-02, AD-01
**Shared Infrastructure:** Calendar Integration Framework (Tier 2 infrastructure)

**Recommendation:** Build calendar integration framework once (Small-Medium project), reuse across all calendar-based projects. Not duplicate projects, but shared component opportunity.

---

#### 10. All Document Processing Projects
**Projects:** IR-02, IR-03, IR-04, IR-07, PM-01, PM-02, PM-03, PM-04, LC-02, LC-03, LC-04, LC-06
**Shared Infrastructure:** Document processing pipeline (PDF/Word/Excel parsing, OCR, extraction)

**Recommendation:** Build document processing infrastructure as part of IR-03, reuse for all document-based projects. Different document types (research vs. legal vs. private markets) may need specialized parsing, but core pipeline is shared.

---

### Consolidation Summary Table

| Project IDs | Overlap Type | Consolidation Action | Effort Saved | Priority |
|---|---|---|---|---|
| InvRel-06 = LC-03 | **Duplicate project** | Single "Side Letter Query Bot" as part of IR-03 | Medium-Large (6-12 weeks) | **Critical** |
| AD-02 = IR-03 extension | **Duplicate project** | AD-02 is milestone of IR-03, not separate | Medium-Large (6-12 weeks) | **Critical** |
| AD-03 = IR-03 infrastructure | **Duplicate project** | AD-03 is first phase of IR-03 | Clarifies dependencies | **Critical** |
| InvRel-02 vs. AD-01 | Significant overlap | Build InvRel-02 first, generalize later if valuable | Small-Medium (2-6 weeks) | Medium |
| CA-04 and CA-05 | Significant overlap | Single "Corporate Access & Broker Analytics" | Small (2-4 weeks) | Medium |
| PM-05 vs. IR-03 | Significant overlap | PM-05 as feature of IR-03, not standalone | Medium (4-6 weeks) | Medium |
| IR-12, InvRel-03, InvRel-05 | Shared data dependency | IR-12 first, others consume its data | Ensures single source of truth | High |

**Total Effort Savings from Consolidation:** 20-40 weeks of development time by avoiding duplicate infrastructure and correctly scoping projects as features vs. standalone builds.

**Strategic Impact:**
- Eliminates 3 duplicate projects (InvRel-06/LC-03, AD-02, AD-03 as separate from IR-03)
- Reframes 3 projects as features/extensions rather than standalone (PM-05, AD-02, AD-03)
- Identifies 2 consolidation opportunities (CA-04/05, InvRel-02/AD-01)
- Clarifies dependency chain for performance data (IR-12 → InvRel-03/05)
- Reduces total project count from 60 to approximately 50-55 distinct builds

---

## Conclusion

This infrastructure and roadmap analysis reveals:

1. **7 Tier 1 foundational components** enable 40+ of 60 use cases
2. **Document Repository & RAG System (IR-03)** is the single highest-leverage investment (13 projects)
3. **Financial Data Warehouse** is critical for Investment Research and Investor Relations (11 projects)
4. **15-20 use cases** are strong "buy vs. build" candidates, focusing in-house development on core competencies
5. **3 duplicate projects** should be consolidated (InvRel-06/LC-03, AD-02, AD-03)
6. **4-phase roadmap** balances foundation building with quick wins, delivering value throughout implementation

**Recommended First Actions:**
1. Begin IR-03 (Document Repository & RAG) as foundational Large project
2. Build Slack Integration Framework as quick foundational Small project
3. Launch CA-01 (Event Tracker) as first quick win with minimal dependencies
4. Start Financial Data Warehouse to enable Investment Research section
5. Initiate build vs. buy evaluations for Legal & Compliance (Harvey, compliance AI tools)

By following this strategic roadmap and consolidating overlapping projects, the firm can systematically implement 50-55 of 60 use cases over 18-24 months while maximizing infrastructure reuse and minimizing duplicate effort.
