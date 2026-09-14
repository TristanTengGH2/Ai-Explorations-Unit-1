# Research

> EDITING DIRECTIVE: USER AND AGENT EDIT THIS FILE COLLABORATIVELY. THE USER MUST REVIEW AND APPROVE ITS CONTENT.

Purpose of this file: Develop and record the evidence and decisions that will guide the technical specification.

## Instructions for the user

You are responsible for the ethics, accuracy, and fairness of the research. Direct the inquiry toward useful questions, judge sources and suggestions rather than accepting them at face value, and approve only results supported by verified evidence and audience needs. Seek evidence that challenges your assumptions, represent uncertainty honestly, and reject claims you cannot verify. See [UNESCO's Guidance for generative AI in education and research](https://www.unesco.org/en/articles/guidance-generative-ai-education-and-research).

## Instructions for the agent

Read AGENTS.md, brief.md, and this file. Begin with a concise orientation and one focused question.

Guide the research one stage at a time. Help the user explore options, assess sources, and identify contrary evidence or uncertainty without making decisions for them. Draft concise updates for review, and never mark research or feature choices approved on the user's behalf.

## Reference employee profiles

- Alex — Los Angeles, 24, junior video editor: Uses text, image, and video-generation tools for production work. Streams reference media and uses social platforms across a phone, laptop, and television. Wants to understand impacts beyond text prompts and is particularly attentive to water use.
- Jordan — Austin, 38, creative technologist: Uses coding agents and generative tools in long, irregular sessions. Games on a desktop PC and participates in frequent video calls. Finds "prompts per day" too simplistic and wants assumptions, ranges, and project-level totals.
- Robin — Chicago, 56, operations manager: Uses text AI occasionally but spends substantial time in video meetings, streaming media, and social platforms. Is skeptical of the company's motives and needs plain-language explanations, visible sources, and honest indications of uncertainty.

These are fictional starting profiles, not evidence about demographic groups. Research the activities, circumstances, and needs they represent rather than making assumptions based on age or location.

## Audience needs

Record information about the activities, circumstances, and needs represented by all three reference profiles. Separate evidence from assumptions that still need checking.

### Investigation draft — 2026-09-14 — awaiting user review

Goal: assess the five user-authorized candidates against the brief, available evidence, and the existing calculator. Done for this stage means identifying useful calculation changes, credible sources, limitations, and decisions still needed. This is a feasibility investigation, not an approved specification or a finalized coefficient dataset.

The profiles establish design needs, not observed employee behavior. No interviews or usability studies have been conducted.

| Profile | Need stated in the profile | Proposed response | Assumption to check with employees |
|---|---|---|---|
| Alex | Media generation, multiple viewing devices, water concerns | Separate AI media inputs, device-aware streaming, explicit water coverage | Whether generation counts, clip settings, and device hours are practical inputs |
| Jordan | Irregular coding work, project totals, visible assumptions | Project activity totals and adjustable calculation scenarios; meeting inputs | Whether token or request records are available for coding projects |
| Robin | Frequent meetings and streaming; limited AI use; skepticism | Useful digital totals even with zero AI, plain-language source and uncertainty explanations | Whether explanations make estimates understandable and trustworthy |

Balanced coverage means each profile has useful inputs and interpretable results. It does not require assuming equal usage or assigning habits based on age or city.

### Existing calculator findings

Direct inspection of `ai-footprint-calculator.html` found carbon and water outputs, low/high estimates, a coding/agent preset, daily totals, and annualization. Therefore merely adding ranges, water, or a coding label would not constitute a new feature.

The existing carbon calculation uses the employee's selected location for AI electricity. Proposed correction for review: distinguish a user's device location from the assumed remote data-center location; do not imply the latter is known. Existing source claims and confidence-interval wording still need a separate numerical audit before reuse.

## Possible features

Generate several possibilities before choosing. Keep the initial notes brief. For each idea, record:

- what it would help someone learn or do
- the profiles or needs it would serve
- any evidence or implementation challenge that might affect it

## Source assessments

### Investigated sources

All links below were accessed on 2026-09-14. Decisions are agent recommendations pending user review. Confidence refers to the stated use, not universal accuracy.

**S1 — Luccioni, Alexandra Sasha; Jernite, Yacine; Strubell, Emma (2024). “Power Hungry Processing: Watts Driving the Cost of AI Deployment?” ACM FAccT. [Paper record and abstract](https://arxiv.org/abs/2311.16863).**

- Checked directly: abstract describes measurements for 1,000 inferences across task categories and differences between task-specific and general-purpose models.
- Proposed use: evidence for distinguishing activities rather than using one universal prompt factor.
- Limitations: benchmark conditions do not establish current commercial-service consumption. Full numerical tables have not been verified in this pass; no image coefficient is adopted.
- Confidence/decision: medium; use with qualifications for feature rationale, not production defaults yet.

**S2 — EcoLogits contributors (undated, live documentation). [Methodology](https://ecologits.ai/latest/methodology/).**

- Checked directly: scope and limitations; currently documents LLM inference and video generation, while image generation is listed as upcoming. Excludes training, networking, and end-user devices; includes modeled hardware impacts and water from data centers and electricity generation.
- Proposed use: compatible starting point for extending the existing estimator and explaining missing components.
- Limitations: estimates depend on assumptions about undisclosed systems; live documentation must be pinned to a version before implementation. It does not substantiate a complete digital-life footprint.
- Confidence/decision: medium; use with qualifications. Image generation needs another source.

**S3 — EcoLogits contributors (undated, live documentation). [Environmental Impacts of Video Generation](https://ecologits.ai/latest/methodology/video_generation/).**

- Checked directly: equations use model-specific latency estimates, video dimensions/frame count, hardware power, data-center overhead, electricity factors, and hardware allocation. The documentation assigns whole-machine power to a request without a batch-allocation term.
- Proposed use: video estimates based on supported models and clip settings rather than one generic “video prompt.”
- Limitations: modeled hardware and latency are not direct measurements of a user's job; whole-machine allocation can affect comparability with shared production serving. Verify supported settings and the underlying study before selecting coefficients.
- Confidence/decision: medium; use with qualifications as a candidate method.

**S4 — Carbon Trust, commissioned by DIMPACT (2026). [The carbon impact of AI video generation](https://www.carbontrust.com/our-work-and-impact/guides-reports-and-tools/the-carbon-impact-of-ai-video-generation).**

- Checked directly: publisher overview; report PDF also accessible. Overview identifies inconsistent disclosures and the importance of repeated generations in professional workflows.
- Proposed use: support counting attempts across a project, not only accepted outputs.
- Limitations: media-industry commissioned research; the report's numerical estimates have not been audited here. No universal per-video factor is adopted.
- Confidence/decision: medium; use with qualifications for workflow rationale.

**S5 — Elsworth, Cooper, et al. (2025). [Measuring the environmental impact of delivering AI at Google Scale](https://arxiv.org/html/2508.15734v1). arXiv:2508.15734v1.**

- Checked directly: sections 3–4 and Table 1. Reports 0.24 Wh for the median Gemini Apps text prompt in May 2025, including serving-system overhead. Excludes user devices, external networking, and training. Water accounting concerns data-center cooling; emissions use market-based accounting.
- Proposed use: contrary evidence against transferring older benchmark estimates universally; demonstrate why measurement boundaries matter.
- Limitations: provider-authored, product/date-specific, and a median rather than a workload mean. Multiplying this median by requests would be an illustrative scenario, not a measured project total. Cooling-only water cannot substitute for cooling-plus-electricity water.
- Confidence/decision: medium; use with qualifications as a cross-check, not a universal default.

**S6 — Carbon Trust (June 2021). [Carbon impact of video streaming](https://www.carbontrust.com/our-work-and-impact/guides-reports-and-tools/carbon-impact-of-video-streaming).**

- Checked directly: publisher summary reports approximately 55 g CO2e per viewing hour in Europe, identifies the viewing device as a major contributor, and finds small emissions effects from resolution changes under its model.
- Proposed use: support hours plus viewing-device inputs; historical benchmark for validation.
- Limitations: older European estimate, not a current US default. Netflix funded the study, developed with DIMPACT consultation. Component values and boundaries require PDF-level checking before reuse.
- Confidence/decision: medium; use with qualifications; do not adopt 55 g/hour universally.

**S7 — Obringer, Renee; Rachunok, Benjamin; Maia-Silva, Debora; Arbabzadeh, Maryam; Nateghi, Roshanak; Madani, Kaveh (2021). “The overlooked environmental footprint of increasing Internet use.” Resources, Conservation & Recycling 167, 105389. [Author-hosted paper](https://www.kavehmadani.com/_files/ugd/34bbdd_53607307c30b4599b6d0315b4e302033.pdf?index=true), [DOI](https://doi.org/10.1016/j.resconrec.2020.105389).**

- Checked directly: pages 1 and 3 describe a proxy method for fixed-line data storage/transmission and a videoconferencing example of 157 g CO2e/hour using 2.5 GB/hour.
- Proposed use: historical comparison and evidence of methodological uncertainty.
- Limitations: not a measured current meeting-service footprint; supplementary assumptions have not been checked. Its data-volume approach differs from S6, including much larger claimed resolution-related savings. These are not interchangeable endpoints of a confidence interval.
- Confidence/decision: low for current coefficients; reject as the default meeting factor, retain as contrary evidence. Do not promise a fixed percentage saving from camera-off use.

### Calculation implications — proposed, not approved

- Keep electricity, carbon emissions, and water as separate quantities. Sum like units over the same reporting period.
- A project estimate can sum activity quantities times compatible per-unit factors. Count retries and discarded outputs; do not convert elapsed coding hours into tokens without evidence.
- Streaming and meeting totals can use hours times a supported hourly factor. Distinguish personal participation from whole-meeting totals and avoid counting the same device energy twice during overlapping activities.
- Explain what each estimate includes: servers, networks, devices, manufacturing, and training. Do not present incompatible scopes as a fair ranking.
- Adjustable scenarios must change the calculation. Low/high scenarios are not automatically statistical confidence intervals; adding source endpoints does not establish a combined 95% interval.
- Water remains an audience need. Missing water estimates must read “not estimated,” not zero. An employee's city does not identify the cooling location for a cloud request.
- Avoid adding digital-use estimates onto a broad personal baseline if that would count the same electricity twice.

For each source, record:

- the full citation and working link
- the claim or figure the project may use
- evidence checked directly
- important limitations or uncertainty
- confidence and decision: use, use with qualifications, or reject

## Selected features

### Recommended candidates after investigation — NOT APPROVED

| Candidate | New contribution to calculation | Balanced audience value | Feasibility finding |
|---|---|---|---|
| 1. AI activity breakdown | Separate text, image, and video quantities and supported factors | Alex's media work; Jordan's mixed workflows; clear categories for Robin | Supported in principle by S1–S4; image defaults still need verification |
| 2. Project-level AI totals | Aggregate actual project activities and repeated attempts over a chosen project period | Jordan's irregular work; Alex's production iterations; accessible totals for Robin | Feasible accounting feature; existing coding preset alone is insufficient |
| 3. Streaming comparison | User-entered viewing hours and device affect the digital total | Directly addresses Alex and Robin; provides optional context for Jordan | S6 supports approach; current device/component factors unresolved |
| 4. Video-meeting comparison | Personal meeting hours contribute to the same-period digital total | Directly addresses Robin and Jordan; useful workplace context for Alex | Weakest numerical basis in this pass; current factor and scope unresolved |
| 5. Adjustable assumptions and estimate ranges | Recalculate totals under visible, supported assumptions and show sensitivity | Jordan can inspect assumptions; Robin can judge uncertainty; Alex can inspect media/water limitations | Feasible; must go beyond existing range display and avoid arbitrary bounds |

This set satisfies the brief's category distribution in concept. It does not yet have enough verified coefficients for implementation approval.

Alternatives deferred for review: gaming would deepen Jordan's coverage but replace a shared workplace activity; social-media estimates would help Alex and Robin but require defining mixed browsing/video behavior; a standalone water toggle would duplicate existing functionality. These are proposed trade-offs, not user-approved rejections.

### Next research decisions

1. User authorized deeper investigation of operational electricity across servers, networks, and devices, with manufacturing and training assessed separately. This authorizes research, not final calculation defaults.
2. Verify image-generation benchmarks and current streaming/meeting component factors before accepting defaults.
3. Pin model/data versions and record units, geography, measurement period, scope, and uncertainty for each chosen factor.
4. Review all three profile journeys equally, including a zero-AI case and missing water data.

User approval status: investigation authorized; research contents and feature selections awaiting review. Do not begin the technical specification yet.

List the five selected features. Briefly explain why each was selected and how the set serves all three reference profiles. Name a few serious alternatives and explain why they were rejected.

User approval: Review the completed research directly. Confirm that sources exist and support the claims the project will use, correct the document as needed, and explicitly approve the selected features before developing the specification. The agent cannot complete this approval on the user's behalf.

## Deeper investigation — component scope and calculation evidence

Draft for review, 2026-09-14. This section updates the initial feasibility findings above. Broader scope improves completeness; it does not remove uncertainty in the inputs.

### Recommended accounting structure

Use one common operational boundary for comparisons: remote servers and cooling, network transmission, home/office router allocation, and user devices. Show the components separately so missing evidence is visible. Report an incomplete estimate as a **subtotal of estimated components**, not a complete footprint.

| Component | AI work | Streaming | Meetings | What must be established |
|---|---|---|---|---|
| Remote servers | Inference requests, including repeated attempts | Hosting and content delivery | Meeting processing/relay | Activity-specific factor; whether cooling is included |
| Networks | Prompt uploads and generated downloads | Delivered media data | Upload and download traffic | Access type and allocation method; avoid reusing server energy here |
| Router | Allocated share of router operation | Same | Same | Shared usage and overlapping hours |
| User devices | Actual active device time | Viewing time and device | Participation time and device | Average operating power; monitor/peripheral inclusion |
| Manufacturing | Separate allocated hardware emissions | Separate allocated hardware emissions | Separate allocated hardware emissions | Hardware lifetime and allocation denominator |
| Training/content production | Separate where supportable | Original production excluded from delivery estimate | No generic equivalent | Do not add a guessed training percentage or equate different creation processes |

This structure is a proposed synthesis of the checked methods, not a claim that every component already has a reliable coefficient.

### Additional source checks and candidate factors

**S1 follow-up — full [Luccioni et al. PDF](https://arxiv.org/pdf/2311.16863), Table 2, PDF page 6.** The table reports image-generation mean electricity of 2.907 kWh per 1,000 queries, with standard deviation 3.31 kWh. Unit conversion gives **2.907 Wh per image**. This is a historical benchmark across the tested models, not a current commercial-model default. The standard deviation is not a user-level confidence interval; mean minus standard deviation would even be negative. Recommendation: qualified educational benchmark only; inspect per-model configurations before implementing model-specific image estimates. This supersedes the earlier note that no numerical table had been checked.

**S6 follow-up — [Carbon Trust full streaming report](https://www.carbontrust.com/sites/default/files/documents/resource/public/Carbon-impact-of-video-streaming.pdf), Tables 3, 5, and 10, printed pages 43, 62, and 101.** Verified historical candidate inputs: data centers/content delivery **1.3 Wh per viewing hour**; conventional fixed network **0.0065 kWh/GB**; laptop **22 W**; desktop including monitor **115 W**; TV **100 W**. These are 2020-era model assumptions, not current measurements of employees' equipment. Its alternative power model separates network baseline from traffic-dependent consumption. Recommendation: use the component structure; retain these values only as explicitly dated scenarios until replaced or accepted with qualifications. Do not blend the conventional and power-model network factors in one result.

**S8 — Zoom (undated, live documentation). [Zoom system requirements: Zoom Web App](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0058323).** Checked directly: recommended group-call bandwidth includes 2.6 Mbps upload and 1.8 Mbps download for 720p; the service adapts bandwidth. Proposed use: a documented bandwidth scenario. These are connectivity recommendations, not measured traffic or energy consumption. Confidence: high about the published recommendation, low as an average-use proxy. Decision: use with qualifications; do not infer meeting-server energy from it.

**S9 — US Environmental Protection Agency (2025, revision 2 June 12). [eGRID2023 Summary Data](https://www.epa.gov/egrid/summary-data).** Checked directly: CO2e output rates are listed in lb/MWh; the US rate is 770.884. Conversion gives approximately **349.67 g CO2e/kWh**. Proposed use: a dated US electricity-generation scenario, with subregion factors when location is known. Limitations: annual generation-average accounting, not hourly marginal emissions or a full electricity lifecycle factor. Transmission losses require separate treatment if estimating delivered electricity. Confidence: high for table values; medium for applying them to a workload. Decision: use with qualifications; distinguish local devices from remote infrastructure.

**S10 — Google research team (2025). [Life-Cycle Emissions of AI Hardware: A Cradle-To-Grave Approach and Generational Trends](https://arxiv.org/abs/2502.01671), arXiv:2502.01671.** Checked directly: abstract establishes a hardware lifecycle assessment including accelerator manufacturing. Proposed use: evidence that manufacturing deserves separate accounting. Limitations: provider hardware study; numerical tables and allocation assumptions have not been audited here. Confidence: medium for this qualitative use. Decision: use with qualifications; no manufacturing coefficient adopted.

**Unresolved access leads:** The 2024 Nature Communications article [The environmental sustainability of digital content consumption](https://doi.org/10.1038/s41467-024-47621-w) could not be opened through either publisher URL or DOI; stopped after two failures. The [2024 LBNL data-center report](https://bies.lbl.gov/publications/2024-lbnl-data-center-energy-usage-report) PDF link redirected to a JavaScript/robot check. Search snippets are insufficient to approve coefficients. Both remain unverified leads; no numerical values from them are adopted.

### Calculation methods and worked checks

These are mathematical checks using candidate factors, not validated estimates of an employee's actual footprint.

1. **Device electricity:** `kWh = average watts × active hours / 1,000`. With S6's historical laptop assumption, two hours gives `22 × 2 / 1,000 = 0.044 kWh`. Prefer measured average power for the actual workload when available; a charger rating is not average consumption. A desktop factor that includes a monitor must not receive another monitor allowance.
2. **Electricity emissions:** sum `component kWh × component grid factor`. The laptop example with S9's US factor gives approximately `0.044 × 349.67 = 15.39 g CO2e` from electricity generation only. This excludes networks, servers, manufacturing, and other electricity lifecycle contributions.
3. **Meeting traffic scenario:** decimal `GB = (upload Mbps + download Mbps) × 0.45 × hours`. S8's 720p group-call recommendation implies `4.4 × 0.45 = 1.98 GB` over one hour if sustained continuously. This is a scenario, not observed traffic. It does not establish a full meeting footprint or justify multiplying by every participant.
4. **Project image scenario:** 20 generations at S1's benchmark mean gives `20 × 2.907 = 58.14 Wh`. Count discarded generations. Label model mismatch and excluded components rather than presenting this as a measurement.
5. **Remote cooling and water:** if IT electricity is known, facility electricity is `IT kWh × PUE`. On-site consumption is `IT kWh × on-site WUE` only when WUE uses that denominator; indirect water is `facility kWh × electricity water-consumption factor`. Do not apply PUE twice to a factor already covering facility electricity. S3 supplies this structure. Site-specific water coefficients remain unresolved.

### Why a single “accurate total” remains difficult

- **Allocated footprint versus avoided energy:** dividing shared infrastructure energy among activities is an accounting choice. Removing one activity need not save its allocated share immediately. Present scenario differences as differences in estimated allocation unless a causal savings method is supported.
- **Source disagreement:** retain separate named scenarios when studies use different boundaries. The lowest and highest published figures are not automatically uncertainty bounds for the same quantity.
- **Project records:** useful inputs include request counts, output sizes, generated media settings, and retries. Coding agents may perform hidden work; elapsed session hours alone do not identify remote computation. Record missing work as a limitation.
- **Water meaning:** consumption and withdrawal differ. Liters also do not communicate local scarcity by themselves. Never infer that water impact is small or large solely from a global-volume comparison.
- **Manufacturing/training:** report separately unless compatible allocations are available for every compared activity. Existing AI factors may already include manufacturing; adding it again would double-count. A defensible training share needs both model training impact and a justified lifetime allocation, currently unavailable here.

### Equal-profile walkthrough checks for later validation

| Profile | Proposed example to test | Evidence of success to seek |
|---|---|---|
| Alex | Image/video project with discarded attempts, plus streaming on two device types | Attempts affect totals; device differences are visible; missing water is explicitly labeled |
| Jordan | Irregular multi-day coding project with overlapping meetings | Project period is explicit; missing remote activity is disclosed; one physical device-hour is not counted twice |
| Robin | Zero AI, several meetings and streaming sessions | Digital subtotal remains useful; sources and exclusions are understandable; comparisons do not imply a required opinion about AI |

These are proposed usability checks, not observed results. Shared-device energy should be recorded once per time interval, then allocated across simultaneous activities if necessary. User-entered hours should not silently multiply shared router energy or imply unique devices.

### Updated recommendation and readiness

Keep the five candidates. The deeper investigation supports a component-based calculator and supplies dated candidate factors and reproducible arithmetic. It does **not** yet support an unqualified current total across all components.

- Ready for review: component scope, project accounting, scenario controls, historical image/streaming factors, and dated grid factors.
- Still unresolved: current model-specific image factors; verified video-model configuration data; meeting-server electricity; current network factors; component-specific water coefficients; consistent manufacturing and training allocation.
- Recommended handling: let supported components contribute to a clearly labeled subtotal; show omitted components alongside it. Do not manufacture values to fill gaps or report missing components as zero.

Research and feature approval remain pending. No implementation or specification changes made.

## Commands

### Start research

User: Open the project repository as your workspace, start a fresh chat, and type `start research`.

### Save transcript

Agent: After the user approves the selected features, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `research-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
