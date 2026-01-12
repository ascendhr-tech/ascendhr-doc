# Bulk Import Candidates from CSV

**Story ID:** US-4.12  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Scout/Recruiter  
**Priority:** Nice to Have (Phase 2)  
**Complexity:** M (2-3 days)

---

## User Story

> **As a** Scout/Recruiter,  
> **I want to** bulk import multiple candidates from a CSV file,  
> **So that** I can efficiently add candidates from job fairs, referral programs, or external databases.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Candidate list page | Click "Import CSV" button | Adding bulk candidates |
| Job fair event | Post-event with collected resumes | Batch processing |
| External ATS migration | Migrating from old system | One-time data transfer |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Import successful | Candidate list with new entries | Candidates added |
| Validation errors | Error report with fixes needed | Correcting data |
| Partial success | Summary showing success/failures | Reviewing results |

---

## Business Logic

### CSV Format Requirements

**Required Columns:**
- `full_name` (string, max 100 chars)
- `email` (string, valid email format)
- `source` (string, must match existing sources)

**Optional Columns:**
- `phone` (string)
- `resume_url` (string, valid URL)
- `linkedin_url` (string, valid URL)
- `years_experience` (number)
- `current_position` (string)
- `notes` (text)
- `tags` (comma-separated)

**Attribute Columns (Dynamic):**
- `attr_backend_development` (number 1-20)
- `attr_database_design` (number 1-20)
- etc. (any configured attributes)

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - Import 10 Valid Candidates

**Type:** ✅ Happy Path

**Given**
- CSV file "candidates.csv" with 10 rows
- All data valid and properly formatted
- Example row:
  ```csv
  full_name,email,phone,source,years_experience,attr_backend_development
  Alex Chen,alex@email.com,+66123456789,LinkedIn,7,18
  ```

**When**
- I click "Import CSV"
- I upload "candidates.csv"
- System validates file
- I click "Confirm Import"

**Then**
- System processes file in background
- Progress indicator: "Importing... 5/10 (50%)"
- All 10 candidates created successfully
- Each candidate:
  - Status = New
  - Source = LinkedIn
  - Attributes populated (Backend Development = 18)
  - Created_at = current timestamp
- Success message: "10 candidates imported successfully"
- Email notifications sent (if configured)
- Fit scores calculated automatically (if positions matched)
- Redirected to candidate list showing new entries

---

### Scenario 2: Happy Path - Import with Partial Attributes

**Type:** ✅ Happy Path

**Given**
- CSV has basic info + some attributes
- Not all attributes provided (acceptable)

**When**
- Import file with:
  - Name, email, source (required)
  - Backend Development, Database Design (2 of 10 attributes)

**Then**
- Candidates created with partial data
- Missing attributes = null (can be filled later)
- Warning: "2 of 10 attributes provided - complete profiles for better fit scores"
- Import proceeds successfully

---

### Scenario 3: Alternative Path - Download Template

**Type:** 🔀 Alternative Path

**Given**
- First time using import feature

**When**
- I click "Import CSV"
- Modal shows "Download Template" link
- I click download

**Then**
- CSV template downloaded: "candidate_import_template.csv"
- Template includes:
  - Header row with all column names
  - Example row with sample data
  - Comments explaining format
- Sample content:
  ```csv
  # AscendHR Candidate Import Template
  # Required: full_name, email, source
  # Optional: phone, resume_url, years_experience, attributes
  full_name,email,source,attr_backend_development,attr_database_design
  John Doe,john@example.com,LinkedIn,16,15
  ```

---

### Scenario 4: Alternative Path - Dry Run (Preview Mode)

**Type:** 🔀 Alternative Path

**Given**
- Want to verify data before actual import

**When**
- Upload CSV
- Check "Preview Only (Don't Import)"
- Click "Validate"

**Then**
- System validates all rows
- Shows preview table:
  ```
  Row | Name       | Email            | Status
  ----|------------|------------------|--------
  1   | Alex Chen  | alex@email.com   | ✓ Valid
  2   | Jane Doe   | jane@email.com   | ✓ Valid
  3   | Bob Smith  | invalid-email    | ✗ Invalid email
  ```
- Validation summary: "2 valid, 1 error"
- No data imported (preview only)
- Can download error report
- Can fix and re-upload

---

### Scenario 5: Alternative Path - Map Custom Columns

