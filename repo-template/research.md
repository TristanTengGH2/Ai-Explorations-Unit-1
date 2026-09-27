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

**User decision — 2026-09-21: approved for background evidence only.** Supports the claim that energy consumption varies by task and model under the tested conditions. Numerical averages are not approved as calculator defaults because the tested models and workloads do not sufficiently represent the intended users. This decision supersedes earlier candidate-use recommendations for S1 below; numerical examples remain research notes, not approved calculation factors.

Review clarified that results are reported per 1,000 inference requests, not per token. Tests used sequential requests without batching; the multipurpose comparison used FLAN-T5 and BLOOMz. The separate text-generation benchmark generated 10 new tokens per input. Reported energy included idle power from the other GPUs on the test node. See the paper's methods and results, pages 4–6. The user considered author credibility and explicitly approved the limited background use after discussing these limitations.

- Checked directly: abstract describes measurements for 1,000 inferences across task categories and differences between task-specific and general-purpose models.
- Proposed use: evidence for distinguishing activities rather than using one universal prompt factor.
- Limitations: benchmark conditions do not establish current commercial-service consumption. Full numerical tables have not been verified in this pass; no image coefficient is adopted.
- Confidence/decision: medium; use with qualifications for feature rationale, not production defaults yet.

**S2 — EcoLogits contributors (undated, live documentation). [Methodology](https://ecologits.ai/latest/methodology/).**

**User decision — 2026-09-21: approved with qualifications for specific supported text-model inference estimates.** Disclose model-specific assumptions, modeled rather than measured consumption, and excluded components. This is not blanket approval of every model coefficient or a complete footprint. Pin the software/data version and check the selected model configurations before implementation. Video methodology remains under the separate S3 review; image generation requires another source.

The user accepted limited use following discussion of the methodology and the existing calculator's reliance on EcoLogits. Existing use establishes provenance, not independent verification of every estimate.

- Checked directly: scope and limitations; currently documents LLM inference and video generation, while image generation is listed as upcoming. Excludes training, networking, and end-user devices; includes modeled hardware impacts and water from data centers and electricity generation.
- Proposed use: compatible starting point for extending the existing estimator and explaining missing components.
- Limitations: estimates depend on assumptions about undisclosed systems; live documentation must be pinned to a version before implementation. It does not substantiate a complete digital-life footprint.
- Confidence/decision: medium; use with qualifications. Image generation needs another source.

**S3 — EcoLogits contributors (undated, live documentation). [Environmental Impacts of Video Generation](https://ecologits.ai/latest/methodology/video_generation/).**

**Validity audit — 2026-09-21: credible modeled method; numerical use remains conditional.** The linked underlying work, Jegham, Gamazaychikov, and Luccioni's 2026 preprint *Lights, Camera, Carbon*, directly measured GPU energy for open video models across three GPU configurations and varied frames, steps, resolution, batch size, and audio. EcoLogits extends that work to server power, cooling, water, and embodied impacts. The underlying paper is a preprint rather than a peer-reviewed publication; it measures GPU energy only. Estimates for proprietary services infer energy from API generation time and assumed hardware/power, which the authors say cannot be directly verified. Use only for supported model-and-setting scenarios, pin the EcoLogits version, and show the resulting interval and exclusions. Do not treat it as a measured value for every commercial video tool.

- Checked directly: equations use model-specific latency estimates, video dimensions/frame count, hardware power, data-center overhead, electricity factors, and hardware allocation. The documentation assigns whole-machine power to a request without a batch-allocation term.
- Proposed use: video estimates based on supported models and clip settings rather than one generic “video prompt.”
- Limitations: modeled hardware and latency are not direct measurements of a user's job; whole-machine allocation can affect comparability with shared production serving. Verify supported settings and the underlying study before selecting coefficients.
- Confidence/decision: medium; use with qualifications as a candidate method.

**S4 — Carbon Trust, commissioned by DIMPACT (2026). [The carbon impact of AI video generation](https://www.carbontrust.com/our-work-and-impact/guides-reports-and-tools/the-carbon-impact-of-ai-video-generation).**

**User decision — 2026-09-21: approved with qualifications for background and project-accounting evidence.** Use it to support counting repeated generations and discarded attempts and to explain that video settings affect impact. Do not use its figures as a universal per-video factor; any numerical use must retain the cited model, resolution, duration, frame rate, grid, lifecycle boundary, and training-allocation assumptions.

The user approved this limited use after reviewing concerns about the publisher's presentation, investigating the authors and expert reviewers, and tracing the report's estimates. The report identifies its project team, discloses DIMPACT funding, and documents review by relevant academic and industry specialists. Its numerical analysis has a stated basis but combines modeled inference, measured case-study workstation electricity, and assumed training allocations; it is not journal peer review or direct measurement of every commercial service.

- Checked directly: publisher overview; report PDF also accessible. Overview identifies inconsistent disclosures and the importance of repeated generations in professional workflows.
- Proposed use: support counting attempts across a project, not only accepted outputs.
- Limitations: media-industry commissioned research; the report's numerical estimates have not been audited here. No universal per-video factor is adopted.
- Confidence/decision: medium; use with qualifications for workflow rationale.

**S5 — Elsworth, Cooper, et al. (2025). [Measuring the environmental impact of delivering AI at Google Scale](https://arxiv.org/html/2508.15734v1). arXiv:2508.15734v1.**

**Validity audit — 2026-09-21: valid first-party product measurement and useful cross-check; not an independent universal factor.** The authors document direct production-fleet telemetry covering accelerators, host CPU/DRAM, idle capacity, and data-center overhead. The paper is a Google-authored arXiv preprint, and outsiders cannot reproduce the proprietary fleet data. The 0.24 Wh result is the daily median Gemini Apps text prompt in May 2025, not a mean, token-normalized value, or result for other models and dates. Use to demonstrate production efficiency and boundary differences; do not multiply it into a general employee-project estimate.

- Checked directly: sections 3–4 and Table 1. Reports 0.24 Wh for the median Gemini Apps text prompt in May 2025, including serving-system overhead. Excludes user devices, external networking, and training. Water accounting concerns data-center cooling; emissions use market-based accounting.
- Proposed use: contrary evidence against transferring older benchmark estimates universally; demonstrate why measurement boundaries matter.
- Limitations: provider-authored, product/date-specific, and a median rather than a workload mean. Multiplying this median by requests would be an illustrative scenario, not a measured project total. Cooling-only water cannot substitute for cooling-plus-electricity water.
- Confidence/decision: medium; use with qualifications as a cross-check, not a universal default.

**S6 — Carbon Trust (June 2021). [Carbon impact of video streaming](https://www.carbontrust.com/our-work-and-impact/guides-reports-and-tools/carbon-impact-of-video-streaming).**

**Validity audit — 2026-09-21: sound historical industry white paper for structure and dated scenarios.** The full report names its analysts, documents equations, factors, boundaries, and two alternative network-allocation methods, and includes consultation from the IEA, LBNL, University of Bristol, industry researchers, and media companies. Netflix provided seed funding; the Carbon Trust states that it retained editorial control. It is not a peer-reviewed journal article. Its 55 gCO2e/hour result represents European 2020 on-demand viewing with a representative device mix and operational electricity only. Use its component structure and explicitly dated device scenarios; do not use 55 g/hour as a current or universal default.

- Checked directly: publisher summary reports approximately 55 g CO2e per viewing hour in Europe, identifies the viewing device as a major contributor, and finds small emissions effects from resolution changes under its model.
- Proposed use: support hours plus viewing-device inputs; historical benchmark for validation.
- Limitations: older European estimate, not a current US default. Netflix funded the study, developed with DIMPACT consultation. Component values and boundaries require PDF-level checking before reuse.
- Confidence/decision: medium; use with qualifications; do not adopt 55 g/hour universally.

**S7 — Obringer, Renee; Rachunok, Benjamin; Maia-Silva, Debora; Arbabzadeh, Maryam; Nateghi, Roshanak; Madani, Kaveh (2021). “The overlooked environmental footprint of increasing Internet use.” Resources, Conservation & Recycling 167, 105389. [Author-hosted paper](https://www.kavehmadani.com/_files/ugd/34bbdd_53607307c30b4599b6d0315b4e302033.pdf?index=true), [DOI](https://doi.org/10.1016/j.resconrec.2020.105389).**

**Validity audit — 2026-09-21: legitimate published perspective, unsuitable for calculator coefficients.** The paper identifies academic affiliations, a journal DOI, received/revised/accepted dates, and openly describes its method as a rough estimate using proxy variables. Its meeting and streaming results scale impact linearly with data volume. That allocation does not represent the largely fixed short-term power of shared networks and conflicts with the more careful distinction between average and marginal allocation documented in S6. Retain only as historical evidence of disagreement and the risks of proxy methods; reject its 157 gCO2e/hour meeting value and camera-off savings as defaults.

- Checked directly: pages 1 and 3 describe a proxy method for fixed-line data storage/transmission and a videoconferencing example of 157 g CO2e/hour using 2.5 GB/hour.
- Proposed use: historical comparison and evidence of methodological uncertainty.
- Limitations: not a measured current meeting-service footprint; supplementary assumptions have not been checked. Its data-volume approach differs from S6, including much larger claimed resolution-related savings. These are not interchangeable endpoints of a confidence interval.
- Confidence/decision: low for current coefficients; reject as the default meeting factor, retain as contrary evidence. Do not promise a fixed percentage saving from camera-off use.

**User source decision — 2026-09-21: approved the remaining sources based on publisher and website credibility, subject to the documented limitations.** Sources 3, 5, 6, and 9–12 may support only the claims and scopes recorded in their audits. Source 7 may provide historical context but none of its numerical proxies may contribute to a complete estimate. Source 8 may provide a labeled Zoom bandwidth scenario, but that scenario may not be converted into or included in a complete meeting-footprint estimate. Missing meeting components must remain visibly “Not Estimated.” This approval covers source use; it does not approve the proposed features or final calculator factors.

### Calculation implications — proposed, not approved

- Keep electricity, carbon emissions, and water as separate quantities. Sum like units over the same reporting period.
- A project estimate can sum activity quantities times compatible per-unit factors. Count retries and discarded outputs; do not convert elapsed coding hours into tokens without evidence.
- Streaming and meeting totals can use hours times a supported hourly factor. Distinguish personal participation from whole-meeting totals and avoid counting the same device energy twice during overlapping activities.
- Do not use Source 7's proxy coefficients or Source 8's recommended bandwidth to claim a complete meeting estimate. Until stronger component evidence is selected, show supported device or traffic scenarios separately and label the unresolved remainder “Not Estimated.”
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

### Approved features

**User decision — 2026-09-24: approved all five features.** Approval includes the safeguards established during review: unsupported meeting components display “Not Estimated”; coding-agent use is based on actual available activity records rather than inferred from session duration; water gaps remain visible; assumptions, sources, boundaries, dates, and exclusions accompany adjustable scenarios; and employee location applies only to known local electricity use, not an assumed cloud data-center location.

| Candidate | New contribution to calculation | Balanced audience value | Feasibility finding |
|---|---|---|---|
| 1. AI activity breakdown | Separate text, image, and video quantities and supported factors | Alex's media work; Jordan's mixed workflows; clear categories for Robin | Supported in principle by S1–S4; image defaults still need verification |
| 2. Project-level AI totals | Aggregate actual project activities and repeated attempts over a chosen project period | Jordan's irregular work; Alex's production iterations; accessible totals for Robin | Feasible accounting feature; existing coding preset alone is insufficient |
| 3. Streaming comparison | User-entered viewing hours and device affect the digital total | Directly addresses Alex and Robin; provides optional context for Jordan | S6 supports approach; current device/component factors unresolved |
| 4. Video-meeting comparison | Personal meeting hours contribute to the same-period digital total | Directly addresses Robin and Jordan; useful workplace context for Alex | Weakest numerical basis in this pass; current factor and scope unresolved |
| 5. Adjustable assumptions and estimate ranges | Recalculate totals under visible, supported assumptions and show sensitivity | Jordan can inspect assumptions; Robin can judge uncertainty; Alex can inspect media/water limitations | Feasible; must go beyond existing range display and avoid arbitrary bounds |

This set satisfies the brief's category distribution: features 1 and 2 improve professional-AI accounting, features 3 and 4 connect it with broader digital activity, and feature 5 addresses the strongest remaining need for transparent uncertainty and assumptions. The specification must select only supported factors and preserve incomplete results as labeled subtotals.

Alternatives excluded from this project: gaming would deepen Jordan's coverage but replace a shared workplace activity; social-media estimates would help Alex and Robin but require defining mixed browsing/video behavior; detailed hardware-manufacturing calculations lack compatible allocation factors; and a standalone water toggle would duplicate existing functionality.

### Next research decisions

1. User authorized deeper investigation of operational electricity across servers, networks, and devices, with manufacturing and training assessed separately. This authorizes research, not final calculation defaults.
2. Verify image-generation benchmarks and current streaming/meeting component factors before accepting defaults.
3. Pin model/data versions and record units, geography, measurement period, scope, and uncertainty for each chosen factor.
4. Review all three profile journeys equally, including a zero-AI case and missing water data.

User approval status: source validity, limited source uses, and the five-feature selection are approved. The specification must turn the approved safeguards into testable requirements and select numerical defaults only within their supported scopes.

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

**Validity audit — 2026-09-21: authoritative for Zoom's stated connection requirements only.** It is first-party product documentation and explicitly says bandwidth adapts to the participant's network. It does not report actual average data transfer, server electricity, network electricity, carbon, or water. Use only to construct a labeled maximum/recommended-bandwidth scenario if needed. It cannot validate the meeting-footprint feature by itself.

**S9 — US Environmental Protection Agency (2025, revision 2 June 12). [eGRID2023 Summary Data](https://www.epa.gov/egrid/summary-data).** Checked directly: CO2e output rates are listed in lb/MWh; the US rate is 770.884. Conversion gives approximately **349.67 g CO2e/kWh**. Proposed use: a dated US electricity-generation scenario, with subregion factors when location is known. Limitations: annual generation-average accounting, not hourly marginal emissions or a full electricity lifecycle factor. Transmission losses require separate treatment if estimating delivered electricity. Confidence: high for table values; medium for applying them to a workload. Decision: use with qualifications; distinguish local devices from remote infrastructure.

**Validity audit — 2026-09-21: authoritative and arithmetic verified for the stated scope.** EPA describes eGRID as covering nearly all US grid-connected electricity generation and publishes its technical resources. The official site still identifies revised eGRID2023 as the current release. The conversion is correct: `770.884 lb/MWh × 453.59237 g/lb ÷ 1,000 kWh/MWh = 349.667 gCO2e/kWh`. Use the appropriate eGRID subregion for known US device electricity; use the US average only as a labeled fallback. Do not apply a user's eGRID region to an unknown remote data center or describe this combustion/output rate as full lifecycle carbon.

**S10 — Google research team (2025). [Life-Cycle Emissions of AI Hardware: A Cradle-To-Grave Approach and Generational Trends](https://arxiv.org/abs/2502.01671), arXiv:2502.01671.** Checked directly: abstract establishes a hardware lifecycle assessment including accelerator manufacturing. Proposed use: evidence that manufacturing deserves separate accounting. Limitations: provider hardware study; numerical tables and allocation assumptions have not been audited here. Confidence: medium for this qualitative use. Decision: use with qualifications; no manufacturing coefficient adopted.

**Validity audit — 2026-09-21: credible first-party hardware LCA for Google TPUs; limited external verification.** The Google-authored arXiv preprint documents an ISO 14040/14044-aligned assessment, a six-year assumed machine life, first-party manufacturing inputs, and measured operational data across Google's TPU fleet. It excludes rack, network, and auxiliary storage/compute components, and some proprietary manufacturing inputs are used internally without disclosure. Use to establish that embodied hardware emissions exist and require lifecycle allocation. Do not transfer its TPU coefficients to GPU servers or add a per-request manufacturing factor without a compatible utilization/lifetime allocation.

**S11 — Istrate, Robert, et al. (2024). [“The environmental sustainability of digital content consumption.”](https://doi.org/10.1038/s41467-024-47621-w) Nature Communications 15, 3724.** Access issue resolved on 2026-09-21. The article is peer reviewed, names reviewers, follows ISO 14040/14044 lifecycle assessment, and publishes data and code. It models a global-average annual user across web, social media, streaming, music, and video conferencing, including data centers, networks, customer-premises equipment, devices, and embodied impacts. Its user archetype and some load-proportional network assumptions are modeled averages rather than measurements of our employees. Decision: use with qualifications for comprehensive boundary design and sensitivity checks; do not copy its global-average behavior or convert its annual total into a universal hourly meeting factor.

**S12 — Shehabi, Arman, et al. (2024). [2024 United States Data Center Energy Usage Report](https://datacenters.lbl.gov/publications/2024-lbnl-data-center-energy-usage-report). Lawrence Berkeley National Laboratory, DOI 10.71468/P1WC7Q.** Access issue resolved on 2026-09-21. This is an official laboratory report prepared in response to the US Energy Act of 2020, with named authors, DOI, historical modeling, and forecast scenarios. A June 2026 LBNL update now supersedes its national electricity forecasts. These reports describe aggregate US data-center electricity and facility modeling, not energy or water per AI request. Decision: use only for national data-center context or methodological background; do not derive a per-user coefficient by dividing national totals by estimated requests.

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

Research and feature selection were approved by the user on 2026-09-24. No implementation or specification changes have been made.

## Commands

### Start research

User: Open the project repository as your workspace, start a fresh chat, and type `start research`.

### Save transcript

Agent: After the user approves the selected features, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `research-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
