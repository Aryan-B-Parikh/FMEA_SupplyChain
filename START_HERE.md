# 🚀 GETTING STARTED - Dynamic Supply Chain System

## Quick Start

### 1. Run the Dynamic Network Test
```bash
python test_dynamic_expansion.py
```

**What it shows:**
- ✅ 5 warehouses configured
- ✅ 3 distribution hubs ready
- ✅ 20+ routes created per city dynamically
- ✅ Multi-hop routing through hubs demonstrated

### 2. Start the Web Application
Open new terminal and run:
```bash
streamlit run app.py
```

Navigate to: **http://localhost:8501**
Go to: **🚚 Supply Chain Risk** tab

### 3. Test Examples

Try these inputs in Guardian Mode:

#### Example 1: Test Multi-Warehouse Routing
```
Ship 500 units to Seattle with budget $15,000
```
**Expected:** System creates 5 direct routes + 15 multi-hop routes = 20 total options

#### Example 2: Test Predefined City with Expanded Options
```
URGENT: Send 1000 units to Chicago by Feb 15th with budget $20,000
```
**Expected:** Uses predefined routes but shows all available alternatives

#### Example 3: Test Multi-Hop Routing
```
Ship 750 units to Portland (multi-hop preferred)
```
**Expected:** Creates routes through distribution hubs

---

## What You Get

### 🏢 5 Warehouses (was 2):
- Warehouse_North
- Warehouse_South
- Warehouse_East       ← NEW!
- Warehouse_West       ← NEW!
- Warehouse_Central    ← NEW!

### 🌐 3 Distribution Hubs (NEW!):
- Hub_Northeast (for multi-hop routing)
- Hub_Midwest (for multi-hop routing)
- Hub_Southeast (for multi-hop routing)

### 📦 For Every City:
- **5 direct routes** (one from each warehouse)
- **15 multi-hop routes** (via distribution hubs)
- **Total: 20+ routing options** (was only 2 before!)

---

## How to Expand

### Want 10 Warehouses?
Edit `mitigation_module/network_config.py`:
```python
WAREHOUSES = {
    # Add more warehouses here!
    "Warehouse_Northwest": {"capacity": 2800, "location": "Northwest", "priority": 6},
    # System auto-adapts - NO CODE CHANGES!
}
```

### Want 5 Hubs?
Edit `mitigation_module/network_config.py`:
```python
DISTRIBUTION_HUBS = {
    # Add more hubs here!
    "Hub_Southwest": {"location": "Southwest", "max_throughput": 4200},
    # Multi-hop routes auto-generated!
}
```

**That's it!** No other code changes needed. System automatically:
- Creates routes from ALL warehouses
- Generates multi-hop combinations
- Updates cost calculations
- Adjusts routing logic

---

## Files to Review

1. **DYNAMIC_NETWORK_GUIDE.md** - Complete architecture explanation
2. **test_dynamic_expansion.py** - Test script showing all features
3. **mitigation_module/network_config.py** - Warehouse & hub config (EDIT THIS)
4. **mitigation_module/dynamic_network.py** - Dynamic route generation (auto-runs)

---

## Key Features

✅ **NO HARDCODING** - All routes generated dynamically
✅ **UNLIMITED EXPANSION** - Add warehouses/hubs without code changes  
✅ **MULTI-HOP ROUTING** - Warehouse → Hub → Destination
✅ **20+ ROUTES PER CITY** - Maximum flexibility for risk mitigation
✅ **INTELLIGENT ROUTING** - Auto-selects best route based on cost & risk
✅ **BACKWARD COMPATIBLE** - Legacy routes (1-10) still work

---

## Support

Questions? Check:
- **DYNAMIC_NETWORK_GUIDE.md** - Full documentation
- **Comments in network_config.py** - Configuration help
- **test_dynamic_expansion.py output** - Example scenarios

🎯 **Remember:** Just edit the config, code adapts automatically!