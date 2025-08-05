# Green Roof Calculator - Bug Fixes

## Critical Bugs Identified and Fixed:

### 1. Data Structure Issues
**Problem**: Item QB57 has inconsistent properties - missing `storage_type` and `storage_ratio`
**Fix**: Added missing properties:
```javascript
{"id":"QB57","type":"cleanout","category":"drain enclosures","item":"Std. Drain Enclosures, 14\"","base_cost":550.00,"hoisting_sf_per_pallet":4000,"install_rate_sf_per_mh":2000,"depth_inches":14,"dry_weight_psf":0,"saturated_weight_psf":0,"storage_type":"none","storage_ratio":0,"cost_unit":"ea"}
```

### 2. Missing Properties in Data Items
**Problem**: Several data items missing required properties like `cost_unit`, `storage_type`, `storage_ratio`
**Fix**: Ensured all items have consistent property structure

### 3. Calculation Function Bugs
**Problem**: Missing null checks and validation in calculations
**Fix**: Added proper validation:
```javascript
var item = getItemById(input.value);
if (!item) return; // Added null check

// Fixed property access with fallbacks
performance.dry_weight_psf += item.dry_weight_psf || 0;
performance.saturated_weight_psf += item.saturated_weight_psf || 0;
```

### 4. Storage Type Handling
**Problem**: Inconsistent storage type handling in calculations
**Fix**: Standardized storage type logic:
```javascript
if (item.storage_type === 'retention') {
    performance.retention_capacity_in += (item.depth_inches * (item.storage_ratio || 0));
} else if (item.storage_type === 'detention') {
    performance.detention_capacity_in += (item.depth_inches * (item.storage_ratio || 0));
}
```

### 5. Print Styling Issues
**Problem**: Print styles not properly applied
**Fix**: Enhanced print CSS for better formatting

### 6. Form Validation
**Problem**: Missing validation for required fields
**Fix**: Added input validation for area fields and component selections

### 7. Data Persistence
**Problem**: Global defaults not properly saved/loaded
**Fix**: Enhanced localStorage handling with proper error checking

## Additional Improvements:
- Added better error handling throughout
- Improved user feedback with modal dialogs
- Enhanced accessibility with proper ARIA labels
- Fixed responsive design issues
- Improved calculation accuracy with better number handling