<!--
Copyright 2026 Snowflake Inc.
SPDX-License-Identifier: Apache-2.0

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# AI-Powered Predictive Grid Maintenance

A complete predictive maintenance solution for power grid transformers built on Snowflake's AI Data Cloud.

---

## Overview

This solution demonstrates how utilities can leverage Snowflake to build an end-to-end predictive maintenance system combining:

- **Structured Data**: Sensor readings, asset metadata, maintenance history
- **Unstructured Data**: Technical manuals, maintenance logs, visual inspections
- **Machine Learning**: XGBoost failure prediction, Isolation Forest anomaly detection, RUL estimation
- **Cortex Agents**: Natural language queries via Snowflake Intelligence
- **Real-time Dashboard**: Streamlit-powered monitoring and alerting

### Business Value

| Metric | Impact |
|--------|--------|
| Cost Avoidance | $400K+ per prevented failure |
| SAIDI Improvement | Reduced outage duration |
| Customer Protection | Proactive maintenance for 100 transformers |
| ROI | 10x+ return on predictive maintenance investment |

---

## Repository Structure

```
sfguide-ai-powered-predictive-grid-maintenance/
│
├── deploy.sh                    # Main deployment script
├── clean.sh                     # Teardown script
├── run.sh                       # Runtime operations
├── setup_venv.sh                # Python venv setup
├── requirements.txt             # Python dependencies
│
├── scripts/                     # SQL Scripts
│   ├── 01_infrastructure_setup.sql
│   ├── 02_structured_data_schema.sql
│   ├── 03_unstructured_data_schema.sql
│   ├── 04_ml_feature_engineering.sql
│   ├── 05_ml_training_prep.sql
│   ├── 06_ml_models.sql
│   ├── 07_business_views.sql
│   ├── 08_semantic_model.sql
│   ├── 09_intelligence_agent.sql
│   ├── 10_security_roles.sql
│   ├── 10_streamlit_dashboard.sql
│   ├── 11_load_structured_data.sql
│   ├── 12_load_unstructured_data.sql
│   ├── 13_populate_reference_data.sql
│   ├── 14_generate_recent_sensor_data.sql
│   └── 99_sample_queries.sql
│
├── streamlit/                   # Streamlit dashboard
│   ├── grid_reliability_dashboard.py
│   └── environment.yml
│
├── data_generators/             # Data generation scripts
│   ├── generate_asset_data.py
│   ├── generate_maintenance_logs.py
│   ├── generate_technical_manuals.py
│   ├── generate_visual_inspections.py
│   └── load_unstructured_full.py
│
└── utilities/                   # Utility scripts
    └── test_snowflake_connection.py
```

---

## Prerequisites

- **Snowflake Account** with `ACCOUNTADMIN` role ([sign up for free trial](https://signup.snowflake.com/))
- **Python 3.8+** ([download](https://www.python.org/downloads/))
- **Git** installed

Verify installations:
```bash
python3 --version
pip --version
```

---

## Setup Guide

### Step 1: Install Snowflake CLI

```bash
pip install snowflake-cli-labs
```

Or download installer from [Snowflake CLI releases](https://github.com/snowflakedb/snowflake-cli/releases)

Verify: `snow --version`

---

### Step 2: Configure Snowflake Connection

```bash
snow connection add
```

| Prompt | Value |
|--------|-------|
| Connection name | `default` |
| Account | Your account identifier |
| User | Your username |
| Password | Your password |
| Role | `ACCOUNTADMIN` |
| Other prompts | Press Enter to skip |

> Find your account identifier in the URL: `https://<account-identifier>.snowflakecomputing.com`

---

### Step 3: Test Connection

```bash
snow connection test -c default
```

---

### Step 4: Clone Repository

```bash
git clone https://github.com/Snowflake-Labs/sfguide-ai-powered-predictive-grid-maintenance.git
cd sfguide-ai-powered-predictive-grid-maintenance
```

---

### Step 5: Deploy

```bash
chmod +x deploy.sh
./deploy.sh
```

> **Note:** The deployment script automatically creates a Python virtual environment and installs all required dependencies. If dependency installation fails, you can manually run:
> ```bash
> pip install -r requirements.txt
> ```

| Phase | Description | Duration |
|-------|-------------|----------|
| 1 | Infrastructure setup | ~1 min |
| 2-3 | Data schemas | ~2 min |
| 4-5 | ML pipeline | ~2 min |
| 6 | Analytics views | ~1 min |
| 7 | Data generation & loading | ~5 min |
| 8 | ML training | ~3 min |
| 9 | Streamlit dashboard | ~1 min |

**Total: ~15-20 minutes**

---

### Step 6: Verify & Access

**Streamlit Dashboard:**
- Snowflake UI → **Projects** → **Streamlit** → **GRID_RELIABILITY_DASHBOARD**

**Cortex Agent:**
- Snowflake UI → **Projects** → **Snowflake Intelligence** → **Grid Reliability Intelligence Agent**

---

## What Gets Deployed

### Database Schemas

| Schema | Purpose |
|--------|---------|
| **RAW** | Sensor readings, asset master, maintenance history |
| **UNSTRUCTURED** | Technical manuals, maintenance logs, inspections |
| **FEATURES** | Engineered ML features |
| **ML** | Model registry, predictions, training data |
| **ANALYTICS** | Business views, semantic model |

### ML Models

| Model | Purpose |
|-------|---------|
| XGBoost Classifier | Failure probability prediction |
| Isolation Forest | Anomaly detection |
| Linear Regression | Remaining Useful Life (RUL) |

### Risk Score

```
Risk Score = (Anomaly × 0.3) + (Failure_Prob × 0.5) + (RUL_Factor × 0.2)

  0-40:   Low (routine monitoring)
  41-70:  Medium (increased monitoring)
  71-85:  High (schedule maintenance)
  86-100: Critical (immediate action)
```

---

## Explore the Solution

### Dashboard Pages

| Page | Description |
|------|-------------|
| Overview | Executive KPIs, risk distribution |
| Asset Map | Geographic heatmap |
| High-Risk Alerts | Critical notifications |
| Asset Details | Sensor trends |
| ROI Calculator | Financial modeling |
| Work Orders | Maintenance generation |

### Cortex Agent Questions

```
"Which assets need immediate attention?"
"Show me critical assets in Miami-Dade county"
"Find maintenance reports mentioning oil leaks"
"What's the ROI of our predictive maintenance?"
"Give me a health profile for asset T-SS073-001"
```

---

## Cleanup

```bash
./clean.sh
```

---

## Additional Resources

- [Snowflake CLI](https://docs.snowflake.com/en/developer-guide/snowflake-cli/index)
- [Cortex Analyst](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst)
- [Cortex Agents](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents)
- [Cortex Search](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-search)
- [Snowflake Intelligence](https://docs.snowflake.com/user-guide/snowflake-cortex/snowflake-intelligence)
- [Streamlit in Snowflake](https://docs.snowflake.com/en/developer-guide/streamlit/about-streamlit)

---

## License

Copyright (c) Snowflake Inc. All rights reserved.

Licensed under the Apache 2.0 license.

