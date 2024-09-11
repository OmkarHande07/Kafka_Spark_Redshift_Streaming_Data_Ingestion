# Kafka_Spark_Redshift_Streaming_Data_Ingestion
Developed a Hybrid Type of solution using Cloud and Local System

Using the producer script data will be generated for tellecommunication like call_duration, service_provider, start_time, end_time which will be dumped into kafka topic and this data will be ingested into AWS Redshift Warehouse.on the top of it dashboard will be created using AWS QuickSight. 

**Steps to create Pipeline:**

1. Run the docker-compose.yml file(input file) in the cmd with [docker compose -f docker-compose.yml up -d] command.In docker desktop container will start running then wait till all services gets started.
2. Using pip command - install python pyspark, kafka-python, faker library (it is used to generate mock data in the producer script)
3. In docker desktop - container - go to control-centre -> click on the port on which it is started-> it will open confluent kafka page here we can create kafka topic.
4. Now open 2 instances of cmd - In 1 window run spark_redshift_stream.py file (input file) this will start spark session and also read the data from kafka topic applying some DQ check and dumping into redshift. | In 2nd windoq eun kafka_producer.py script which will generare mock data.
5. Now records will be ingested into the kafka topic in realtime.
6. Go to AWS Redshift start the cluster then using query editor create schema and table for the destination.
7. After record gets inserted into kafka topic we can check records in the redshift table by running SELECT query.
8. On the top of this table we can create simple dashboard usign AWS QuickSight -> Create Dataset -> select Redshift -> Give some name -> For DataBase server copy the Endpoint of Redshift-cluster and paste it -> 5439 as port -> enter username and password->create -> Select cschema -> select table -> select Direct;y Query Your Data option -> create.
9. now canvas will be open here -> for checking count for each telephone_provider:
    select Piechart -> from left side drag & drop the network_provider column -> chart will be displayed -> we can change the name for it.
10. For call duration :
    Select Bar Chart -> drag & drop network_provider on  X-axis -> call_duration on Y-axis ( here sumation will be applied)
11. Now we can publish this dashboard and it will realtime.     
 
