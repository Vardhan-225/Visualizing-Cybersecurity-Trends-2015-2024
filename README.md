# Visualizing Cybersecurity Trends (2015–2024)

## Cyber Events Database Analysis

**Author:** Akash Thanneeru — Northwest Missouri State University (S569652@nwmissouri.edu)

---

## Overview

This project analyzes the **CISSM Cyber Events Database** published by the [Center for International and Security Studies at Maryland](https://cissm.umd.edu/cyber-events-database). The database is an extensive, publicly available collection of cyber-incident records spanning 2014 to the present. It was created to address the critical need for consistent, well-structured data that supports strategic decisions about cyber-event prevention and response.

Using **Tableau** as the primary visualization tool, the project transforms over **13,400 recorded cyber events** into interactive dashboards and charts that reveal patterns in threat actors, targeted industries, geographic distribution, and attack types across the 2015–2024 time frame.

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
| `Cyber Events Database-CISSM.twbx` | Packaged **Tableau workbook** with interactive dashboards and visualizations. |
| `CYBER EVENTS DATABASE ANALYSIS_Akash Thanneeru.pptx` | **Presentation** summarizing the project — motivation, methodology, visualizations, and key insights. |
| `Cyber Events Database Codebook.pdf` | Official **codebook** describing every field in the CISSM database. |

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

The Tableau workbook and presentation include the following analyses:

### 1. Filled Map — Cyber Events by Actor Country & Actor Type
A geographic heat map showing the global distribution of cyber events by the country of origin of threat actors and their classification.

### 2. Stacked Vertical Bar Graph — Attack Distribution vs. Event Type
Tracks the yearly distribution of cyberattacks by event type (Disruptive, Exploitative, Mixed, Undetermined). **Key finding:** Exploitative attacks have become significantly more prevalent in recent years, indicating a strategic shift toward data theft and system-vulnerability exploitation.

### 3. Stacked Horizontal Bar Chart — Industry & Actor Type Distribution
Examines the impact of cyberattacks across industries. **Key finding:** Finance, public administration, and healthcare are the most frequently targeted sectors. Nation-state actors tend to target critical infrastructure (public administration), while criminal actors focus on financial institutions, healthcare, and education services.

### 4. Dual-Layer Map — Industry Distribution of Cyberattacks
Combines a filled map with a symbol map to visualize how attacks on various industries are distributed geographically.

### 5. Dual-Layer Map — Attacks On vs. Attacks From Each Country
Correlates the number of attacks a country receives with the number it originates. **Key finding:** Russia is the largest source of cyberattacks (1,741 originating attacks) yet experiences relatively few incoming attacks (370). The United States is the most targeted country (6,479 attacks) while also originating a notable number of attacks (139).

### 6. Tree Map — Attack Event Sub-Types
A tree map visualization that highlights the most common sub-types of cyber events in the dataset.

---

## Tools & Technologies

- **Tableau** — Interactive data visualization and dashboard creation.
- **Microsoft Excel** — Data filtering, cleaning, and preparation.
- **Microsoft PowerPoint** — Project presentation and storytelling.
- **CISSM Cyber Events Database** — Primary data source ([https://cissm.umd.edu/cyber-events-database](https://cissm.umd.edu/cyber-events-database)).

---

## Conclusion

The analysis of the Cyber Events Database offers critical insights into the multifaceted challenges of cybersecurity. By understanding global threat dynamics, adapting defense tactics, addressing sector-specific vulnerabilities, and fostering collaborative responses, stakeholders can navigate the cybersecurity landscape with greater resilience and efficacy. In an ever-evolving digital environment, informed decision-making and proactive action are essential for safeguarding against cyber threats and preserving the integrity of critical systems and data.

---

## Data Source & Acknowledgments

Data sourced from the **Center for International and Security Studies at Maryland (CISSM)** Cyber Events Database, developed in collaboration with **GoTech**. The database includes information on cyberattacks from 2014 to the present, enabling users to distill analytical insights on cyber threats to specific industries and regions.