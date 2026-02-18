# 🇮🇳 Indian Cities & Currency Support Guide

## Overview
The system now fully supports **Indian cities** with **automatic currency conversion** between USD and INR (Indian Rupees)!

## Features

### ✅ Supported Indian Cities
The system recognizes 40+ major Indian cities including:
- **Mumbai** (Bombay)
- **Delhi**
- **Bangalore** / **Bengaluru**
- **Hyderabad**
- **Chennai** (Madras)
- **Kolkata** (Calcutta)
- **Pune**
- **Ahmedabad**
- **Jaipur**
- **Surat**
- And many more...

### ✅ Automatic Currency Detection
The system automatically detects:
1. **City Location**: Recognizes Indian vs US cities
2. **Currency Type**: USD ($) or INR (₹/Rs/Rupees)
3. **Auto-Conversion**: Converts USD to INR for Indian cities

### ✅ Currency Conversion Rate
- **Exchange Rate**: 1 USD = ₹83.50 (as of Feb 2026)
- **Automatic**: No manual conversion needed

## Usage Examples

### Example 1: Indian City with INR Budget
```
Input: "Ship 500 units to Mumbai with budget ₹50,000"

Result:
✅ Destination: Mumbai
✅ Quantity: 500 units
✅ Budget: ₹50,000
✅ Currency: INR (Indian Rupees)
```

### Example 2: Indian City with USD Budget (Auto-Converts!)
```
Input: "Send 750 units to Bangalore with budget $5,000"

Result:
✅ Destination: Bangalore
✅ Quantity: 750 units
✅ Budget: ₹417,500 (automatically converted from $5,000)
✅ Currency: INR
```

### Example 3: Indian City without Budget
```
Input: "I need to ship 300 units to Chennai"

Result:
✅ Destination: Chennai
✅ Quantity: 300 units
✅ Budget: Not specified
✅ Currency: INR (auto-detected based on city)
```

### Example 4: US City with USD Budget (Works as Before!)
```
Input: "Ship 500 units to Boston with budget $10,000"

Result:
✅ Destination: Boston
✅ Quantity: 500 units
✅ Budget: $10,000
✅ Currency: USD
```

## Supported Currency Formats

### USD (Dollar)
- `$10,000`
- `budget of $5000`
- `max cost 15000`
- `under $10000`

### INR (Indian Rupees)
- `₹50,000` (using ₹ symbol)
- `Rs 50000` or `Rs. 50,000` (using Rs/Rs.)
- `rupees 75000` or `rupee 75000`
- `INR 100000`

## How It Works Behind the Scenes

### 1. Input Parsing
```python
# User enters:
"Ship 500 units to Mumbai with budget $5,000"

# System detects:
- City: Mumbai (Indian city ✅)
- Budget: $5,000 (USD)
- Conversion needed: YES
```

### 2. Auto-Conversion
```python
# System converts:
USD Budget: $5,000
Exchange Rate: 83.50
INR Budget: ₹417,500
```

### 3. Display
```python
# UI shows all costs in INR:
💵 Budget: ₹417,500
💰 Total Cost: ₹385,000
✅ Within Budget: ₹32,500 remaining
```

## Testing

Run the test script to verify functionality:
```bash
python test_indian_city_currency.py
```

This will test:
- ✅ Indian city detection
- ✅ Currency extraction (USD & INR)
- ✅ Full requirement parsing
- ✅ Automatic USD → INR conversion

## Key Benefits

### 🌍 Global Support
- Works seamlessly for both US and Indian cities
- No configuration required

### 💱 Smart Conversion
- Automatically converts USD to INR for Indian cities
- Preserves USD for US cities

### 🎯 User-Friendly
- Users can enter amounts in either currency
- System handles conversion automatically
- Clear currency symbols in UI ($ vs ₹)

### 🔒 Non-Breaking
- All existing US city functionality preserved
- No changes to current workflows
- Backward compatible

## Dashboard Display

When you use Indian cities, the dashboard automatically shows:

### Budget Display
```
💵 Budget: ₹50,000 (instead of $50,000)
```

### Cost Metrics
```
Original Plan Cost: ₹385,000
Mitigation Plan Cost: ₹412,000
Cost per Unit: ₹825.00
```

### Budget Status
```
✅ Within Budget: ₹38,000 remaining from ₹450,000 budget
```

## Important Notes

### Internal Calculations
- All route costs stored in USD (from CSV dataset)
- Costs are converted to INR **only for display** when showing Indian city results
- This ensures consistency with existing cost data

### Exchange Rate
- Current rate: 1 USD = ₹83.50
- This can be updated in the code if needed
- See: `mitigation_module/input_handler.py` → `USD_TO_INR_RATE`

### Cost Data Source
- Route costs come from `Dataset_AI_Supply_Optimization.csv` (in USD)
- Dynamic routes use default cost per km (in USD)
- Display converts to INR for Indian cities

## Troubleshooting

### City Not Recognized?
**Solution**: Check spelling. Common variations are supported:
- Bangalore / Bengaluru ✅
- Mumbai / Bombay ✅
- Chennai / Madras ✅

If your city isn't recognized, add it to `INDIAN_CITIES` list in `mitigation_module/input_handler.py`

### Currency Not Converting?
**Solution**: Ensure you specify the city before the budget:
```
✅ Good: "Ship to Mumbai with budget $5000"
❌ Bad: "Budget $5000 to ship to Mumbai"
```

### Wrong Currency Symbol?
**Solution**: The system auto-detects based on city:
- Indian city → Shows ₹
- US city → Shows $

If you see the wrong symbol, verify the city is in the `INDIAN_CITIES` list.

## Examples in Streamlit App

### Try these inputs in Guardian Mode:

**Indian Cities:**
```
1. "Ship 1000 units to Mumbai with budget ₹100,000"
2. "Send 500 units to Bangalore with budget $3,000"
3. "URGENT: 750 units to Delhi by Feb 15th with Rs 80000 budget"
4. "I need to ship 300 units to Chennai"
```

**US Cities (Still Work!):**
```
1. "Ship 500 units to Boston with budget $10,000"
2. "Send 1000 units to Chicago with budget $20,000"
3. "URGENT: Deliver 750 units to Seattle by 2/15"
```

## Summary

🎉 **The system now supports:**
- ✅ 40+ Indian cities
- ✅ INR currency input (₹, Rs, Rupees)
- ✅ Automatic USD → INR conversion
- ✅ Currency-aware display
- ✅ All existing US city features

🔧 **No changes needed for:**
- ✅ Existing workflows
- ✅ US city shipments
- ✅ Route optimization logic
- ✅ Data files

---

**Ready to ship globally! 🌏📦**
