---
title: "Bigquery Cost Control"
date: 2020-05-24T14:00:23-07:00
draft: false
tags: ["Google Cloud Platform", "Cloud", "BigQuery", "SQL", "Python", "Big Data"]
---

Part _ in a series on working with data in BigQuery on Google Cloud Platform
******

Cost control is a significant issue when working with big data queries (and with cloud applications in general.) If you perform queries carelessly, without specifying exactly what data you need and without estimating the cost, you can easily end up with an eye-popping cloud services bill.

Google [recommends a number of best practices](https://cloud.google.com/bigquery/docs/best-practices-costs) for controlling costs when using BigQuery:

1. <a href = "#avoidselect">Avoid `SELECT *`</A>
2. <a href = "#sampledata">Sample data using preview options</a>
3. <a href = "#pricequeries">Price queries before running them</a>


<a id = "avoidselect">
## Avoid `SELECT *`

This one seems obvious but can be a difficult habit to break. Developers and database people among us are used to issuing a `SELECT *` statement, maybe with a `LIMIT` clause, to get an overview of the table structure and contents. That can get you in trouble with BigQuery. Remember that it is not only the number of records, but the number of *columns* which can be very large in a big data setting. Google states that

>Applying a LIMIT clause to a `SELECT *` query does not affect the amount of data read. You are billed for reading all  bytes in the entire table, and the query counts against your free tier quota.

The reason for this behavior is that using `LIMIT` does not affect the number of bytes *scanned*, only the number of records returned.

Instead, it is recommended that we use one of the [data preview options](https://cloud.google.com/bigquery/docs/best-practices-costs#preview-data):

* In the Cloud Console or the classic web UI, on the table details page, click the Preview tab to sample the data.
* In the command-line interface, use the `bq head` command and specify the number of rows to preview.
* In the API, use tabledata.list to retrieve table data from a specified set of rows.

<a id = "sampledata">
## Sample data using preview options
### Previewing queries in the Console

Here is an example of previewing a query on the [USA Names](https://console.cloud.google.com/marketplace/details/social-security-administration/us-names) dataset, which consists of names from Social Security card applications. This query is large by usual database standards (~100MB), but still very small by big data standards.
![BigQuery cost preview](/images/bq-cost-1.png)

### Previewing with `bq head`

Use the `bq head` to preview data. This command is very useful for exploring data - since it does not initiate a query job, `bq head` will not incur costs. It does not show the size of the returned data, but does give a good view of data structure. Notice that the syntax for referring to datasets and table names is a bit different from the syntax used in SQL:

Performing `bq head --maxrows=10 bigquery-public-data:samples.shakespeare` will give:

<img src = "/images/bq-head-ex.png" width = "464" height = "182">

<a id = "pricequeries">
## Price queries before running them
Queries are priced according to the number of bytes read. Unfortunately, there is not a way to view query cost directly before running it. You will have to get the query size and then use the [GCP Pricing Calculator](https://cloud.google.com/products/calculator/) to get a cost estimate.

The method for getting the query size in the Console is discussed above. To get the size of a query before actually running it, use `bq` with the `--dry-run` flag:

<img src = "/images/bq-dry-run.png" width = "854" height = "122">

The full command is:

```
bq query \
  --use_legacy_sql=false \
  --dry_run \
  'SELECT HCPC, RECID, SHORT_DESCRIPTION, PRICE1
   FROM
     `bigquery-public-data.cms_codes.hcpcs`
   LIMIT
     1000'
```
