# FMP_JSONQuery
---
### General Info:

- **Function:**	JSONQuery
- **Purpose:**		Filters and/or harvests data from a JSON object/array of child elements.
- **Requires:**	v18 or later of FileMaker Pro / FileMaker Server
- **External Dependencies:** None
- **Current Version:**		2.0 (20240906_1710)
- **Demo File**: [CF_JSONQuery_v2_PUBLIC_RELEASE_20240912_2340.fmp12.zip](https://github.com/steve-ssh/FMP_JSONQuery/blob/main/CF_JSONQuery_v2_PUBLIC_RELEASE_20240912_2340.fmp12.zip)
- **Updating From Previous Version:** [v2.0 Removed Features.md](https://github.com/steve-ssh/FMP_JSONQuery/blob/main/v2.0%20Removed%20Features.md)

- **Input Parameters**:
	- **Json:**			_JSON_
	- **TargetPath:**			_JSON path to target value_
	- **Operator:**				_See lists below_
	- **ComparisonValue:**			_Value to which the target value is compared_
	- **ValueType:**				_Data-type of target value_
	- **ResultPath:**			_JSON path / aggregate expression / transformation_
	
- **Return Value:**
	- A JSON array/object with filtered/matched results

---

### Optimized Operators

- **Text/Number/Boolean Matching:**
  
	 - EQUALS		( = )
	 - BEGINS_WITH	( LIKE )
	 - BEGINS_WITH_ANY
	 - IN
	 - EXACT

---

### Non-Optimized Operators

- **Text Matching:**
	- ENDS_WITH
	- ENDS_WITH_ANY
	- CONTAINS
	- CONTAINS_ANY
	- CONTAINS_CASE_SENSITIVE

- **Number and Date Comparisons:**
	-  <
	-  <=
	-  \>
	-  \>=
	-  ...
	-  ...x
	-  x...
	-  x...x
	-  NUMERIC_EQUALS	

- **Node Existence & Data Type Operators:**
	- PATH_EXISTS
	- IS_EMPTY
	- IS_NON_EMPTY
	- IS_NON_NULL

- **Other:**
	- MATCH_ALL		(Default Operator)
	- {OMIT}		Prefix before operator to return non-matched object/array values

---

### Value Types:

- **General:**
	- JSONString
	- JSONNumber
	- JSONBoolean
	- JSONNull

- **Date:**
 	- DATE_YYYYDDMM
  - DATE_YYYYMMDD
  - DATE_DDMMYYYY
  - DATE_MMDDYYYY
  - YEAR_YYYYDDMM
  - YEAR_YYYYMMDD
  - YEAR_DDMMYYYY
  - YEAR_MMDDYYYY
  - MONTH_YYYYDDMM
  - MONTH_YYYYMMDD
  - MONTH_DDMMYYYY
  - MONTH_MMDDYYYY
  - DAY_YYYYDDMM
  - DAY_YYYYMMDD
  - DAY_DDMMYYYY
  - DAY_MMDDYYYY


- **Decimal Char:**
	- ","
	- "."

---

### Aggregate Functions:

- **General:**
	- COUNT (*)
	- COUNT ( path ; data_types )
	- SUM	( path ; dec_char / date_fmt )
	- MIN	( path ; dec_char / date_fmt )
	- MAX	( path ; dec_char / date_fmt )
	- AVG	( path ; dec_char / date_fmt )

- **Text:**
	- LIST ( path ; delim_code )
	- LIST_DISTINCT ( path ; delim_code )

- **Path:**
 	- PATH ( path )	

- **Data Types:**
	- NUMBER
	- STRING
	- EMPTY_STRING
	- NON_EMPTY_STRING
	- NULL
	- BOOLEAN
	- TRUE
	- FALSE
	- ARRAY
	- OBJECT
	- ALL

---

### Transformations:

- **Transformation Template:**
 ```
{
	BASE_PATH: 'ResultPath',	
	TEMPLATE: 'json',		
	MAP: [
	   {
	      SOURCE: 'path',
		 OUTPUT: 'path',
		 DATA_TYPE: see below ,
		 DEFAULT: '',
		 DELETE: boolean
	   }
	]
  }
```

- **Values for MapItem.DATA_TYPE:**

  - NUMBER
  - STRING
  - BOOLEAN
  - ARRAY
  - OBJECT
  - NULL
  - RAW
  - SAFE

- **Special options for MapItem.SOURCE:**
  - .
  - .KEY.
  - .INDEX.
  - ../		Reference data from one level up, relative to BASE_PATH

- **Special options for MapItem.OUTPUT:**
  - .
  - .KEY.

---

### Special Path Notation:

- **Target Path:**
	- [*]		Wildcard array-index / object-key

- **Result Path:**
	- [*]		Wildcard array-index  
	- ./		Return matched child elements in a single array.  
	- ~/		Return matched children in context.

---

### Internal Flags:

  Internal flags are variables defined near the beginning of the JSONQuery custom function code.
  The values assigned to these variables can be modified to perform small customization to the behavior of the JSONQuery function.

**JSONQuery defines the following internal flags:**

- **_MXR=50000**   defines the recursion limit imposed within JSONQuery.
    - Recommended to leave as-is.
      
- **_FMT=1**   defines whether or not JSON output should be formatted.
    - Set to 0 to return JSON as non-formatted.
      
- **_DMA=1**   defines whether or not the Operator parameter should default to MATCH_ALL.
    - Set to 0 to indicate that there should be no default.

  



