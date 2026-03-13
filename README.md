# Visualizing Cybersecurity Trends (2015–2024)

## Cyber Events Database Analysis

**Author:** Akash Thanneeru — Northwest Missouri State University (S569652@nwmissouri.edu)

---

## Overview

This project analyzes the **CISSM Cyber Events Database** published by the [Center for International and Security Studies at Maryland](https://cissm.umd.edu/cyber-events-database). The database is an extensive, publicly available collection of cyber-incident records spanning 2014 to the present. It was created to address the critical need for consistent, well-structured data that supports strategic decisions about cyber-event prevention and response.

Using **Tableau** as the primary visualization tool, the project transforms **13,408 recorded cyber events** into interactive dashboards and charts that reveal patterns in threat actors, targeted industries, geographic distribution, and attack types across the 2015–2024 time frame.

---

## Motivation

The increasing scale and impact of cyber events is an enduring concern for both public and private sectors. Information on threat actors, motives, affected industries, and classified impacts is often scarce, fragmented, or locked behind expensive private sources. This project bridges that gap by distilling analytical insights from the CISSM database so that stakeholders can:

- Observe cybersecurity trends over time.
- Identify sector-specific vulnerabilities.
- Analyze the behavior of different threat-actor types (criminal, nation-state, hacktivist, etc.).
- Inform resource-allocation decisions for cyber-event prevention and response.

---

## Repository Contents

| File | Description |
|------|-------------|
| `Cyber Events Database - CISSM_Filtered_Data.xlsx` | Filtered dataset containing **13,408 cyber-event records** with 18 attributes (see *Dataset Schema* below). |
| `Cyber Events Database-CISSM.twbx` | Packaged **Tableau workbook** (version 2024.1.2) with 7 worksheets, 1 interactive dashboard, and 1 story. |
| `CYBER EVENTS DATABASE ANALYSIS_Akash Thanneeru.pptx` | **Presentation** summarizing the project — motivation, methodology, visualizations, and key insights. |
| `Cyber Events Database Codebook.pdf` | Official **codebook** describing every field in the CISSM database. |

---

## Tableau Workbook — Technical Details

The `.twbx` file is a packaged Tableau workbook (source platform: Windows, Tableau version **2024.1.2 build 20241.24.0425.1340**, published to [Tableau Public](https://public.tableau.com)). It bundles the XML workbook definition together with a **Hyper data extract** (`Extract.hyper`, ~4 MB, 13,408 rows × 14 columns).

### Data Source & Extract

| Property | Value |
|----------|-------|
| Connection type | Excel direct (`excel-direct`) — sheet "Sheet 1" from `Cyber Events Database - CISSM` |
| Extract engine | Tableau Hyper (schema `Extract`, table `Extract`) |
| Extract columns | `slug` TEXT, `event_date` TEXT, `actor` TEXT, `actor_type` TEXT, `organization` TEXT, `industry_code` BIG_INT, `industry` TEXT, `motive` TEXT, `event_type` TEXT, `event_subtype` TEXT, `description` TEXT, `source_url` TEXT, `country` TEXT, `actor_country` TEXT |
| Total records | **13,408** |

### Calculated Fields

The workbook defines the following Tableau calculated fields (LOD / table-calc style):

| Calculated Field | Formula | Role |
|------------------|---------|------|
| **Number of Attacks** | `COUNT([slug])` | Measure — counts distinct event records per visual grouping |
| **Year** | `INT(SPLIT([event_date], "-", 1))` | Dimension — extracts the year component from the `event_date` string |
| **Month** | `INT(SPLIT([event_date], "-", 2))` | Dimension — extracts the month component |
| **Date** | `INT(SPLIT([event_date], "-", 3))` | Dimension — extracts the day component |

### Worksheets

The workbook contains **7 worksheets**:

| # | Worksheet | Mark Type | Row Shelf | Column Shelf | Color Encoding | Size Encoding | Filters |
|---|-----------|-----------|-----------|--------------|----------------|---------------|---------|
| 1 | **Symbol Map — Actor Country vs Actor Type** | Multipolygon (filled map) | Latitude (generated) | Longitude (generated) | Actor Type | Number Of Attacks | Actor Type, Year |
| 2 | **Stacked Bar Graph — Attack Distribution vs Event Type** | Bar | Number of Attacks (SUM) | Year | Event Type | — | Actor Type, Year, Event Type |
| 3 | **Stacked Horizontal Bar Chart — Cyberattacks, Industry, and Actor Type Distribution** | Bar | Year | Number of Attacks (SUM) | Actor Type | — | Actor Type, Year, Industry |
| 4 | **Dual Layer Map — Cyberattacks vs Industry Distribution** | Layer 1: Multipolygon; Layer 2: Circle | Latitude (generated) × 2 layers | Longitude (generated) | Layer 1: Industry; Layer 2: fixed `#e15759` | Number of Attacks | Industry |
| 5 | **Symbol Map — Attack Distribution across regions** | Layer 1: Multipolygon; Layer 2: Auto | Latitude (generated) × 2 layers | Longitude (generated) | Layer 1: `#76b7b2`; Layer 2: `#4e79a7` | — | Country |
| 6 | **Tree Map — Attack Event Sub Type** | Automatic (square) | — | — | — | — | — |
| 7 | **Bar Graph — Forecast of the number of attacks** | Automatic | Number of Attacks (forecast) | Year | — | — | — |

> **Reference line:** The *Stacked Bar Graph* worksheet includes an **average reference line** on the Number of Attacks axis (scope: per-pane, formula: `average`), enabling quick comparison of each year's total against the multi-year mean.

### Dashboard & Story

| Component | Details |
|-----------|---------|
| **Dashboard 1** | Fixed size **1000 × 800 px**. Contains three map worksheets (Actor Country vs Actor Type, Cyberattacks vs Industry Distribution, Attack Distribution across regions) arranged side-by-side with interactive filter controls for **Actor Type**, **Year**, **Industry**, and **Country**. Color and size legends are exposed as dashboard zones for user reference. |
| **Story 1** | Fixed size **1016 × 964 px**. Sequences the worksheets into a guided narrative for presentation use. |

---

## Dataset Schema

The filtered Excel dataset contains the following 18 columns:

| Column | Description |
|--------|-------------|
| Actor | Name of the threat actor or group |
| Actor Country | Country of origin of the threat actor |
| Actor Type | Classification (Criminal, Nation-State, Hacktivist, etc.) |
| Country | Target country of the cyber event |
| Date | Day of the month the event was recorded |
| Description | Brief narrative of the incident |
| Event Date | Full date of the cyber event |
| Event Subtype | Specific sub-category (e.g., Exploitation of Application Server) |
| Event Type | High-level category (Disruptive, Exploitative, Mixed, Undetermined) |
| Industry | Industry sector affected |
| Industry Code | NAICS-style industry code |
| Month | Month of the event |
| Motive | Reported motive (Financial, Protest, Espionage, etc.) |
| Organization | Targeted organization |
| Slug | Unique record identifier |
| Source Url | URL of the public source reporting the event |
| Year | Year of the event |
| Number Of Attacks | Count of attacks in the record |

---

## Visualizations & Key Findings

### 1. Symbol Map — Cyber Events by Actor Country & Actor Type

A **multipolygon filled map** with actor-type color encoding and attack-count size encoding. Interactive filters allow slicing by **Actor Type** and **Year**.

**Key findings from the data:**

- **75.4 %** of events (10,108) have an **undetermined** actor country, highlighting the attribution challenge in cybersecurity.
- Among attributed events, **Russia** is the dominant source with **1,741 originating attacks**, followed by China (157), North Korea (149), and the United States (139).
- Nation-state actors concentrate in a handful of countries (Russia, China, North Korea, Iran), while criminal activity is globally dispersed.

---

### 2. Stacked Vertical Bar Graph — Attack Distribution vs. Event Type

A **stacked bar chart** with Year on the x-axis and `COUNT([slug])` (Number of Attacks) on the y-axis, color-encoded by **Event Type**. An **average reference line** is drawn across the axis. Filters: Actor Type, Year, Event Type.

**Key findings from the data (2014–2023; 2024 data not yet available in the extract):**

| Year | Exploitative | Disruptive | Mixed | Undetermined | **Total** | **YoY Growth** |
|------|-------------|-----------|-------|-------------|-----------|----------------|
| 2014 | 358 | 262 | 13 | — | 633 | — |
| 2015 | 509 | 316 | 32 | — | 857 | +35.4 % |
| 2016 | 628 | 445 | 30 | 1 | 1,104 | +28.8 % |
| 2017 | 422 | 360 | 28 | — | 810 | −26.6 % |
| 2018 | 599 | 205 | 20 | — | 824 | +1.7 % |
| 2019 | 614 | 414 | 39 | — | 1,067 | +29.5 % |
| 2020 | 901 | 561 | 283 | 2 | 1,747 | **+63.7 %** |
| 2021 | 596 | 397 | 405 | 32 | 1,430 | −18.1 % |
| 2022 | 940 | 892 | 671 | 58 | 2,561 | **+79.1 %** |
| 2023 | 1,112 | 307 | 879 | 77 | 2,375 | −7.3 % |

- **Exploitative** events dominate every year, comprising **49.8 %** of all events (6,679), followed by Disruptive at 31.0 % (4,159) and Mixed at 17.9 % (2,400).
- The sharpest year-over-year spikes occurred in **2020 (+63.7 %)** — coinciding with the COVID-19 pandemic and accelerated digitization — and **2022 (+79.1 %)** — coinciding with the Russia-Ukraine conflict.
- **Mixed** attacks (combining exploitative and disruptive elements) surged from just 39 in 2019 to **879 in 2023**, a ~23× increase, signaling increasingly sophisticated multi-vector campaigns.

---

### 3. Stacked Horizontal Bar Chart — Cyberattacks, Industry, & Actor Type Distribution

A **horizontal stacked bar chart** with Year on the row shelf and `COUNT([slug])` on the column shelf, color-encoded by **Actor Type**. Filters: Actor Type, Year, Industry.

**Key findings from the data:**

**Top 10 targeted industries:**

| Rank | Industry | Events | Share |
|------|----------|--------|-------|
| 1 | Public Administration | 2,511 | 18.7 % |
| 2 | Health Care and Social Assistance | 1,801 | 13.4 % |
| 3 | Information | 1,388 | 10.4 % |
| 4 | Educational Services | 1,269 | 9.5 % |
| 5 | Finance and Insurance | 1,252 | 9.3 % |
| 6 | Professional, Scientific, and Technical Services | 1,109 | 8.3 % |
| 7 | Other Services (except Public Administration) | 931 | 6.9 % |
| 8 | Manufacturing | 610 | 4.5 % |
| 9 | Retail Trade | 456 | 3.4 % |
| 10 | Transportation and Warehousing | 426 | 3.2 % |

**Criminal vs. Nation-State targeting patterns:**

| | Criminal (top 3) | Nation-State (top 3) |
|---|---|---|
| 1 | Health Care & Social Assistance (1,732) | Public Administration (231) |
| 2 | Public Administration (1,376) | Information (109) |
| 3 | Educational Services (1,108) | Other Services (79) |

- **Criminals** (76.0 % of all events) overwhelmingly target **healthcare** and **education** — sectors with sensitive personal data and often limited cybersecurity budgets.
- **Nation-state** actors (5.5 %) focus on **public administration** (31.4 % of their attacks), reflecting espionage and geopolitical objectives.
- **Hacktivists** (13.9 %) heavily target **public administration** (815 events) and **information** (202 events), consistent with politically motivated operations.

---

### 4. Dual-Layer Map — Industry Distribution of Cyberattacks

A **dual-axis map** combining a **filled multipolygon layer** (color: Industry) with a **proportional circle layer** (size and color: Number of Attacks, circle fill `#e15759`). Filter: Industry.

**Key findings from the data:**

- The United States dominates with **6,479 targeted events** (48.3 % of all events), followed by the United Kingdom (729), Italy (409), Ukraine (383), and Russia (370).
- The top 5 target countries account for **62.5 %** of all recorded cyber events, revealing extreme geographic concentration.

---

### 5. Dual-Layer Map — Attacks On vs. Attacks From Each Country

A **dual-axis map** with two layers — Layer 1: filled multipolygon showing attacks **on** each country (fill `#76b7b2`), Layer 2: symbol map showing attacks **from** each country (fill `#4e79a7`). Filter: Country.

**Key findings from the data:**

| Country | Attacks On | Attacks From | Ratio (On:From) |
|---------|-----------|-------------|----------------|
| United States | 6,479 | 139 | 46.6 : 1 |
| United Kingdom | 729 | 51 | 14.3 : 1 |
| Ukraine | 383 | 125 | 3.1 : 1 |
| Russian Federation | 370 | 1,741 | **1 : 4.7** |
| China | 156 | 157 | 1 : 1 |
| North Korea | — | 149 | Pure source |
| Iran | — | 87 | Pure source |

- **Russia** is the only major country that originates far more attacks than it receives — it receives 1 attack for every 4.7 it originates — making it the world's largest net cyber attacker in this dataset.
- The **United States** absorbs nearly **half of all global cyber events** while originating a relatively small share, reinforcing its status as the primary global target.
- **North Korea** and **Iran** appear almost exclusively as **attack sources** with negligible inbound events recorded.
- **Ukraine** shows a near-balanced but elevated profile (383 inbound vs. 125 outbound), reflecting the active cyber conflict with Russia.

---

### 6. Tree Map — Attack Event Sub-Types

An **automatic (square) tree map** sized by record count over the `event_subtype` dimension.

**Key findings from the data:**

| Rank | Event Subtype | Events | Share |
|------|---------------|--------|-------|
| 1 | Exploitation of Application Server | 4,499 | 33.6 % |
| 2 | Data Attack | 2,609 | 19.5 % |
| 3 | Message Manipulation (phishing/social engineering) | 1,085 | 8.1 % |
| 4 | External Denial of Service | 902 | 6.7 % |
| 5 | Exploitation of End Hosts | 827 | 6.2 % |
| 6 | Data Attack + App Server Exploitation (combined) | 602 | 4.5 % |
| 7 | External Denial of Services (alternate label*) | 524 | 3.9 % |

- **Application-server exploitation** is the single largest attack vector, accounting for **one-third** of all events. This includes SQL injection, remote code execution, and web-application vulnerabilities.
- **Data attacks** (unauthorized data exfiltration/destruction) represent nearly **one in five** events.
- **Denial-of-service** attacks (combining both label variants*) total **1,426 events (10.6 %)**.

> \* The source data contains two slightly different labels ("External Denial of Service" and "External Denial of Services") that refer to the same attack category. They are counted separately here to match the raw data, but aggregate to 1,426 combined events.
- The long tail of subtypes indicates multi-vector sophistication: 602 events combined data attacks *with* application-server exploitation in a single incident.

---

### 7. Bar Graph — Forecast of Number of Attacks

A **bar chart with Tableau's built-in forecasting** (automatic mark type), plotting the calculated `Number of Attacks` measure against `Year`. Mark labels are enabled.

**Key finding:** The forecast model projects continued high volumes of cyber events, consistent with the exponential growth observed between 2019 and 2023 (from 1,067 to 2,375 events — a 122.6 % increase over four years).

---

## Aggregate Statistical Findings

### Actor Type Breakdown

| Actor Type | Events | Share |
|------------|--------|-------|
| Criminal | 10,192 | 76.0 % |
| Hacktivist | 1,862 | 13.9 % |
| Nation-State | 735 | 5.5 % |
| Undetermined | 400 | 3.0 % |
| Hobbyist | 189 | 1.4 % |
| Terrorist | 30 | 0.2 % |

### Motive Breakdown

| Motive | Events | Share |
|--------|--------|-------|
| Financial | 7,547 | 56.3 % |
| Undetermined | 3,100 | 23.1 % |
| Protest | 1,620 | 12.1 % |
| Political-Espionage | 618 | 4.6 % |
| Sabotage | 317 | 2.4 % |
| Personal Attack | 93 | 0.7 % |
| Industrial-Espionage | 90 | 0.7 % |

### Actor Type × Event Type Cross-Tabulation

| Actor Type | Exploitative | Disruptive | Mixed | Undetermined |
|------------|-------------|-----------|-------|-------------|
| Criminal | 5,418 (53.2 %) | 2,339 (22.9 %) | 2,281 (22.4 %) | 154 |
| Hacktivist | 434 (23.3 %) | 1,351 (72.6 %) | 68 (3.7 %) | 9 |
| Nation-State | 462 (62.9 %) | 238 (32.4 %) | 28 (3.8 %) | 7 |
| Hobbyist | 46 | 139 | 4 | — |
| Terrorist | 25 | 5 | — | — |

- **Criminals** favor exploitative tactics (53 %) but are also the primary source of mixed attacks (22 %).
- **Hacktivists** overwhelmingly use **disruptive** methods (73 %), such as DDoS and defacement.
- **Nation-state** actors strongly prefer **exploitative** techniques (63 %), consistent with espionage campaigns.

### Top Named Threat Actors

| Actor | Type | Events |
|-------|------|--------|
| cl0p | Criminal | 301 |
| Anonymous | Hacktivist | 279 |
| NoName057(16) | Hacktivist | 254 |
| Vice Society | Criminal | 162 |
| NGB 3rd Technical Surveillance Bureau | Nation-State | 135 |
| LockBit 3.0 | Criminal | 134 |
| GRU / SANDWORM (Unit 74455) | Nation-State | 118 |
| ALPHVM (BlackCat) | Criminal | 100 |
| Killnet | Hacktivist | 96 |
| Black Basta | Criminal | 96 |

### Monthly Seasonality

Attack volumes are relatively stable across months (range: 1,027 – 1,249 events), with a modest peak in **August (1,249)** and **March (1,185)** and slight troughs in **May (1,027)** and **December (1,027)**.

### United States — Detailed Breakdown

The US accounts for **6,479 events (48.3 %)** of the dataset. Breakdown by actor type:

| Actor Type | Events on US |
|------------|-------------|
| Criminal | 5,853 (90.3 %) |
| Hacktivist | 256 (4.0 %) |
| Undetermined | 155 (2.4 %) |
| Nation-State | 107 (1.7 %) |
| Hobbyist | 100 (1.5 %) |
| Terrorist | 8 (0.1 %) |

---

## Tools & Technologies

- **Tableau Desktop / Public 2024.1** — Interactive data visualization, calculated fields, Hyper extract engine, dual-axis maps, forecasting, story-based presentation.
- **Tableau Hyper Extract** — Columnar in-memory data engine used to store and query the 13,408-row dataset (14 columns, ~4 MB).
- **Microsoft Excel** — Data filtering, cleaning, and preparation.
- **Microsoft PowerPoint** — Project presentation and storytelling.
- **CISSM Cyber Events Database** — Primary data source ([https://cissm.umd.edu/cyber-events-database](https://cissm.umd.edu/cyber-events-database)).

---

## Conclusion

The analysis of the Cyber Events Database offers critical insights into the multifaceted challenges of cybersecurity. By understanding global threat dynamics, adapting defense tactics, addressing sector-specific vulnerabilities, and fostering collaborative responses, stakeholders can navigate the cybersecurity landscape with greater resilience and efficacy. In an ever-evolving digital environment, informed decision-making and proactive action are essential for safeguarding against cyber threats and preserving the integrity of critical systems and data.

---

## Data Source & Acknowledgments

Data sourced from the **Center for International and Security Studies at Maryland (CISSM)** Cyber Events Database, developed in collaboration with **GoTech**. The database includes information on cyberattacks from 2014 to the present, enabling users to distill analytical insights on cyber threats to specific industries and regions.