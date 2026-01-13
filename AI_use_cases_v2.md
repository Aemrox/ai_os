# AI use cases — v2

## Objective

Boost efficiency and decision-making efficacy across XN's teams by leveraging AI for automation and insight generation. Goal is to free employees from low-value, manual tasks to focus on high-value analysis, judgement, and alpha generation.

---

## Investment Research & Analysis

### IR-01: Earnings Preview Generator

**Trigger:** 24-48 hours before scheduled earnings release (detected via earnings calendar)

**Process:** AI compiles pre-earnings briefing for upcoming report. Pulls current consensus estimates and recent revision trends. Surfaces XN's internal expectations from BipSync notes and compares against Street. Identifies key debates and controversies from recent broker research. Extracts questions management dodged or addressed poorly last quarter. Flags specific metrics and commentary topics to monitor.

**Output:** Earnings preview document posted to relevant Slack channel containing: (1) Consensus estimates for key metrics with recent revision direction, (2) XN view vs. Street (where we differ and why), (3) Key debates to listen for (e.g., "Street expects margin expansion but management has been noncommittal") (4) Management credibility check (did they deliver on last quarter's promises?)

**T-shirt size:**
**Medium to Large** — Size depends on API availability and required interactivity.

**Questions:**
- Data sourcing: What are the primary data sources, and how accessible are their APIs?
- What are the human-in-the-loop interaction points?
- Do standardized report templates exist, or do these need to be developed?
- This could serve as a pilot project for evaluating AI workflow tools.

---

### IR-02: Investment Memo Devil's Advocate

**Trigger:** Analyst uploads draft investment memo (Word/PDF) to designated folder or Slack channel

**Output:** Pre-mortem document delivered to analyst containing: (1) Summary of thesis as understood, (2) Contradictory evidence with source citations and links, (3) Risk factors not addressed in memo, (4) Questions the IC might ask, (5) Historical analogies of similar setups that failed

**T-shirt size:**
**Small to Medium** — Assumes limited external sources (primarily web search) for evaluation. Size increases significantly if this requires the same comprehensive information access as IR-03, at which point this becomes a feature of IR-03 rather than a standalone product.

**Questions:**
- What content is typically included in these investment memos?
- **Critical:** What sources should be consulted to effectively evaluate the memo?
- Workflow considerations: Is Slack the optimal trigger, or would integration into an AI chat interface be preferable? V1 scope needs definition.
- Prompt engineering will be critical; recommend establishing an evaluation framework to ensure quality.

---

### IR-03: Research Document Q&A Bot

**Trigger:** Natural language question asked via Slack command (e.g., What's our thesis on NVDA?)

**Process:** AI interprets the question, searches across all connected sources, retrieves relevant passages, and synthesizes a coherent answer. Cites specific documents and timestamps. If information is stale (>90 days), flags this in response.

**Output:** Slack response containing: (1) Direct answer to question, (2) Supporting evidence with citations, (3) Links to source documents, (4) Date of most recent relevant information, (5) Follow-up questions to refine if needed

**T-shirt size:**
**Extra Large** — This is an ongoing, iterative project with substantial scope as functionality is added and the company knowledge base is structured. Recommend small, agile iterations to deliver incremental value while refining the implementation.

**Questions:**
- Workflow considerations: Slack integration adds overhead. Consider developing a solid Slackbot codebase as a foundational pre-project before full integration.
- Data scope and architecture: What data sources should be included, and where does this data currently reside?
- Are there common, high-value questions that could define an initial MVP? Starting with predefined queries would enable stepwise delivery of immediate value.
- Many other use cases could ultimately become features of this bot, as it necessitates core infrastructure: MCP tools, comprehensive data aggregation, and Slack integration.
- Recommend collaborative technical specification session to map dependencies and define phased implementation.  

---

### IR-04: Automated Research Digest

**Trigger:** Daily schedule (6:00 AM) or on-demand request

**Process:** AI identifies new research relevant to each analyst's coverage universe. Summarizes key points from each piece. Personalizes digest based on individual coverage assignments and stated interests. Prioritizes by materiality and timeliness.

**Output:** Personalized email to each analyst containing: (1) Priority reads with one-sentence summaries, (2) Secondary reads organized by ticker, (3) "You might have missed" section for tangentially relevant items, (4) Direct links to full documents

**T-shirt size:**
**Small** if leveraging established feeds with minimal customization. Escalates to **Medium to Large** if requirements include deep ongoing customization, feedback mechanisms, and proactive research capabilities.

**Questions:**
- Scope is highly dependent on research source breadth and variety. Aggregating established email subscriptions or ticker feeds is straightforward; proactive search functionality increases complexity substantially.
- How are analyst domains defined? What level of customization is required—simple company/ticker lists, or fully customized feeds per analyst?

---

### IR-05: Company Comps Generator

**Trigger:** On demand or upon submission

**Process:** AI identifies appropriate peer set based on sector, business model, and size. Pulls current financials and forward estimates. Calculates relevant multiples (EV/Revenue, EV/EBITDA, P/E, etc.). Formats into XN's standard comp table template.

**Output:** Excel file (maybe dashboard?) containing: (1) Formatted comp table with peers, (2) Trading multiples (current, NTM, historical range), (3) Growth and margin metrics, (4) Data footnotes with pull dates, (5) Suggested additions/removals based on AI peer analysis

**T-shirt size:**
**Large to Extra Large** if building from scratch with custom underlying tools. Reduces to **Medium** if solid financial data and trading data infrastructure already exists.

**Questions:**
- Workflow observation needed: Require walkthrough of current analyst workflow to accurately assess complexity.
- Quality assurance: Given the objective nature of this output, recommend establishing a robust evaluation framework to ensure accuracy.
- Data infrastructure: Scope depends on consolidation and availability of financial data. A comprehensive data warehouse would address this dependency and provide reusable infrastructure for multiple projects.
- Hidden dependencies: This project requires tools for pulling and assembling financial and trading data that will have broader utility across other use cases.

---

### IR-06: Consensus Estimate Change Monitor

**Trigger:** Daily schedule (7:00 AM) and real-time for material changes (>5% revision)

**Process:** AI monitors estimate revisions across XN's coverage universe. Calculates magnitude of change versus prior consensus. Identifies which analysts revised and their historical accuracy. Contextualizes change against recent company news or events.

**Output:** Alert for material changes containing: (1) Ticker and metric changed, (2) Old vs. new consensus, (3) Which analysts revised and direction, (4) Likely catalyst (linked to recent news if identifiable), (5) Historical context (is this analyst typically early/accurate?). Daily summary email with all changes.

**T-shirt size:**
Difficult to estimate without additional clarification on requirements and data sources.

**Questions:**
- Data source clarification needed: Does this use trading data, analyst reports, or both? Either option suggests dependencies on underlying infrastructure (real-time aggregation of financial data, analyst reports, and trading data).
- Real-time vs. scheduled: Real-time monitoring significantly increases complexity, requiring persistent server infrastructure and service deployment. Reducing to hourly or periodic scheduling substantially decreases scope.
- Overlap with IR-04: This appears functionally similar to the Automated Research Digest. Clarify differentiating requirements, or consider implementing as a feature of IR-04. 

---

### IR-07: Expert Call Insight Extractor

**Trigger:** New expert transcript available in AlphaSense/Tegus

**Process:** AI reads expert transcript and extracts: key claims with confidence level, data points cited, areas of expertise validation, and potential biases. Compares expert's view against other experts on same topic. Cross-references against XN's internal thesis.

**T-shirt size:**
**Small** if data is readily accessible with straightforward workflow. Increases if data cleaning and aggregation are required. Escalates to **Medium** if external research is needed to validate expert credentials.

**Questions:**
- Note: This functionality exists in many AI tools currently available.
- Are transcripts already available in a structured format? Is cross-referenced data easily accessible?
- Expertise validation: What sources are available to verify expert credentials and background?

---

### IR-08: Investment Memo First Draft Generator

**Trigger:** Analyst request with specified ticker and thesis direction

**Process:** AI gathers all available information on the company. Structures a first draft (at least business context?) following XN's investment memo template. Populates sections with relevant data and analysis. Flags gaps where additional research is needed. Includes placeholder for analyst's proprietary view.

**Output:** Word document containing: (1) Company overview with key statistics, (2) Industry context and competitive position, (3) Historical financial summary, (4) Valuation analysis with comps, (5) Risk factors from 10-K, (6) Thesis section (placeholder for analyst input), (7) Flagged gaps requiring additional work

**T-shirt size:**
**Medium** for MVP iteration, but recommend treating as **Large** with extended research phase. This project could establish foundational infrastructure for multiple other use cases (IR-02, IR-03) and warrants careful implementation.

**Questions:**
- Strategic value: Strong candidate for initial implementation as it provides base infrastructure for both devil's advocate (IR-02) and research bot (IR-03) use cases.
- Template requirements: What data and analytics are included in the memo template? This will significantly impact scope and requires detailed review.
- Financial data dependency: Historical financials requirement flags need for comprehensive financial data collection infrastructure.
- Dependencies: If comps are essential, IR-05 becomes a prerequisite.
- Human-in-the-loop touchpoints: Beyond the thesis section, what other analyst input points are required? Should the thesis be provided upfront, or is the entire document intended as preparatory material for thesis development?
- Gap identification: Defining "sufficient" is challenging. Recommend training on or few-shot prompting with existing investment memos to establish quality standards for gap evaluation. 

---

### IR-09: Quantitative Screen with Qualitative Filter

**Trigger:** Weekly schedule (Monday 6:00 AM) or on-demand with custom parameters

**Process:** AI runs quantitative screen based on specified parameters (e.g., Revenue growth >20%, P/E <20, Market cap >$5B). For companies passing quant screen, reads most recent earnings transcript and filters for qualitative keywords (e.g., "AI tailwinds," "market share gains," "new product launch"). Ranks results by combined score.

**Output:** Report containing: (1) List of companies passing both filters, (2) Key statistics for each, (3) Relevant transcript excerpts explaining qualitative match, (4) Link to full screen results, (5) Changes versus prior week's screen

**T-shirt size:**
**Small** for V1 if financial search criteria are well-structured and accessible via third-party APIs. Escalates to **Large or Extra Large** if custom data aggregation and filtering is required. Size also depends on approach to maintaining and updating keyword evaluation criteria for transcripts.

**Questions:**
- Trading data interface: Scope heavily dependent on available APIs and interfaces. Natural language to search conversion is straightforward if all parameters are accessible via third-party services; becomes significantly more complex if custom data aggregation is needed.
- Evaluation maintenance: Post-screening evaluation is iterative and requires ongoing refinement. How will keyword lists and scoring criteria be maintained and updated?
- Output clarification: What differentiates the summary report from the "full results" screen?

---

### IR-10: Macro Event Portfolio Impact Analyzer

**Trigger:** Major news event detected (e.g., "port strike," "tariff announcement," "rate decision") or on-demand query

**Process:** AI identifies the macro event and relevant keywords. Searches all portfolio company docs for related risk factor disclosures. Analyzes management commentary on the topic from recent transcripts. Maps potential exposure by position size.

**Output:** Risk exposure report containing: (1) Event summary, (2) Portfolio companies with relevant risk factor language (with excerpts), (3) Management commentary on the topic, (4) Position-weighted exposure ranking, (5) Historical examples of similar events and portfolio impact

**T-shirt size:**
**Medium** if leveraging an existing feed of major events for an MVP that highlights events, identifies portfolio company risk exposures, and aggregates citations and reactions. **XXXL** if proactive event detection and news aggregation are required.

**Questions:**
- Risk assessment: Event detection and market impact analysis is a mature product category with significant complexity. Strongly recommend leveraging an existing event feed rather than building detection capabilities from scratch.
- Is there an existing event feed currently ingested that this could build upon? 

---

### IR-11: Portfolio Scenario Analyzer

**Trigger:** On-demand request specifying scenario parameters

**Process:** AI models portfolio impact under specified scenarios (e.g., rates +100bps, oil +20%, recession probability increase). Uses historical factor sensitivities and company-specific exposures. Generates range of outcomes with confidence intervals.

**Output:** Scenario analysis report containing: (1) Portfolio P&L impact under base/bull/bear for each scenario, (2) Most exposed positions (positive and negative), (3) Factor decomposition of exposures, (4) Hedging suggestions, (5) Historical analogs and actual outcomes

**T-shirt size:**
**XL to XXXL** regardless of approach. Even with an established, validated model, this remains **Large to XL** due to data infrastructure requirements and report construction complexity.

**Questions:**
- **Critical limitation:** This task exceeds the capabilities of standard LLMs, which will produce unreliable and hallucinated outputs for complex financial modeling.
- This is fundamentally an ML engineering project requiring a production ML pipeline, comprehensive financial data warehouse, and validated models—not an LLM application.
- Strong recommendation: Partner with or license from an established provider rather than building from scratch. This requires specialized expertise beyond typical LLM implementation. 

---

### IR-12: Quarterly Performance Review Data Compiler

**Trigger:** Month-end schedule (T+3 after month close) or on-demand

**Process:** AI aggregates performance data across required dimensions: attribution by sector/position, alpha vs. beta decomposition, gross/net returns, factor exposures, portfolio turnover, win/loss rates, ROIC by position.

**Output:** Formatted QPR data package containing: (1) Performance summary tables, (2) Attribution waterfall, (3) Factor exposure charts, (4) Position-level P&L, (5) QoQ and YoY comparisons

**T-shirt size:**
**Medium to Large** in best-case scenario, assuming comprehensive financial data warehouse, available analysis tools, and straightforward conversion of custom models to tools. Scope depends heavily on financial analysis tool complexity.

**Questions:**
- **Prerequisite:** Comprehensive financial data integration is required before this project can begin.
- Computational approach: LLMs are not well-suited for mathematical analysis. Recommend building dedicated calculation tools rather than relying on LLM computation.
- What existing financial analysis tools and libraries are available? Additional discovery needed.
- Visualization requirements: Research needed on charting libraries that meet investment team standards. Expect iterative refinement.

---

### IR-13: Trading Strategy Back-tester

**Trigger:** On-demand request with specified strategy parameters

**Process:** AI backtests specified trading intuitions (e.g., sizing rules, entry/exit timing, options strategies) against historical data. Accounts for transaction costs, slippage, and corporate actions. Generates performance statistics and identifies regime-dependent results.

**Output:** Backtest report containing: (1) Strategy P&L over test period, (2) Risk-adjusted returns, (3) Comparison to alternative parameter sets, (4) Statistical significance assessment

**T-shirt size:**
**XL to XXXL** — Similar in scope and complexity to IR-11.

**Questions:**
- This is an ML engineering project complementary to IR-11 with comparable complexity.
- Strategy detail requirements: Significant scope difference between simple trade execution analysis ("execute this trade on this date") versus AI-driven strategy execution (which would require IR-11 as prerequisite).
- Expertise gap: Comprehensive understanding of backtesting methodologies required before providing accurate estimate.
- Strong recommendation: Research existing backtesting tools and platforms before considering custom development.

---

## Market Intelligence

### MI-01: Portfolio Company News Monitor

**Trigger:** Continuous (real-time during market hours) with daily digest at 6:30 AM

**Process:** AI monitors all news sources for portfolio company mentions. Scores each item for materiality (price-moving potential) and relevance. Filters out noise (routine press releases, duplicate coverage). Clusters related stories.

**Output:** Real-time Slack alerts for high-materiality items. Daily digest email containing: (1) Top stories by position with one-sentence summaries, (2) Sentiment indicators, (3) Stories requiring analyst attention flagged, (4) Coverage gaps (positions with no recent news)

**T-shirt size:**

**Questions:**

---

### MI-02: Competitor Intelligence Tracker

**Trigger:** Continuous monitoring with weekly synthesis

**Process:** AI monitors competitors of each portfolio company across multiple dimensions: earnings results, guidance changes, product announcements, executive changes, hiring patterns, patent filings. Identifies developments that could impact portfolio company competitive position.

**Output:** Weekly competitor briefing per coverage sector containing: (1) Material competitor developments, (2) Hiring trend analysis (who's scaling vs. cutting), (3) Product/strategy shifts, (4) Implications for portfolio companies, (5) Suggested follow-up research

**T-shirt size:**

**Questions:**

---

### MI-03: Industry News Synthesizer

**Trigger:** Daily (6:00 AM) and weekly (Monday morning comprehensive)

**Process:** AI aggregates industry news across XN's coverage sectors. Identifies themes and trends across multiple stories. Separates signal (new information) from noise (repeated coverage). Highlights implications for portfolio.

**Output:** Daily brief containing: (1) Top industry developments per sector, (2) Emerging themes across stories, (3) Portfolio relevance notes. Weekly synthesis adding: (4) Trend analysis, (5) Data points worth tracking, (6) Suggested deep-dives

**T-shirt size:**

**Questions:**

---

### MI-04: Regulatory Filing Monitor

**Trigger:** Real-time for material filings; daily digest for routine

**Process:** AI monitors SEC filings for portfolio companies and key holders. For 8-Ks, extracts material event type and key details. For 13-Fs, tracks position changes by notable investors. For Form 4s, identifies insider buying/selling patterns. Scores each filing for significance.

**Output:** Alerts for material 8-Ks containing: (1) Filing type, (2) Key disclosure summary, (3) Market implications, (4) Link to full filing. Daily digest of all filings with significance scores. Weekly 13-F summary of smart money movements.

**T-shirt size:**

**Questions:**

---

### MI-05: Social Sentiment Monitor

**Trigger:** Continuous during market hours with alerts for significant shifts

**Process:** AI monitors social platforms for portfolio company mentions. Analyzes sentiment and detects unusual volume or sentiment shifts. Filters out bot activity and low-quality posts. Identifies influential accounts driving conversation.

**Output:** Alert for significant sentiment shifts containing: (1) Ticker and direction of shift, (2) Volume comparison to baseline, (3) Representative posts driving sentiment, (4) Influential accounts involved, (5) Potential catalyst if identifiable. Weekly social sentiment summary across portfolio.

**T-shirt size:**

**Questions:**

---

### MI-06: Hiring Pattern Intelligence

**Trigger:** Weekly analysis (Monday morning)

**Process:** AI tracks job postings and headcount changes at portfolio companies and competitors. Categorizes postings by function (engineering, sales, etc.) and seniority. Identifies acceleration or deceleration versus historical baseline. Detects strategic shifts indicated by new role types.

**Output:** Weekly hiring intelligence report containing: (1) Net headcount changes by company, (2) Hiring acceleration/deceleration flags, (3) New role types suggesting strategic shifts, (4) Competitive hiring comparison, (5) Employee sentiment trends from Glassdoor

**T-shirt size:**

**Questions:**

---

### MI-07: Management Commentary Tracker

**Trigger:** After each earnings call; quarterly synthesis

**Process:** AI tracks what management says about specific topics (margins, competition, capex, hiring, demand) across multiple quarters. Identifies changes in tone or substance. Flags contradictions with prior statements. Compares commentary against actual results.

**Output:** Topic-specific tracking report containing: (1) Management quotes on topic by quarter, (2) Tone/substance change flags, (3) Contradictions with prior statements, (4) Accuracy scorecard (did they deliver what they promised?), (5) Red flags for IC discussion

**T-shirt size:**

**Questions:**

---

## Private Markets

### PM-01: CIM Analyzer

**Trigger:** New CIM uploaded to deal folder in Egnyte

**Process:** AI extracts key information from CIM: business description, financial metrics (revenue, EBITDA, growth rates), customer concentration, management team, risk factors, deal terms if included. Compares metrics against public comps and prior XN private deals. Flags unusual terms or metrics.

**Output:** CIM summary document containing: (1) One-page business overview, (2) Key financial metrics in standard format, (3) Comparison to public comps, (4) Comparison to prior XN deals, (5) Risk factor summary, (6) Flags and questions for further diligence, (7) Recommendation on whether to proceed

**T-shirt size:**

**Questions:**

---

### PM-02: Data Room Document Processor

**Trigger:** New documents added to data room (detected via folder monitoring)

**Process:** AI processes new data room documents as they arrive. Classifies by document type. Extracts key information relevant to diligence. Tracks completeness against standard checklist. Flags missing items, inconsistencies, or risk factors.

**Output:** Running data room digest containing: (1) New documents summary with key extracts, (2) Checklist completion status, (3) Missing items list, (4) Inconsistencies across documents, (5) Risk factors identified, (6) Questions for management

**T-shirt size:**

**Questions:**

---

### PM-03: Deal Terms Comparison

**Trigger:** On-demand when evaluating new deal terms

**Process:** AI compares proposed deal terms against XN's historical private investments and available market data. Analyzes valuation metrics, governance terms, liquidation preferences, anti-dilution provisions, board rights, information rights, and other material terms.

**Output:** Deal comparison report containing: (1) Term-by-term comparison to XN historical average, (2) Valuation metrics vs. comparable deals, (3) Governance terms assessment, (4) Flags for terms outside normal range, (5) Suggested negotiation points

**T-shirt size:**

**Questions:**

---

### PM-04: Private Portfolio Company Update Processor

**Trigger:** Monthly/quarterly report received from portfolio company (email attachment or data room upload)

**Process:** AI extracts key metrics from unstructured reports (revenue, EBITDA, cash burn, headcount, KPIs). Compares against prior periods and projections. Identifies variances and trends. Populates standardized tracking template.

**Output:** Standardized update containing: (1) Key metrics in consistent format, (2) Variance analysis vs. prior period and budget, (3) Trend charts, (4) Flags for metrics outside expected range, (5) Data populated in XN tracking model. Alert if update is overdue.

**T-shirt size:**

**Questions:**

---

### PM-05: Private Investment Q&A Bot

**Trigger:** Natural language question chatbot (e.g., What was our price/share in Grok Series B?)

**Process:** AI interprets question and searches private investment records. Handles queries about: investment history, pricing across rounds, ownership percentages, board seats, valuation marks, company metrics over time.

**Output:** Direct answer with supporting data: (1) Answer to specific question, (2) Source document reference, (3) Related context (e.g., if asking about pricing, includes ownership % and current mark), (4) Last update date

**T-shirt size:**

**Questions:**

---

## Operations & Finance

### OF-01: Expense Report Generator

**Trigger:** End of month or on-demand request from employee

**Process:** AI aggregates credit card transactions and uploaded receipts. Matches receipts to transactions. Categorizes expenses. Cross-references calendar for business purpose. Checks against expense policy. Generates formatted expense report.

**Output:** Draft expense report containing: (1) Categorized expenses with receipts attached, (2) Business purpose (auto-populated from calendar where possible), (3) Policy compliance flags, (4) Missing receipts list, (5) Ready for employee review and submission

**T-shirt size:**

**Questions:**

---

### OF-02: Spend Analytics Dashboard

**Trigger:** Monthly schedule (first week of month) and on-demand

**Process:** AI aggregates and analyzes spending across all categories. Identifies trends, anomalies, and opportunities. Evaluates vendor concentration. Compares against budget. Suggests consolidation opportunities.

**Output:** Monthly spend report containing: (1) Spend by category with trends, (2) Top vendors with YoY comparison, (3) Budget variance analysis, (4) Anomaly flags (unusual spending patterns), (5) Consolidation opportunities (multiple vendors for same service), (6) Contract renewal calendar

**T-shirt size:**

**Questions:**

---

### OF-03: Month-End Close Automator

**Trigger:** Month-end schedule (close calendar)

**Process:** AI generates recurring journal entries from templates. Calculates standard accruals based on defined methodologies. Prepares reconciliation. Identifies unusual balances requiring review. Custom reporting for Fund and Monthly Financials for Mgmt Co.

**Output:** Close package containing: (1) Recurring entries posted, (2) Accrual calculations with support, (3) Reconciliation templates populated, (4) Unusual balance flags, (5) Close checklist progress, (6) Variance analysis vs. prior month

**T-shirt size:**

**Questions:**

---

### OF-04: Annual Budget Preparation Assistant

**Trigger:** Annual budget cycle kickoff (typically Q4) or on-demand for reforecasts

**Process:** AI compiles budget inputs from multiple sources. Pulls historical actuals by category and cost center. Analyzes spending trends and seasonality patterns. Incorporates known commitments (contracts, headcount plans, scheduled investments). Flags areas with significant YoY variance for review. Generates first-pass budget by applying growth assumptions to historical baseline.

**Output:** Draft budget package containing: (1) Historical spending by category with trend analysis, (2) First-pass budget by cost center using defined assumptions, (3) YoY variance analysis with drivers, (4) Known commitments and step-changes itemized, (5) Areas flagged for management input (discretionary spend, new initiatives), (6) Comparison to prior year budget vs. actual performance

**T-shirt size:**

**Questions:**

---

### OF-05: Management Fee Calculator

**Trigger:** Monthly/quarterly schedule per fund terms

**Process:** AI calculates management and performance fees according to fund documents. Applies investor-specific terms from side letters. Generates fee notices and supporting calculations. Maintains audit trail.

**Output:** Fee package containing: (1) Fee calculations by fund and investor, (2) Supporting detail and methodology, (3) Side letter adjustments applied, (4) Comparison to prior period, (5) Fee notices ready for distribution, (6) Audit trail documentation

**T-shirt size:**

**Questions:**

---

### OF-06: Incentive Fee Calculator

**Trigger:** Quarterly/annual schedule per fund terms (crystallization periods) or on-demand for estimates

**Process:** AI calculates incentive fees by investor according to fund documents. Tracks high water marks by investor and series. Applies hurdle rates where applicable. Calculates performance above HWM and hurdle. Applies investor-specific terms from side letters (reduced rates, modified hurdles, founders terms). Handles crystallization timing and loss carryforward. Generates investor-level fee calculations with full supporting detail.

**Output:** Incentive fee package containing: (1) Fee calculations by investor with performance detail, (2) High water mark tracking (prior HWM, current NAV, accrued catch-up), (3) Hurdle rate calculations where applicable, (4) Side letter adjustments applied (rate reductions, modified terms), (5) Crystallization schedule and timing, (6) Comparison to prior period and year-to-date accrual, (7) Audit trail with methodology documentation

**T-shirt size:**

**Questions:**

---

### OF-07: Daily Tax Lot Processor

**Trigger:** On-demand query (e.g., "Where is the NVDA tax lot from March?") or scheduled reporting

**Process:** AI ingests all Enfusion tax lot tables across funds and accounts. Indexes lots by security, acquisition date, cost basis, holding period, and basket assignment. For queries, searches across tables to locate specific lots and returns location, status, and key attributes. For reporting, aggregates lots by basket, calculates realized/unrealized gains by tax character, and generates basket-level summaries.

**Output:** For queries: Direct answer with lot location, cost basis, holding period status, and basket assignment. For reporting: (1) Tax lot inventory by basket with acquisition dates and cost basis, (2) Holding period status (short-term vs. long-term) by lot, (3) Realized gains/losses by basket with tax character, (4) Unrealized gain/loss summary by basket, (5) Wash sale exposure flags

**T-shirt size:**

**Questions:**

---

### OF-08: Daily Cash Position Summary

**Trigger:** Daily schedule (8:00 AM)

**Process:** AI aggregates cash positions across all accounts. Reconciles against expected balances. Identifies discrepancies. Calculates total available liquidity by currency. Important for KFO and Mgmt Co (in Quickbooks, but would like to see standalone)

**Output:** Cash summary for DL containing: (1) Total cash by currency and account type, (2) Comparison to prior day and expected, (3) Discrepancy flags, (4) Large movements highlighted, (5) Liquidity availability summary

**T-shirt size:**

**Questions:**

---

### OF-09: Capital Flows Report Generator

**Trigger:** Monthly schedule (first business day of month) or on-demand on Dashboard

**Process:** AI aggregates all subscription, redemption, and transfer activity across funds (Exponent, Vector, Amplify) for the reporting period. Pulls data from investor records and fund admin systems. Categorizes flows by external vs. internal, and by series/tranche. Calculates net capital flows by fund and in aggregate.

**Output:** Capital flows report ready for email distribution containing: (1) Summary table showing inflows, outflows, and net flows by fund, (2) Detailed subscription schedule with investor name, amount, series/tranche, and notes, (3) Detailed redemption schedule with investor name, net amount, series/tranche, and notes, (4) Transfer schedule showing series transfers and account movements, (5) Comparison to prior month and YTD cumulative flows

**T-shirt size:**

**Questions:**

---

### OF-10: Daily Reconciliation Monitor

**Trigger:** Daily schedule (end of day) with ongoing tracking for open items

**Process:** AI ingests reconciliation data from automated feeds. Compares positions and trades across internal systems and counterparties. Identifies breaks and categorizes by type (price, quantity, missing trade, timing). For unsettled trades, tracks aging and assigns ownership (JG/CK). Monitors resolution progress on open items. Escalates aged breaks based on defined thresholds.

**Output:** Daily Slack post to operations channel containing: (1) Reconciliation summary (matched vs. breaks), (2) New breaks identified with details and suggested resolution, (3) Open items tracker showing owner, age, and status, (4) Unsettled trades list with expected settlement dates, (5) Escalation flags for items exceeding age thresholds, (6) Week-over-week trend on break volume

**T-shirt size:**

**Questions:**

---

### OF-11: Statement Reconciliation Processor

**Trigger:** Monthly/quarterly statements received from counterparties (PDF via email or portal)

**Process:** AI extracts data from PDF statements using OCR. Parses account balances, positions, transactions, and fees from various statement formats (prime brokers, custodians, fund admin). Compares extracted values against internal Excel records. Identifies discrepancies and calculates variance amounts. Flags items requiring investigation.

**Output:** Reconciliation workpaper containing: (1) Side-by-side comparison of statement vs. Excel, (2) Matched items confirmed, (3) Discrepancies identified with variance amounts, (4) Suggested explanations for common variance types, (5) Items requiring manual investigation flagged, (6) Audit trail of source documents and extraction confidence scores

**T-shirt size:**

**Questions:**

---

## Legal & Compliance

### LC-01: End-of-Day Trade Surveillance

**Trigger:** Daily schedule (end of trading day)

**Process:** AI reconciles all trades against compliance constraints. Checks trades against restricted list. Cross-references with corporate access events and expert calls in surrounding time window. Applies compliance rules. Flags potential violations for review.

**Output:** Surveillance report containing: (1) Trades cleared (no issues), (2) Flags requiring review with: trade details, rule triggered, relevant context (meeting, call, etc.), (3) Resolution actions required, (4) Audit trail

**T-shirt size:**

**Questions:**

---

### LC-02: Vendor Contract Reviewer

**Trigger:** New contract uploaded for legal review

**Process:** AI reviews contract against XN's standard positions. Extracts key terms: liability, indemnification, termination, IP, data handling, etc. Compares against playbook. Identifies deviations and risks. Suggests redlines based on historical negotiations.

**Output:** Contract review memo containing: (1) Key terms summary, (2) Deviations from XN standard, (3) Risk assessment, (4) Suggested redlines with rationale, (5) Comparison to similar historical contracts, (6) Recommended negotiation priorities

**T-shirt size:**

**Questions:**

---

### LC-03: Side Letter Term Repository

**Trigger:** On-demand query or new side letter drafted

**Process:** AI maintains searchable repository of all side letter terms by provision type. For queries, returns relevant precedents. For new drafts, suggests language based on similar prior letters. Tracks which investors have which provisions.

**Output:** For queries: Relevant precedent language with investor/date context. For new letters: Suggested language with sources. Matrix view of which investors have which provisions.

**T-shirt size:**

**Questions:**

---

### LC-04: NDA Processor

**Trigger:** NDA request via email or form submission

**Process:** AI selects appropriate NDA template based on deal type and counterparty. Pre-populates party information. Adjusts terms based on counterparty type (corporate vs. PE vs. individual). For incoming NDAs, compares against XN standard and flags deviations.

**Output:** For outgoing: Completed NDA ready for signature. For incoming: Review summary with deviation flags and suggested responses.

**T-shirt size:**

**Questions:**

---

### LC-05: Marketing Footnote Generator

**Process:** AI scans marketing content for claims requiring disclosure. Generates appropriate footnotes based on claim type. Applies current regulatory requirements. Cross-references with prior approved language.

**Output:** Footnote suggestions containing: (1) Flagged claims requiring disclosure, (2) Suggested footnote language, (3) Regulatory basis, (4) Prior approved language for similar claims, (5) Items requiring legal judgment

**T-shirt size:**

**Questions:**

---

### LC-06: Fund Document Assistant

**Trigger:** On-demand query or new document drafting

**Process:** AI provides searchable access to all fund documentation. For queries, returns relevant provisions across documents. For drafting, suggests language based on prior documents and current requirements. Tracks document versions and amendments.

**Output:** For queries: Relevant provisions with document/section citations. For drafting: Suggested language with precedent sources. Version tracking and amendment summary.

**T-shirt size:**

**Questions:**

---

### LC-07: Policy Monitoring System

**Trigger:** Continuous regulatory monitoring; periodic internal policy review

**Process:** AI monitors regulatory developments relevant to XN. Compares new requirements against existing internal policies. Identifies gaps or conflicts. Flags upcoming compliance deadlines.

**Output:** Monthly regulatory update containing: (1) New regulations/guidance affecting XN, (2) Policy gaps identified, (3) Recommended policy updates, (4) Compliance calendar, (5) Industry peer responses (where available)

**T-shirt size:**

**Questions:**

---

## Investor Relations

### IR-01: LP Communication Drafter

**Trigger:** Request for routine LP communication (meeting confirmation, update, etc.)

**Process:** AI generates draft communication based on request type. Personalizes for specific LP using relationship history. Applies appropriate tone and format. Includes relevant attachments or links.

**Output:** Draft communication containing: (1) Personalized message, (2) Relevant context from relationship history, (3) Appropriate attachments, (4) Suggested follow-up actions

**T-shirt size:**

**Questions:**

---

### IR-02: Investor Meeting Prep Generator

**Trigger:** Investor meeting scheduled (detected via calendar)

**Process:** AI generates meeting briefing document. Compiles: relationship history, prior meeting notes, questions they've asked, their portfolio allocation, relevant recent developments. Prepares answers to likely questions based on historical pattern.

**Output:** Meeting brief containing: (1) LP profile and relationship summary, (2) Prior meeting notes and open items, (3) Questions they typically ask with prepared answers, (4) Relevant portfolio updates for their interests, (5) Suggested talking points, (6) Open items to address

**T-shirt size:**

**Questions:**

---

### IR-03: Investor Letter First Draft

**Trigger:** Quarterly schedule or on-demand

**Process:** AI generates first draft of quarterly letter. Incorporates: performance summary, top contributors/detractors, portfolio positioning, market outlook framework. Maintains consistent voice based on prior letters. Flags sections requiring PM/CIO input.

**Output:** Draft letter containing: (1) Performance summary, (2) Portfolio commentary, (3) Market discussion framework, (4) Outlook section (placeholder for PM input), (5) Sections flagged for review

**T-shirt size:**

**Questions:**

---

### IR-04: DDQ Response

**Trigger:** New DDQ received (Excel/Word document)

**Process:** AI reads new DDQ questions. Matches each question to prior responses. Suggests answers using most recent approved language. Updates data fields with current information. Flags questions requiring new responses or review.

**Output:** Pre-populated DDQ containing: (1) Suggested answers for each question, (2) Confidence score per answer, (3) Source of suggested answer (prior DDQ reference), (4) Flags for questions needing fresh response, (5) Data fields updated to current

**T-shirt size:**

**Questions:**

---

### IR-05: Quarterly Cheat Sheet Generator

**Trigger:** Monthly/quarterly schedule (after NAV finalization)

**Process:** AI generates visual summary of fund status. Compiles: AUM trend, performance summary, top contributors/detractors, key exposures, position-level theses. Formats for LP consumption.

**Output:** One-page cheat sheet containing: (1) AUM and flow summary, (2) Performance chart and statistics, (3) Top 5 contributors/detractors with brief thesis, (4) Key exposures (sector, geography, factor), (5) Notable position changes

**T-shirt size:**

**Questions:**

---

### IR-06: Side Letter Query Bot

**Trigger:** Natural language question

**Process:** AI interprets question and queries side letter repository. Handles queries about: which LPs have specific provisions, what terms apply to specific LP, comparison of terms across LPs.

**Output:** Direct answer with: (1) Response to specific question, (2) Supporting detail (LP names, specific language), (3) Related provisions that may be relevant, (4) Caveats or exceptions

**T-shirt size:**

**Questions:**

---

### IR-07: Investor Data Aggregator

**Trigger:** Daily schedule and on-demand

**Process:** AI aggregates investor data from multiple sources into unified view. Reconciles across sources. Maintains historical record. Generates investor-specific statements → Push into a centralized dashboard

**Output:** Consolidated investor data containing: (1) Current balances by fund/share class, (2) Transaction history, (3) Private investment allocations, (4) Co-investment positions, (5) Investor-specific reports on demand

**T-shirt size:**

**Questions:**

---

## Corporate Access

### CA-01: Event Identifier and Tracker

**Trigger:** Email received in Corporate Access inbox or (ideally) from company websites / sell-side

**Process:** AI parses corporate access emails for event details: company, date, location, format, bank/sponsor. Extracts key information. Creates structured event record. Identifies relevant coverage analysts.

**Output:** Event record containing: (1) Structured event details, (2) Coverage analyst match, (3) Relevance score based on portfolio/coverage, (4) Calendar invitation draft, (5) Conflict check against existing calendar

**T-shirt size:**

**Questions:**

---

### CA-02: Calendar Sync and Routing / Tracker

**Trigger:** New event identified or analyst RSVP

**Process:** AI routes events to appropriate analyst calendars based on coverage. Integrates with catalyst calendar for context. Manages conflicts and suggests alternatives. Tracks RSVPs and attendance.

**Output:** Calendar events properly routed with: (1) Event on correct analyst calendar, (2) Catalyst context included, (3) RSVP tracking

**T-shirt size:**

**Questions:**

---

### CA-03: Corporate Access Forecaster

**Trigger:** Quarterly planning cycle or on-demand

**Process:** AI analyzes historical patterns to forecast upcoming corporate access opportunities. Predicts: recurring conferences, typical company event timing, bank NDR patterns. Enables proactive planning + flags relevancy for any new events that come up

**Output:** Forward calendar containing: (1) Predicted events by company, (2) Confidence levels based on historical consistency, (3) Suggested RSVP timing, (4) Gaps in coverage access, (5) Broker relationship opportunities

**T-shirt size:**

**Questions:**

---

### CA-04: Broker Utilization Analyzer

**Trigger:** Monthly/quarterly schedule

**Process:** AI correlates broker spend with value received. Analyzes: commission vs. corporate access quality, research consumption by broker, event allocation vs. request, relationship ROI.

**Output:** Broker scorecard containing: (1) Commission spend by broker, (2) Corporate access events attended, (3) Research consumption metrics, (4) Event fill rate (requested vs. allocated), (5) ROI ranking, (6) Negotiation recommendations

**T-shirt size:**

**Questions:**

---

### CA-05: Corporate Access Reporting

**Trigger:** Monthly schedule and on-demand

**Process:** AI generates corporate access analytics. Tracks: event attendance rates, allocation success rates, coverage gaps, broker performance.

**Output:** Corporate access report containing: (1) Events attended by analyst/sector, (2) Allocation rates by bank, (3) Coverage gaps (companies without recent access), (4) Utilization trends, (5) Planning recommendations

**T-shirt size:**

**Questions:**

---

## Administrative & Cross-Functional

### AD-01: Meeting Prep Automator

**Trigger:** Meeting scheduled (detected via calendar, 5 days ahead)

**Process:** AI generates meeting preparation document. Compiles: participant backgrounds, prior interactions, relevant recent news, suggested talking points, open items from prior meetings

**Output:** Meeting brief containing: (1) Participant bios with recent activity, (2) Prior meeting history and notes, (3) Open items from last interaction, (4) Relevant recent news about participants/their company, (5) Suggested agenda or talking points

**T-shirt size:**

**Questions:**

---

### AD-02: Enterprise Search and Retrieval Bot

**Trigger:** Natural language query via Slack (e.g., Find the latest model for RDDT)

**Process:** AI interprets natural language query and searches document repository. Uses semantic search to find relevant documents even with imprecise queries. Returns ranked results with previews.

**Output:** Search results containing: (1) Ranked document list with relevance scores, (2) Preview snippets showing relevant content, (3) Direct links to documents, (4) Related documents that may be relevant

**T-shirt size:**

**Questions:**

---

### AD-03: Document Tagger and Organizer

**Trigger:** New document uploaded to Egnyte or scheduled batch processing

**Process:** AI analyzes document content and classifies by type, topic, related entities (companies, deals, investors). Suggests folder location. Applies standard metadata tags. Identifies duplicates.

**Output:** Document organization actions: (1) Suggested classification and tags, (2) Recommended folder location, (3) Duplicate detection alerts, (4) Metadata populated, (5) Related documents linked

**T-shirt size:**

**Questions:**

---

### AD-04: Executive Dashboard / Knowledge Bot

**Trigger:** Web interface

**Process:** AI provides unified interface for executive queries across all domains. Interprets natural language questions. Routes to appropriate data sources. Synthesizes cross-functional answers.

**Output:** Tabs for Portfolio Analytics, Fund Performance, Investor Relations, Private Investments, etc. ChatBot direct answers to questions like: (1) "What's our exposure to AI?" (2) "How did we perform vs. benchmark this month?" (3) "Which LPs have redemption notices pending?" (4) "What's the latest on the Grok investment?" Includes supporting data and drill-down links.

**T-shirt size:**

**Questions:**

---

### AD-05: Relationship Mapper

**Trigger:** On-demand query (e.g., "Who at XN knows someone at Tesla?")

**Process:** AI builds and maintains relationship graph based on communication patterns. Tracks: who knows whom, recency of contact, relationship strength, mutual connections. Answers relationship queries.

**Output:** Relationship insights containing: (1) XN contacts with relationships to target, (2) Recency and frequency of interaction, (3) Relationship strength score, (4) Mutual connections, (5) Suggested introduction path, (6) Last interaction summary

**T-shirt size:**

**Questions:**

---
