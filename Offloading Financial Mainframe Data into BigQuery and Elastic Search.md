# Google Cloud Setup and BigQuery Operations

```bash
# Set the Google Cloud project
export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value project)

# Create a Cloud Storage bucket and copy data
gsutil mb gs://$GOOGLE_CLOUD_PROJECT
gsutil cp -r gs://spls/gsp1153/* gs://$GOOGLE_CLOUD_PROJECT

# Create a BigQuery dataset
bq --location=us mk --dataset mainframe_import

# Copy schema files locally
gsutil cp gs://$GOOGLE_CLOUD_PROJECT/schema_*.json .

# Load data into BigQuery tables
bq load --source_format=NEWLINE_DELIMITED_JSON \
    mainframe_import.accounts gs://$GOOGLE_CLOUD_PROJECT/accounts.json schema_accounts.json

bq load --source_format=NEWLINE_DELIMITED_JSON \
    mainframe_import.transactions gs://$GOOGLE_CLOUD_PROJECT/transactions.json schema_transactions.json

# Create a BigQuery view
bq query --use_legacy_sql=false \
"CREATE OR REPLACE VIEW \`$GOOGLE_CLOUD_PROJECT.mainframe_import.account_transactions\` AS
SELECT t.*, a.* EXCEPT (id)
FROM \`mainframe_import.accounts\` AS a
JOIN \`mainframe_import.transactions\` AS t
ON a.id = t.account_id"

# Sample queries
bq query --use_legacy_sql=false \
"SELECT * FROM \`mainframe_import.transactions\` LIMIT 100"

bq query --use_legacy_sql=false \
"SELECT DISTINCT(occupation), COUNT(occupation)
FROM \`mainframe_import.accounts\`
GROUP BY occupation"

bq query --use_legacy_sql=false \
"SELECT *
FROM \`mainframe_import.accounts\`
WHERE salary_range = '110,000+'
ORDER BY name"

# Enable Dataflow API
gcloud services enable dataflow.googleapis.com


```
```bash
export CONNECTION_URL=99edc18b50834731949cc2eff35b5f0d:dXMtY2VudHJhbDEuZ2NwLmNsb3VkLmVzLmlvJDFhNTdkOGM4NjA4ZDQ1YmViOTAwODZjNGQ5ZWNjMWVjJDEzZGQzMzQ3NTZhODRlZmM4ZjA4ZDYyNzM5ZTVkMGVi
```
```bash
export API_KEY=dDdYUVdKUUJORzREZzY5T0hNYmI6b2ppZjZYZWlUVjZHd0ZYYkFPV0pFUQ==
```

```bash
gcloud dataflow flex-template run bqtoelastic \
  --template-file-gcs-location gs://dataflow-templates-us-central1/latest/flex/BigQuery_to_Elasticsearch \
  --region us-central1 \
  --num-workers 1 \
  --parameters index=transactions,maxNumWorkers=1,query='select * from `YOUR_PROJECT_ID.mainframe_import.account_transactions`',connectionUrl=$CONNECTION_URL,apiKey=$API_KEY
````
