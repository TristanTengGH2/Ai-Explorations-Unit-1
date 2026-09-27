# Technical Specification

> EDITING DIRECTIVE: USER AND AGENT EDIT THIS FILE COLLABORATIVELY. THE USER MUST REVIEW AND APPROVE ITS CONTENT.

Purpose of this file: Define what the completed project must do so it can be planned, built, and verified.

## Instructions for the user

Translate the approved research into a specification without distorting its evidence, limitations, or uncertainty. Direct the work toward the intended result, judge gaps and trade-offs rather than accepting invented requirements, and approve only a complete, testable specification grounded in the research.

## Instructions for the agent

Read AGENTS.md, brief.md, research.md, and this file. Begin with a concise orientation and one focused question.

Guide the specification one feature at a time. Help turn approved decisions into precise requirements and surface gaps or trade-offs without inventing requirements or making product decisions. Draft concise updates for review, focus on the intended result rather than implementation steps, and never approve the specification on the user's behalf.

## Goal

Expand the local calculator so employees can estimate supported professional text, image, and video AI activity across a project and compare it with streaming and video-meeting activity. Results must distinguish estimated components from missing ones, expose their sources and assumptions, and help employees interpret uncertainty without implying that the calculator measures their actual footprint.

## Features

For each feature, define:

- the need it addresses and intended audience outcome
- its behavior, inputs, and outputs
- its calculations, supporting evidence, and uncertainty
- its interface expectations and acceptance checks

### 1. AI activity breakdown

**Need and outcome.** Employees can record text, image, and video generation separately instead of treating every AI interaction as an equivalent prompt. This supports Alex's media workflow, Jordan's mixed technical work, and Robin's occasional text use.

**Behavior and inputs.**

- Each activity row requires an activity type: text, image, or video.
- The model/tool control offers models supported by the approved source data plus an **Unknown or unsupported** choice. Changing the activity type updates the available model and setting controls.
- Every row records a nonnegative whole-number quantity. The interface labels the unit for that activity, such as requests, images, or generated clips.
- A supported selection exposes only the settings used by its source factor. The interface must not imply that one model's factor applies to a different model, tool, resolution, duration, or output size.
- An unknown or unsupported selection remains in the activity record and project count, but its electricity, carbon, and water outputs read **Not Estimated**. It contributes no numerical value to the total and is listed as omitted rather than silently treated as zero impact.
- Users can add and remove rows while retaining the existing local, no-server operation.

**Calculations and evidence.**

- For a supported AI row, `row electricity = quantity × electricity factor for the selected model and settings`.
- Text estimates may use a pinned EcoLogits version only for configurations checked against Source 2. Video estimates may use the supported model-and-setting scenarios from Source 3. Source 4 supports counting all generated attempts, including discarded clips.
- Source 1 may explain why activity types differ and may supply a clearly dated educational image scenario only if the selected configuration matches the study. Its cross-model mean must not be presented as a current commercial-tool default.
- AI activities report supported electricity only. Because the remote data-center location is unknown, the calculator does not convert that electricity into operational carbon or water using either the employee's grid or a global-average scenario. Those outputs read **Not Estimated**.
- Each numerical result identifies its factor's source, version or publication date, unit, included components, and exclusions. Carbon, electricity, and water remain separate quantities.

**Interface and uncertainty.**

- Rows visibly identify estimated and unestimated metrics. A project containing unsupported activity is labeled an **estimated subtotal**, followed by the omitted rows or components.
- Missing water data displays **Not Estimated**, never zero.
- Employee location may affect carbon from known local-device electricity in later features; it must not be used as the assumed location of remote AI infrastructure.

**Acceptance checks.**

- Adding supported text, image, and video rows changes the appropriate subtotal using their own units and factors.
- Changing a type refreshes its valid models and settings and cannot leave an incompatible factor selected.
- An unknown model with a positive quantity remains visible, produces **Not Estimated**, and does not silently change the numerical subtotal.
- Increasing quantity scales supported row results proportionally, including repeated and discarded generations.
- The calculator works with zero AI rows and does not require a network connection.

### 2. Project-level AI totals

**Need and outcome.** Employees can answer either “What does my typical day look like?” or “What did this project use?” without converting irregular professional work into an invented daily pattern.

**Approved mode behavior.**

- A visible **Daily / Project** control switches the calculator between two mutually exclusive reporting modes.
- Daily mode retains the existing workflow: activity quantities represent a typical day, with daily and annual results.
- Project mode treats activity quantities as actual totals accumulated during one defined project period. It includes retries, discarded generations, and other recorded attempts.
- The calculator never adds Daily-mode quantities to Project-mode quantities. Switching modes updates labels, summaries, and comparisons so the reporting period is always explicit.
- Elapsed project time must not be converted into prompts, tokens, requests, or remote-compute estimates. Coding-agent activity uses actual available records; unavailable activity remains **Not Estimated**.