**Type:** 🔀 Alternative Path

**Given**
- CSV from external system with different column names
- Their format: "Name", "E-mail", "Phone Number"
- Our format: "full_name", "email", "phone"

**When**
- Upload CSV
- System detects column mismatch
- Column mapping interface shown:
  ```
  CSV Column    →  AscendHR Field
  Name          →  [full_name ▼]
  E-mail        →  [email ▼]
  Phone Number  →  [phone ▼]
  ```
- I map columns correctly
- Click "Import with Mapping"

**Then**
- Data imported using custom mapping
- Mapping saved for future imports
- Success: "10 candidates imported (custom mapping applied)"

---

### Scenario 6: Validation Error - Missing Required Columns

**Type:** ❌ Validation Error

**Given**
- CSV missing "email" column (required)

**When**
- Upload file

**Then**
- Error: "Missing required column: 'email'"
- Import blocked
- Suggestion: "Download template to see required format"
- File not processed

---

### Scenario 7: Validation Error - Invalid Email Format

**Type:** ❌ Validation Error

**Given**
- CSV with row: "Bob Smith,not-an-email,LinkedIn"

**When**
- Processing import

**Then**
- Row 3 validation fails
- Error: "Invalid email format in row 3: 'not-an-email'"
- Options:
  - Skip invalid rows, import rest
  - Fix and re-upload entire file
  - Download error report
- If "Skip": 9 candidates imported, 1 skipped
- Error summary provided

---

### Scenario 8: Validation Error - Duplicate Email in CSV

**Type:** ❌ Validation Error

**Given**
- CSV has 2 rows with same email "alex@email.com"

**When**
- Import attempted

**Then**
- Error: "Duplicate email in rows 2 and 5: alex@email.com"
- Must resolve duplicates before import
- Suggestion: "Keep only one entry per candidate"

---

### Scenario 9: Validation Error - Duplicate Email in Database

**Type:** ❌ Validation Error

**Given**
- Candidate "alex@email.com" already exists in database
- CSV includes "alex@email.com" again

**When**
- Import processed

**Then**
- Row validation fails
- Warning: "Email alex@email.com already exists (existing candidate: CAN-2026-010)"
- Options:
  - Skip duplicate (default)
  - Update existing candidate
  - Create anyway with different email
- If skip: "9 of 10 imported, 1 duplicate skipped"

---

### Scenario 10: Business Rule Error - Invalid Source

**Type:** ⚠️ Business Rule Error

**Given**
- CSV has source: "Facebook" (not configured in system)
- Valid sources: LinkedIn, Referral, Job Board, Direct

**When**
- Import processed

**Then**
- Error: "Invalid source 'Facebook' in row 4"
- Suggestion: "Valid sources: LinkedIn, Referral, Job Board, Direct"
- Options:
  - Map "Facebook" → "Job Board"
  - Skip row
  - Add "Facebook" as new source

---

### Scenario 11: Business Rule Error - Attribute Out of Range

**Type:** ⚠️ Business Rule Error

**Given**
- CSV has attr_backend_development = 25 (max is 20)

**When**
- Validation runs

**Then**
- Error: "Attribute value out of range (1-20) in row 3: Backend Development = 25"
- Must fix value
- Cannot import with invalid attribute scores

---

### Scenario 12: Permission Denied - Non-Recruiter Import

**Type:** 🔒 Permission Denied

**Given**
- I am Interviewer (not Recruiter)

**When**
- I attempt to access import feature

**Then**
- Error: "Only recruiters can import candidates"
- Import button hidden
- Message: "Contact recruiter to import candidates"

---

### Scenario 13: Loop/Retry - Fix and Re-import

**Type:** 🔄 Loop/Retry

**Given**
- First import failed with 5 errors
- Downloaded error report

**When**
- I fix errors in CSV
- Re-upload corrected file
- Click "Import Again"

**Then**
- System processes corrected file
- All validations pass
- 10 candidates imported successfully
- Previous failed attempt logged
- Audit trail: "Import retry succeeded"

---

### Scenario 14: Empty State - No File Selected

**Type:** 📭 Empty State

**Given**
- Import dialog open

**When**
- Click "Import" without selecting file

**Then**
- Error: "Please select a CSV file"
- File input highlighted
- No processing attempted

---

### Scenario 15: Empty State - Empty CSV File

**Type:** 📭 Empty State

