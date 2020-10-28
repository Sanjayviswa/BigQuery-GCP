# BigQuery-GCP
how to use the Web UI to query public tables and load sample data into BigQuery.

#Step1
gcloud auth list
gcloud config list project

Create Public Dataset
----------------------
#standardSQL Step 2:
SELECT
 weight_pounds, state, year, gestation_weeks
FROM
 `bigquery-public-data.samples.natality`
ORDER BY weight_pounds DESC LIMIT 10;

Adding Custom Data
---------
gsutil cp gs://spls/gsp072/baby-names.zip .

unzip baby-names.zip

gsutil cp yob2014.txt gs://<your_bucket>

#Load data to new Table

Create table from:	Google Cloud Storage
Select file from GCS bucket:	<bucket_name>/yob2014.txt, replace <bucket_name> with the name of the bucket you created earlier.
File format:	CSV
Table name	names_2014
Schema > Edit as text:	Slide on, then add the following in the textbox: name:string,gender:string,count:integer

#standardSQL
SELECT
 name, count
FROM
 `babynames.names_2014`
WHERE
 gender = 'M'
ORDER BY count DESC LIMIT 5;

