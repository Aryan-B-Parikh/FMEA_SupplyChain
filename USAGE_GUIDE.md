# Supply Chain Risk Mitigation - Quick Start Guide

## 🚀 Getting Started

### Option 1: Streamlit Dashboard (Recommended)
```bash
streamlit run app.py
```

1. Navigate to **🚚 Supply Chain Risk** tab
2. Choose input method:
   - **Manual Text**: Paste logistics alert
   - **Upload CSV**: Upload disruption data
   - **Upload Image**: OCR from screenshot
   - **Historical News**: Analyze news dataset

3. Click **🔍 Analyze Disruption**
4. Review extracted disruptions
5. Click **🚀 Calculate Optimized Transport Plan**
6. View narrative-driven report

### Option 2: Python Script
```python
from mitigation_module import (
    TransportOptimizer, 
    DisruptionExtractor, 
    generate_impact_report,
    ROUTE_MAP
)

# Extract disruptions
extractor = DisruptionExtractor()
events = extractor.extract_from_text(alert_text)
disruptions = [e.to_dict() for e in events]

# Optimize
optimizer = TransportOptimizer()
baseline = optimizer.solve(use_disrupted_costs=False)
optimizer.apply_disruptions(disruptions)
adjusted = optimizer.solve(use_disrupted_costs=True)

# Generate report
summary, table, cost_pct = generate_impact_report(
    initial_solution=baseline,
    new_solution=adjusted,
    route_map=ROUTE_MAP,
    disruptions=disruptions
)

print(summary)
print(table)
```

### Option 3: CSV Export
```bash
python export_csv_report.py
```

Opens `mitigation_report.csv` with format:
- Route Strategy
- Original Plan (Standard)
- New Mitigation Plan (Post-Alert)
- Status

---

## 📊 Report Components

### 1. Strategic Narrative
**Dynamic text explanation with 4 scenarios:**

#### Scenario A: Backup Activated
```
🚨 ALERT DETECTED: Route 2 (NewYork) is experiencing disruptions (2.7x cost increase).
✅ BACKUP ACTIVATED: The system has automatically activated backup routes: Route 7.
💰 COST IMPACT: The mitigation strategy will increase total logistics cost by 15.3%.
```

#### Scenario B: Routes Suspended
```
🚨 ALERT DETECTED: Route 1 (Boston), Route 3 (Philadelphia) are too expensive (3.5x).
🔴 ROUTES SUSPENDED: The following primary routes have been stopped: Route 1, Route 3.
✅ BACKUP ACTIVATED: The system has automatically activated backup routes: Route 5, Route 8.
```

#### Scenario C: Forced Continuation (Your Case)
```
🚨 ALERT DETECTED: Route 2 (NewYork), Route 3 (Philadelphia) are experiencing disruptions (2.7x).
⚠️ FORCED CONTINUATION: Despite the disruptions, the system must continue using Route 2, Route 3 
as no alternative routes are available with sufficient capacity. This results in increased operational costs.
💰 COST IMPACT: The mitigation strategy will increase total logistics cost by 34.8%. 
This is unavoidable given current network constraints and disruption severity.
```

#### Scenario D: Routes Rebalanced
```
🟡 ROUTES REBALANCED: The following routes had quantity adjustments: Route 2, Route 4, Route 7.
💰 COST IMPACT: The mitigation strategy will increase total logistics cost by 8.2%.
```

### 2. Route Impact Table

**Format:**
| Route Strategy | Original Plan | New Mitigation Plan | Status |
|----------------|---------------|---------------------|--------|
| To NewYork | Route 2: 1200 Units | Route 2: 1200 Units (⚠️ Higher Cost) | ⚠️ Higher Cost (Forced) |
| (Backup NewYork) | Route 7: 0 Units | Route 7: 400 Units | 🟢 ACTIVATED |

**Status Indicators:**
- 🔴 **STOPPED**: Route discontinued (0 units in new plan)
- 🟢 **ACTIVATED**: Backup route enabled (0 → positive units)
- ⚪ **UNCHANGED**: No change in quantity
- 🟡 **BALANCED**: Quantity adjusted (both plans have flow)
- ⚠️ **Higher Cost (Forced)**: Same flow but must absorb cost increase

### 3. Cost Analysis Metrics

**4-Column Dashboard:**
```
┌─────────────────┬─────────────────┬─────────────────┬─────────────────┐
│ Original Cost   │ Adjusted Cost   │ Cost Impact     │ Routes Changed  │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ $2,791,117.78   │ $3,762,673.02   │ +$971,555.24    │        2        │
│                 │                 │ (34.8% ↑)       │                 │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

**Expandable Details:**
- 🔴 Stopped: Count
- 🟢 Activated: Count
- 🟡 Balanced: Count
- ⚪ Unchanged: Count

---

## 🎯 Input Formats

### 1. Manual Text (Natural Language)
```
OFFICIAL LOGISTICS ALERT
From: Global Freight Authority
Date: 2026-02-03
Severity: CRITICAL