**Project inputs and outputs.**

- Project mode asks for a duration value and unit, such as **2 weeks**, rather than specific start and end dates. No exact date is requested or stored.
- The duration labels the common reporting window for AI, streaming, and meeting activity. Changing the duration alone does not invent or rescale any activity quantity.
- An optional project label may help distinguish the result without requiring a client name or other identifying information.
- Project output shows the supported electricity, carbon, and water subtotals for that period, broken down by activity type. Unsupported rows and missing components appear beside the subtotal as **Not Estimated**.
- Only compatible quantities with the same metric, reporting period, and calculation boundary may be added. Operational and manufacturing impacts remain separate when their allocation boundaries are incompatible.
- Project results are not automatically annualized. Any normalized comparison must state its denominator and must not imply that the project repeats throughout the year.

**Interface and acceptance checks.**

- Daily and Project quantities are retained separately during the local page session, and switching modes never copies or combines them.
- A project can be entered using a general duration such as days or weeks without supplying calendar dates.
- Two projects with identical recorded activities produce the same project subtotal even if their durations differ; the duration changes only the reporting context unless the user changes an activity quantity.
- A project containing no supported factor displays no fabricated total and clearly identifies the activity as **Not Estimated**.
- Project summaries name the reporting mode and duration so they cannot be mistaken for daily or annual results.

### 3. Streaming comparison

**Need and outcome.** Employees can compare supported AI estimates with streaming during the same reporting period and see how the viewing device changes local electricity use. Multiple rows support Alex's phone, laptop, and television use while remaining useful to Robin and Jordan.

**Behavior and inputs.**

- Each streaming row records nonnegative viewing hours and one device type.
- Supported device choices use verified average-power factors. The initial evidence supports dated scenarios for a laptop, desktop with monitor, and television. A phone or other device may be listed only with a verified factor or as **Not Estimated**.
- Employees may add multiple device rows. The interface warns them to record one physical device-hour once when activities overlap.
- Daily mode treats the hours as a typical day. Project mode treats them as total hours during the displayed project duration.
- Resolution and connection type are not required because the approved research does not establish reliable current factors for converting those selections into a complete streaming footprint.

**Calculations and evidence.**

- Supported device electricity is `device kWh = average device watts × viewing hours ÷ 1,000`.
- Known local-device carbon is `device kWh × the selected local grid factor`. The calculator uses the applicable EPA eGRID subregion when available and identifies a US-average fallback. It does not apply the employee's location to remote infrastructure.
- Carbon Trust Source 6 supplies the component structure and explicitly dated device-power scenarios. EPA Source 9 supplies US electricity-generation carbon factors. The interface cites both beside the result or in an immediately accessible explanation.
- Network, router, remote-server, manufacturing, and water components contribute only when a compatible verified factor is selected. Otherwise they read **Not Estimated** and the numerical result is labeled a device-electricity subtotal.
- The historical 55 g CO2e per viewing hour from Source 6 must not be used as a current universal default.

**Interface and uncertainty.**

- Every device factor displays its source year and scope so historical assumptions are not presented as measurements of the employee's equipment.
- Streaming results identify the estimated device component and list omitted components directly beside the subtotal.
- Employees with measured or otherwise verified equipment data are not silently assumed to match charger ratings, which do not represent average power.

**Acceptance checks.**

- Adding hours for a supported device increases its electricity and local carbon subtotal proportionally.
- The same hours on devices with different verified power factors produce different device subtotals.
- Unsupported devices remain in the activity summary with **Not Estimated** outputs.
- Changing employee location changes only supported local-device carbon, not remote infrastructure or device electricity.
- Streaming hours appear in the selected Daily or Project mode only and are never counted in both.

### 4. Video-meeting comparison

**Need and outcome.** Employees can include the supported local-device impact of their own meeting participation without presenting a rough network proxy as the footprint of the complete meeting. This directly serves Robin's and Jordan's frequent meeting use and gives Alex the same workplace comparison.

**Behavior and inputs.**

- Each meeting row records nonnegative participation hours and the employee's device type.
- Device choices and power factors follow the same verified device-factor rules as streaming.
- The feature represents one employee's participation. It does not request participant count or multiply the employee's device subtotal across an entire call.
- Daily mode treats hours as typical daily participation. Project mode treats them as total participation during the displayed project duration.
- Camera state, video resolution, and Zoom's recommended bandwidth are not used to calculate savings or a complete meeting footprint.

**Calculations and evidence.**