**Given**
- CSV file has only header row (no data rows)

**When**
- Upload and import

**Then**
- Warning: "CSV file is empty (no data rows)"
- No candidates imported
- Success (technically), but 0 records processed

---

### Scenario 16: Session Timeout - Long Import

**Type:** ⏰ Timeout

**Given**
- Importing 1,000 candidates (large file)
- Process takes 5 minutes
- Session timeout = 30 minutes

**When**
- Import running
- User waits

**Then**
- Import completes in background (server-side)
- Email sent on completion: "Import finished: 1,000 candidates added"
- User can check import history
- Session remains valid (activity)

---

### Scenario 17: Concurrent Modification - Simultaneous Imports

**Type:** ⚡ Concurrent

**Given**
- Two recruiters import different CSV files simultaneously

**When**
- Both processing at same time

**Then**
- Each import processed independently
- Candidate IDs assigned uniquely (no collision)
- Both succeed without conflict
- Audit log tracks both imports with user attribution

---

### Scenario 18: Data Integrity - Transaction Safety

**Type:** ⚠️ Data Integrity

**Given**
- Importing 100 candidates
- Row 50 causes database error (unexpected issue)

**When**
- Import fails mid-process

**Then**
- Transaction rolled back
- Zero candidates imported (all-or-nothing)
- Error: "Import failed at row 50 - no candidates were added"
- Database remains consistent
- Can fix and retry

---

### Scenario 19: Integration Error - Attribute Service Down

**Type:** ⚠️ Integration Error

**Given**
- CSV includes attribute scores
- Player Card System API unavailable

**When**
- Import attempted

**Then**
- Basic candidate data imported successfully
- Attributes queued for later sync
- Warning: "Attributes will sync when Player Card System is available"
- Candidates created, attributes pending
- Non-blocking error

---

### Scenario 20: Performance - Import 1,000 Candidates

**Type:** ⚠️ Performance

**Given**
- Large CSV with 1,000 rows

**When**
- Upload and import

**Then**
- File processed in batches of 100
- Progress indicator: "Processing batch 5/10 (500/1000)"
- All 1,000 imported within 5 minutes
- Background job (non-blocking)
- Email notification on completion
- No timeout or browser freeze

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Import Dialog

```
╔═══════════════════════════════════════╗
║ Import Candidates from CSV            ║
╠═══════════════════════════════════════╣
║                                       ║
║ Step 1: Download Template (Optional)  ║
║ [Download CSV Template]               ║
║                                       ║
║ Step 2: Upload Your File              ║
║ ┌───────────────────────────────────┐ ║
║ │ Drag & drop CSV file here         │ ║
║ │ or [Browse Files]                 │ ║
║ └───────────────────────────────────┘ ║
║                                       ║
║ File Requirements:                    ║
║ • CSV format (.csv)                   ║
║ • Max 1,000 rows                      ║
║ • Required: full_name, email, source  ║
║                                       ║
║ Options:                              ║
║ ☐ Preview only (don't import)         ║
║ ☐ Skip duplicates automatically       ║
║ ☐ Send email notifications            ║
║                                       ║
║ [Cancel] [Validate & Import] ←       ║
╚═══════════════════════════════════════╝
```

### Import Progress

```
╔═══════════════════════════════════════╗
║ Importing Candidates...               ║
╠═══════════════════════════════════════╣
║                                       ║
║ Processing candidates.csv             ║
║                                       ║
║ ████████████░░░░░░░░ 60%             ║
║                                       ║
║ Progress: 60 of 100 candidates        ║
║                                       ║
║ Status:                               ║
║ ✓ Validated: 100                      ║
║ ✓ Imported: 60                        ║
║ ⏳ Remaining: 40                       ║
║                                       ║
║ Estimated time: 2 minutes             ║
║                                       ║
║ [Cancel Import]                       ║
╚═══════════════════════════════════════╝
```

### Import Summary

```
╔═══════════════════════════════════════╗
║ Import Complete                       ║
╠═══════════════════════════════════════╣
║                                       ║
║ ✅ Successfully imported 95 candidates ║
║                                       ║
║ Summary:                              ║
║ • Total rows: 100                     ║
║ • Successful: 95                      ║
║ • Duplicates skipped: 3               ║
║ • Validation errors: 2                ║
║                                       ║
║ Errors:                               ║
║ ❌ Row 5: Invalid email format        ║
║ ❌ Row 23: Invalid source "Twitter"   ║
║                                       ║
║ [Download Error Report (CSV)]         ║
║ [View Imported Candidates]            ║
║ [Import Another File]                 ║
║ [Done]                                ║
╚═══════════════════════════════════════╝
```