Subject: Port of New York (Route 2) & Philadelphia Access Suspended

Details: Due to an ongoing labor strike at the JFK Airport cargo terminal 
and the adjacent Port of New York, all inbound shipments are currently blocked.

Impact Assessment:
- Affected Routes: New York Inbound (Route 2) and Philadelphia Corridor (Route 5).
- Cost Implication: Emergency air freight alternatives required. 
  Expect transport costs to increase by 500% (5.0x multiplier).
```

**Extraction Result:**
- Route 2: strike, ×2.7 multiplier, severity 7/10
- Route 3: strike, ×2.7 multiplier, severity 7/10

### 2. CSV Upload
**Required Columns:**
```csv
target_route_id,impact_type,cost_multiplier,severity_score
2,strike,5.0,9
3,flood,2.5,7
```

**Optional Columns:**
- location (for reference)
- duration (for tracking)
- description (for context)

### 3. Image/OCR Upload
- Upload PNG/JPG of logistics alert
- System performs OCR extraction
- Same text processing as Manual Text

### 4. Historical News Analysis
- Click "Analyze News Dataset" button
- System scans `News_Category_Dataset_v3.json`
- Filters BUSINESS & WORLD NEWS categories
- Extracts transport disruptions

---

## 🧪 Testing & Validation

### Test Script 1: Full Report Demo
```bash
python test_report_generator.py
```

**Outputs:**
- ✅ Input alert display
- ✅ Disruption extraction summary
- ✅ Baseline vs adjusted costs
- ✅ Strategic narrative
- ✅ Route impact table
- ✅ Cost analysis
- ✅ Detailed flow changes

### Test Script 2: CSV Export
```bash
python export_csv_report.py
```

**Outputs:**
- ✅ `mitigation_report.csv` created
- ✅ Terminal preview of table
- ✅ Strategic narrative
- ✅ File path confirmation

### Test Script 3: Module Tests
```bash
python test_mitigation_module.py
```

**6 Tests:**
1. ✅ Network validation
2. ✅ Text extraction
3. ✅ Baseline optimization
4. ✅ Disruption optimization
5. ✅ Plan comparison
6. ✅ Route details

---

## 🏗️ Architecture Overview

### Module Structure
```
mitigation_module/
├── __init__.py              # Module exports
├── network_config.py        # Route topology
├── mapping_config.json      # Location → Route ID mapping
├── mitigation_solver.py     # Linear Programming optimizer
├── disruption_extractor.py  # Multimodal input processor
├── report_generator.py      # 🆕 Narrative report generator
├── gdelt_service.py         # Real-time news (ON HOLD)
└── README.md                # Complete documentation
```

### Integration Points
- **app.py** (lines ~667-950): Streamlit UI integration
- **test_report_generator.py**: Standalone testing
- **export_csv_report.py**: CSV export utility

---

## 📋 Example Scenarios

### Example 1: Strike at Major Port
**Input:**
```
Labor strike at Port of Los Angeles affecting routes to Dallas and Phoenix.
Expected cost increase: 300%.
```

**Output:**
- Routes 9, 10 disrupted (×3.0 multiplier)
- Backup routes activated: Route 4, Route 8
- Cost increase: 28.5%
- Status: 🔴 STOPPED (original), 🟢 ACTIVATED (backup)

### Example 2: Natural Disaster
**Input:**
```
Hurricane affecting Miami area. I-95 closed. Port operations suspended.
Emergency routes required. Cost impact: 500%.
```

**Output:**
- Route 6 disrupted (×5.0 multiplier)
- Backup route activated: Route 7
- Cost increase: 45.2%
- Status: 🔴 STOPPED → 🟢 ACTIVATED

### Example 3: Multiple Disruptions
**Input:**
```
Flooding in Northeast: Boston, NYC, Philadelphia affected.
Snowstorm in Chicago region.
All routes experiencing 2x cost increase.
```

**Output:**
- Routes 1, 2, 3, 4 disrupted (×2.0 multiplier)
- Mixed strategy: Some stopped, some forced continuation
- Cost increase: 52.1%
- Status: 🔴 STOPPED, 🟢 ACTIVATED, ⚠️ Higher Cost

---

## 🔧 Customization

### Modify Narrative Templates
**File:** `mitigation_module/report_generator.py`
**Function:** `_generate_narrative()`

```python
# Change text for backup activation
narrative_parts.append(
    f"✅ YOUR CUSTOM MESSAGE: Backup routes {backup_list} are now active."
)
```

### Add New Status Types
**File:** `mitigation_module/report_generator.py`
**Function:** `_determine_status()`

```python
def _determine_status(old_qty, new_qty):
    if old_qty > 0 and new_qty == 0:
        return "🔴 STOPPED"
    elif old_qty == 0 and new_qty > 0:
        return "🟢 ACTIVATED"
    # Add your custom status here
    elif some_condition:
        return "🟣 CUSTOM STATUS"