- Supported participant-device electricity is `device kWh = average device watts × meeting hours ÷ 1,000`.
- Supported local carbon is `device kWh × the employee's applicable local grid factor`, using Source 9 under the same rules as streaming.
- Source 6 supports the component-based device method. Source 7 may explain historical methodological disagreement but none of its meeting coefficients or camera-off savings enter the calculation. Source 8 documents connection requirements only and supplies no energy, carbon, or water coefficient.
- Meeting servers, network transmission, router allocation, water, and manufacturing remain **Not Estimated** until compatible evidence is available.

**Interface and uncertainty.**

- The primary result is labeled **Estimated participant-device subtotal**, never “meeting footprint” or “total meeting impact.”
- The result lists the participant device as included and shows every unresolved component beside it as **Not Estimated**.
- A plain-language note explains that shared infrastructure consumes energy but the approved sources do not support allocating a complete amount to one participant.
- The interface warns employees not to enter the same physical device-hour twice when simultaneous activities overlap.

**Acceptance checks.**

- Increasing supported meeting-device hours proportionally increases device electricity and local carbon.
- Unsupported devices remain visible and display **Not Estimated** rather than zero.
- Changing local grid location affects participant-device carbon only.
- The result never uses participant count, Zoom bandwidth, Source 7's 157 g CO2e/hour proxy, or a camera-off percentage.
- Zero AI activity with meeting hours still produces a useful participant-device subtotal.

### 5. Guided assumptions and estimate ranges

**Need and outcome.** Employees can see which assumptions drive their results and adjust supported choices without needing technical expertise or turning the calculator into an unsourced coefficient editor. This gives Jordan useful control, Robin visible evidence and limitations, and Alex access to media-specific settings and water-data gaps.

**Behavior and inputs.**

- A plain-language assumptions panel lists the active reporting mode, activity settings, source-backed factors, grid region, included components, omitted components, and source dates or versions.
- Default controls are guided: employees choose only among models, settings, device types, grid regions, and scenarios supported by the approved evidence.
- A device row may optionally replace its dated average-power factor with a user-supplied measured average wattage. The input is labeled **Measured average power (W)** and must not describe a charger or power-supply maximum rating as measured consumption.
- A user-supplied wattage affects only that row's device electricity and dependent local-grid carbon. It does not fill in network, server, water, manufacturing, or other missing components.
- Employees can reset a custom value to the cited source default. Custom values remain local and are identified in on-screen and generated summaries.
- General editing of AI, network, carbon, or water coefficients is outside the guided interface because arbitrary values would not retain a verified scope or source.

**Calculations and ranges.**

- Device rows use the selected source default or user-supplied measured average wattage in the device-energy formulas defined above.
- When one approved method supplies a lower, central, and upper estimate for the same model, settings, unit, and boundary, the interface may show that source's range alongside the central result.
- Ranges from different studies or incompatible boundaries must not be combined and must not be labeled a statistical confidence interval. A source range is labeled with the source's own meaning; a set of alternative assumptions is labeled a **scenario range**.
- The calculator maintains separate electricity, carbon, and water results. Missing values remain **Not Estimated** and never become zero merely to complete a range.

**Interface and uncertainty.**

- The default view presents short assumption summaries, with expandable details for equations, factors, citations, dates, and exclusions.
- Source-backed and user-supplied factors are visually distinguishable. Generated reports reproduce the active assumptions and identify every custom value.
- Adjusting a supported assumption immediately recalculates the affected subtotal and identifies which component changed.
- Plain-language wording describes results as estimates or estimated subtotals and avoids claims that selecting a lower scenario causes an equivalent real-world reduction in shared infrastructure energy.

**Acceptance checks.**

- Selecting a different supported model, setting, device, or grid region changes only the components tied to that assumption.
- Entering a valid measured average wattage changes that device row and labels the factor **User supplied** in both the interface and report.
- Clearing or resetting a custom wattage restores the cited source default and its label.
- Invalid, negative, or nonnumeric wattage input cannot enter the calculation.
- Unsupported components remain **Not Estimated** after any adjustment.
- No combined range is described as a 95% confidence interval unless one cited method directly provides that interpretation for the complete displayed quantity.
- No employee-grid or global-grid assumption converts remote AI electricity into carbon or water.

### Result structure and initial factor boundaries

**Primary result.**

- The main result is an **Estimated electricity subtotal** for the selected Daily or Project period. It adds only supported AI electricity and supported participant-device electricity expressed in compatible kWh units.
- A breakdown shows AI generation, streaming devices, and meeting devices separately. Each category lists its included and omitted components.
- Local-device carbon appears as its own **Estimated local-device carbon subtotal**. It does not include remote AI, streaming-server, or meeting-server carbon.
- Water reads **Not Estimated** for the five new features unless later specification revisions approve a compatible factor. Missing water is not displayed as zero or folded into an apparently complete total.
- Existing lifestyle figures remain available as a separate context section in Daily mode. They are not added to the digital subtotal and display this disclosure: **“This comparison does not account for overlap between household electricity and the device electricity estimated above. Adding the figures together could count some electricity twice.”**

