# AI Applications Data Stores - Complete Solution

## Task 1: Unstructured Data Store for RAG Application

### Data Store Configuration
- **Source**: Cloud Storage
- **Kind of data**: Unstructured
- **Folder to import**: `cloud-samples-data/gen-app-builder/search/cymbal-bank-employee`
- **Multi-region**: global
- **Data store name**: `Datastore Name`
- **Default document parser**: Layout Parser

### Search Application
- **Enterprise edition features**: Enabled
- **Advanced LLM**: Enabled
- **App name**: `App Name`
- **Company name**: Cymbal Bank
- **Multi-region**: global
- **Data Stores**: Select created `Datastore Name`
- **Search type**: Search with an answer

---

## Task 2: Structured Data Store with Periodic Syncing

### BigQuery Findings
- **Rows in lab_dataset.order_info**: 1000

### Data Store Configuration
- **Source**: BigQuery
- **Kind of data**: Structured
- **Sync frequency**: Every day
- **Dataset**: lab_dataset
- **Table**: order_info
- **Data connector name**: `Datastore Name 1`

### Search Application
- **App name**: `App Name 1`
- **Company name**: Cymbal Direct
- **Data Stores**: Select `Datastore Name 1`

---

## Task 3: Website Search Data Store

### Data Store Configuration
- **Source**: Website
- **Advanced**: Disabled
- **Sites to include**:

https://cloud.google.com/generative-ai-app-builder/docs*
https://cloud.google.com/python/docs/reference/discoveryengine/latest*
https://github.com/googleapis/google-cloud-python/tree/main*

- **Sites to exclude**:

  https://cloud.google.com/s/results/generative-ai-app-builder/docs?q*
https://cloud.google.com/s/results/python/docs/reference?q*
https://github.com/search?q*

- **Data store name**: `Datastore Name 2`

### Advanced Indexing Knowledge
1. **Enabled features**:
 - Search with summarization
 - Image search
 - Video search
 - Extractive segments
 - Search with follow-ups

2. **Requirement**: Domain verification

3. **Meta tag uses**:
 - Consider page descriptions
 - Boost labeled results
 - Enable metadata facets

---

## Task 4: Healthcare API Data Store

### FHIR Data
- **Patient count**: 32

### Data Store Configuration
- **Source**: Healthcare API
- **FHIR Store**: Select your fhir_store
- **Data store name**: `Datastore Name 3`

### Location Fact
- Created in same location as FHIR store: **True**

---

## Task 5: Custom Embeddings Data Store

### Cloud Storage Findings
- **PRD PDFs count**: 6
- **prd-prfs.json purpose**: Metadata with ids, ACL, and embeddings

### Data Store Configuration
- **Source**: Cloud Storage
- **Kind of data**: Custom embeddings
- **Data store name**: `Datastore Name 4`

---

## Task 6: Google Drive Data Store

### Configuration Steps
1. Set up Python environment
2. Run populate_drive.py
3. Configure authentication:
 - Provider: Google Identity

### Data Store
- **Source**: Google Drive
- **Drives to sync**: All
- **Data store name**: `Datastore Name 5`

### Second User Test
- Only sees shared docs: **True**

---

## Task 7: Verification Tests

### Test Queries
1. Unstructured: "How do I book air travel?"
2. Structured: Product 6373 orders list
3. Website: "ImportDocumentsRequest"
4. Healthcare: Patient hemoglobin
5. Drive: "Google's revenue"
6. Embeddings: "Framework Atlas"

---

## Task 8: Data Store Update

### Append New Data
- **Source**: Cloud Storage
- **Folder**: [provided]/new_perks
- **Import option**: Append to existing data

---

## Task 9: Cleanup

### Deletion
1. Delete `App Name 1`
2. Delete `Datastore Name 1`