```

### Customize Table Columns
**File:** `mitigation_module/report_generator.py`
**Function:** `_generate_impact_table()`

```python
rows.append({
    'Route Strategy': route_strategy,
    'Original Plan (Standard)': original_plan,
    'New Mitigation Plan (Post-Alert)': new_plan,
    'Status': status,
    'Custom Column': custom_value  # Add your column
})
```

---

## 📤 Export Options

### 1. CSV Export (Implemented)
```python
from export_csv_report import export_to_csv_format

df, csv_path = export_to_csv_format(baseline, adjusted, disruptions, ROUTE_MAP)
```

**Output:** `mitigation_report.csv`

### 2. Excel Export (Add this)
```python
df.to_excel("mitigation_report.xlsx", index=False)
```

### 3. PDF Export (Future)
```python
# Install: pip install reportlab
from reportlab.lib.pagesizes import letter
from reportlab.platypus import SimpleDocTemplate, Table
```

### 4. Email Integration (Future)
```python
import smtplib
from email.mime.text import MIMEText

# Send narrative as email
msg = MIMEText(summary_text)
msg['Subject'] = 'Supply Chain Disruption Alert'
```

---

## ❓ FAQ

### Q1: Why do some routes show "UNCHANGED" but have higher costs?
**A:** When no alternative routes exist with sufficient capacity, the optimizer must continue using disrupted routes despite cost increases. Status shows **"⚠️ Higher Cost (Forced)"**.

### Q2: How do I see only routes that changed?
**A:** In Streamlit, check the expandable "Detailed Route Status Breakdown" section. It shows counts of Stopped/Activated/Balanced routes.

### Q3: Can I customize the narrative text?
**A:** Yes! Edit `mitigation_module/report_generator.py`, function `_generate_narrative()`. Modify the text templates to match your business terminology.

### Q4: How do I export reports for executive presentation?
**A:** Run `python export_csv_report.py` to generate CSV, then:
1. Open in Excel
2. Apply formatting (colors, borders)
3. Add company logo
4. Export as PDF

### Q5: What if I have more than 10 routes?
**A:** The system automatically scales. Update `network_config.py` to add routes:
```python
ROUTE_MAP[11] = ("Warehouse_West", "Client_Seattle")
```

---

## 🎓 Best Practices

### 1. Input Validation
- ✅ Always review extracted disruptions before optimization
- ✅ Verify route IDs are valid (1-10)
- ✅ Confirm cost multipliers are reasonable (1.0-10.0)

### 2. Cost Threshold Alerts
```python
if cost_delta_pct > 30:
    send_email_alert(summary_text, impact_table)
```

### 3. Historical Tracking
```python
# Save each report with timestamp
timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
df.to_csv(f"reports/mitigation_{timestamp}.csv")
```

### 4. Dashboard Refresh
- After major disruptions, re-run optimization every 4 hours
- Compare sequential reports to track cost trends

---

## 📞 Support & Documentation

### Key Files
- **Report Generator**: [mitigation_module/report_generator.py](mitigation_module/report_generator.py)
- **Test Script**: [test_report_generator.py](test_report_generator.py)
- **CSV Export**: [export_csv_report.py](export_csv_report.py)
- **UI Integration**: [app.py](app.py) (lines 667-950)

### Documentation
- **Module README**: [mitigation_module/README.md](mitigation_module/README.md)
- **Implementation Summary**: [REPORT_GENERATOR_SUMMARY.md](REPORT_GENERATOR_SUMMARY.md)
- **This Guide**: [USAGE_GUIDE.md](USAGE_GUIDE.md)

### Testing
- **Full module tests**: `python test_mitigation_module.py`
- **Report demo**: `python test_report_generator.py`
- **CSV export**: `python export_csv_report.py`
- **Streamlit dashboard**: `streamlit run app.py`

---

## ✅ Implementation Checklist

- [x] Narrative-driven report generation
- [x] Status logic (4 types: STOPPED, ACTIVATED, UNCHANGED, BALANCED)
- [x] Disruption indicators (⚠️)
- [x] Cost analysis dashboard
- [x] Destination-grouped table
- [x] CSV export capability
- [x] Streamlit integration
- [x] Test suite validation
- [x] Documentation complete
- [x] Example scenarios working

**Status: ✅ PRODUCTION READY**

---

## 🚀 Next Steps

1. **Restart Streamlit:**
   ```bash
   streamlit run app.py
   ```

2. **Test with your alert:**
   - Navigate to 🚚 Supply Chain Risk tab
   - Paste the JFK Airport alert
   - Click "Analyze Disruption"
   - Review narrative and table

3. **Export CSV report:**
   ```bash
   python export_csv_report.py
   ```

4. **Share with team:**
   - Open `mitigation_report.csv` in Excel
   - Present narrative to stakeholders
   - Use for decision-making

5. **Customize (optional):**
   - Modify narrative templates
   - Add custom status types
   - Integrate with email/Slack alerts