**Initial approved factor boundaries.**

| Component | Initial supported factor | Required label and handling |
|---|---|---|
| Text AI | Model-and-output-specific electricity from a pinned EcoLogits dataset, limited to configurations checked against Source 2 | Modeled remote electricity; version and settings visible; carbon and water Not Estimated |
| Image AI | No current commercial default approved | Activity count remains visible; electricity, carbon, and water Not Estimated |
| Video AI | Model-and-setting-specific electricity from a pinned Source 3/EcoLogits dataset only where the exact configuration is supported | Modeled remote electricity; model, resolution, duration, and other required settings visible; carbon and water Not Estimated |
| Laptop | 22 W from Source 6 | Historical 2020-era device scenario, or User supplied measured average power |
| Desktop and monitor | 115 W from Source 6 | Historical 2020-era device scenario, or User supplied measured average power |
| Television | 100 W from Source 6 | Historical 2020-era device scenario, or User supplied measured average power |
| Phone and other devices | No verified initial factor | Activity remains visible; result Not Estimated unless user supplies measured average power |
| US local-device carbon | 349.667 g CO2e/kWh US generation average from Source 9 | Dated eGRID2023 fallback for US device use; not a remote-data-center or full-lifecycle factor |

- A subregion factor may replace the US fallback only after its value and location mapping are copied from and checked against the same official eGRID release. Otherwise the interface uses the labeled US fallback rather than inventing regional precision.
- Local-device carbon outside the supported US grid data remains **Not Estimated** unless a compatible regional factor is verified and added through a specification revision.
- AI datasets must be stored locally with their version and relevant source metadata so calculations continue to work without a network connection.
- A future source update is a specification revision: record the version change, changed factors, and expected result changes before implementation.

**Result acceptance checks.**

- The main electricity subtotal equals the visible sum of supported AI, streaming-device, and meeting-device electricity for the selected period.
- The local-device carbon subtotal equals supported streaming and meeting device kWh multiplied by the displayed local grid factor; it excludes all AI electricity.
- An omitted row cannot lower, increase, or complete a subtotal and always remains listed as **Not Estimated**.
- Category subtotals add back to the displayed electricity subtotal without hidden factors or rounding differences beyond the displayed precision.
- Daily results never include Project-mode data, and Project results never include Daily-mode data.

## Shared interface and reliability requirements

- The expanded calculator remains a local, client-side experience and requires no server, account, analytics, or network request to calculate results.
- Source links may open online references, but unavailable internet access cannot prevent data entry, calculation, assumption review, or report generation.
- No entered activity, project duration, optional project label, location, or custom wattage leaves the browser. Daily and Project data persist only for the current page session unless a later approved revision adds an explicit local-save control.
- New controls follow the calculator's existing visual language and remain usable on desktop and mobile layouts.
- Every input has a visible label and works by keyboard. Mode changes and recalculated results expose understandable status text to assistive technology without unexpectedly moving keyboard focus.
- Numeric inputs reject invalid and negative values, accept zero, and define practical upper limits that prevent broken displays without silently changing valid entries.
- Empty states explain what to add. Missing estimates use text in addition to color or icons.
- The generated local report reproduces the selected mode, period, activity rows, supported subtotals, custom values, citations, source dates or versions, included components, **Not Estimated** components, and the lifestyle-overlap disclosure when applicable.
- Display rounding never changes stored calculation values. Visible category values reconcile with visible subtotals within the displayed precision.
- Verification must cover Alex's media-and-streaming scenario, Jordan's irregular project-and-meeting scenario, and Robin's zero-AI scenario from `research.md`.

## User approval

**Approved by the user on 2026-09-27.** The approved specification includes the five features, supported-electricity subtotal, separate local-device carbon subtotal, visible **Not Estimated** components, privacy-conscious project durations, guided assumptions with optional measured device power, and the lifestyle-overlap disclosure. Planning may begin after the specification transcript is saved.

## Out of scope

- Social-media and gaming estimates.
- A complete footprint for streaming or video meetings when server, network, router, water, or manufacturing factors are unsupported.
- Camera-off savings derived from Source 7 or footprint calculations derived from Source 8 bandwidth recommendations.
- Detailed hardware-manufacturing or AI-training allocations without compatible per-activity factors.
- Inferring cloud data-center location from the employee's location.
- Converting remote AI electricity to carbon or water with a global-average location assumption.
- Arbitrary editing of remote-infrastructure, carbon, or water coefficients.
- Uploading usage records, dates, project details, or custom assumptions to a server.

## Revisions

If implementation changes the intended result, update the specification and record what changed and why.

## Commands

### Start specification

User: Open the project repository as your workspace, start a fresh chat, and type `start specification`.

### Save transcript

Agent: After the user approves the specification, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `spec-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
