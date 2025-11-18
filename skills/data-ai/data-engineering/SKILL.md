---
name: data-engineering
description: Data engineering, ETL pipelines, data warehousing, and analytics. Master data infrastructure and pipeline design.
---

# Data Engineering & Analytics

## Quick Start

Data engineering builds infrastructure for data processing and analytics.

### ETL Pipelines
```python
# Apache Airflow DAG
from airflow import DAG
from airflow.operators.python import PythonOperator
import pandas as pd

def extract_data(**context):
    df = pd.read_csv('source_data.csv')
    context['ti'].xcom_push(key='extracted_data', value=df)

def transform_data(**context):
    df = context['ti'].xcom_pull(key='extracted_data')
    df['amount'] = df['amount'].astype(float)
    df['date'] = pd.to_datetime(df['date'])
    context['ti'].xcom_push(key='transformed_data', value=df)

def load_data(**context):
    df = context['ti'].xcom_pull(key='transformed_data')
    df.to_sql('sales_data', con=engine, if_exists='append')

dag = DAG('etl_pipeline', default_view='graph')
extract = PythonOperator(task_id='extract', python_callable=extract_data, dag=dag)
transform = PythonOperator(task_id='transform', python_callable=transform_data, dag=dag)
load = PythonOperator(task_id='load', python_callable=load_data, dag=dag)

extract >> transform >> load
```

### SQL Analytics
```sql
-- Data Warehouse Query
SELECT 
    DATE_TRUNC('month', order_date) as month,
    product_category,
    SUM(amount) as total_sales,
    COUNT(*) as order_count,
    AVG(amount) as avg_order
FROM sales_fact
WHERE order_date >= DATE '2024-01-01'
GROUP BY DATE_TRUNC('month', order_date), product_category
ORDER BY month DESC, total_sales DESC;
```

### Real-time Streaming
```python
# Kafka Consumer
from kafka import KafkaConsumer
import json

consumer = KafkaConsumer('events')
for message in consumer:
    event = json.loads(message.value)
    process_event(event)  # Real-time processing
```

## Data Architecture

```
Data Sources
    ↓
Ingestion (Kafka, Airflow)
    ↓
Data Lake (S3, HDFS)
    ↓
Processing (Spark, Flink)
    ↓
Data Warehouse (Snowflake, BigQuery)
    ↓
Analytics & BI (Tableau, Looker)
```

## Key Technologies

- **Pipelines** - Airflow, dbt, Luigi
- **Processing** - Apache Spark, Flink, Beam
- **Warehousing** - Snowflake, BigQuery, Redshift
- **BI Tools** - Tableau, Looker, Power BI
- **Streaming** - Kafka, Kinesis, Pub/Sub

## Resources

- [Apache Airflow Docs](https://airflow.apache.org)
- [dbt Documentation](https://docs.getdbt.com)
- [Apache Spark Docs](https://spark.apache.org/docs)
- [Fundamentals of Data Engineering (Book)](https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298)