### Error Report CSV Format

```csv
row_number,error_type,field,value,message
5,validation_error,email,invalid-email,Invalid email format
23,business_rule_error,source,Twitter,Source not found. Valid sources: LinkedIn, Referral, Job Board, Direct
45,duplicate_error,email,alex@email.com,Email already exists for candidate CAN-2026-010
```

---

## Technical Implementation

### CSV Parser

```javascript
async function importCandidatesFromCSV(file, options = {}) {
  const { 
    skipDuplicates = true, 
    previewOnly = false,
    batchSize = 100 
  } = options;
  
  // 1. Parse CSV
  const rows = await parseCSV(file);
  
  // 2. Validate structure
  const requiredColumns = ['full_name', 'email', 'source'];
  validateColumns(rows[0], requiredColumns);
  
  // 3. Process in batches
  const results = {
    total: rows.length - 1, // Exclude header
    successful: 0,
    errors: [],
    skipped: 0
  };
  
  for (let i = 0; i < rows.length - 1; i += batchSize) {
    const batch = rows.slice(i + 1, i + batchSize + 1); // Skip header
    
    for (const [index, row] of batch.entries()) {
      const rowNumber = i + index + 2; // +2 for header and 1-indexed
      
      try {
        // Validate row
        const validation = validateCandidateRow(row);
        if (!validation.valid) {
          results.errors.push({
            row: rowNumber,
            errors: validation.errors
          });
          continue;
        }
        
        // Check duplicates
        if (skipDuplicates) {
          const exists = await candidateExists(row.email);
          if (exists) {
            results.skipped++;
            continue;
          }
        }
        
        // Create candidate (if not preview)
        if (!previewOnly) {
          await createCandidate({
            full_name: row.full_name,
            email: row.email,
            source: row.source,
            phone: row.phone,
            // ... map other fields
            attributes: extractAttributes(row)
          });
        }
        
        results.successful++;
        
      } catch (error) {
        results.errors.push({
          row: rowNumber,
          error: error.message
        });
      }
    }
    
    // Update progress
    emitProgress({
      processed: i + batch.length,
      total: results.total
    });
  }
  
  return results;
}
```

### Validation Functions

```javascript
function validateCandidateRow(row) {
  const errors = [];
  
  // Required fields
  if (!row.full_name || row.full_name.trim() === '') {
    errors.push({ field: 'full_name', message: 'Name is required' });
  }
  
  // Email validation
  if (!row.email || !isValidEmail(row.email)) {
    errors.push({ field: 'email', message: 'Invalid email format' });
  }
  
  // Source validation
  const validSources = ['LinkedIn', 'Referral', 'Job Board', 'Direct', 'Career Page'];
  if (!validSources.includes(row.source)) {
    errors.push({ 
      field: 'source', 
      message: `Invalid source. Valid: ${validSources.join(', ')}` 
    });
  }
  
  // Attribute range validation
  for (const [key, value] of Object.entries(row)) {
    if (key.startsWith('attr_') && value) {
      const numValue = parseInt(value);
      if (numValue < 1 || numValue > 20) {
        errors.push({
          field: key,
          message: `Attribute value must be 1-20, got ${numValue}`
        });
      }
    }
  }
  
  return {
    valid: errors.length === 0,
    errors
  };
}
```

---

**END OF US-4.12**

---

## Summary

US-4.12 enables efficient bulk candidate management with:

1. ✅ CSV template for easy data preparation
2. ✅ Comprehensive validation before import
3. ✅ Preview mode for safe verification
4. ✅ Column mapping for external data
5. ✅ Batch processing for large files
6. ✅ Error handling with detailed reports
7. ✅ Duplicate detection and handling
8. ✅ Transaction safety (all-or-nothing)

**Key Success Criteria:**
- Import 1,000 candidates in <5 minutes
- <1% error rate on properly formatted files
- Clear error messages for all validation issues
- Zero data corruption from failed imports
- Seamless integration with existing candidate flow

This story significantly improves recruiter efficiency for high-volume hiring events and data migrations.
