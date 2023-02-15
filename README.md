# Low-Latency-Cloud-Data-Pipeline

This project provides a cloud-based solution for processing, storing, and updating transaction data using AWS services. The data pipeline is designed to meet the low latency requirement of the dashboard and ensures that adjusting the state filter requires 5 seconds or less for the new data to populate over a stable, high-bandwidth internet connection.

The data pipeline consists of three main components:

- Data Collection: An API Gateway endpoint accepts incoming JSON payloads containing transaction data. The data is processed by a Lambda function called "post_transaction" and pushed to an SQS queue called "transaction_queue".
- Data Processing: The "transaction_queue" triggers another Lambda function called "process_transactions" which inserts all the records into an RDS database and pushes the order_id of the newly inserted records to another queue called "redshift_queue".
- Data Analysis: Using CloudWatch rules, a Lambda function called "update_redshift" is triggered every 15 minutes to update the new records in the Redshift database.

## Key Features

- Real-time integration of streaming and static data from various sources
- Data warehousing for historical analysis
- Low latency for the reporting tool with a refresh of the data every day at 2:00 am
- Compliance with the SLA of 15 minutes for transactional data to be available in the data warehouse

This solution allows the analytics team to easily create a report based on orders and customer information. They can select a single US state and display the top 3 best-selling pizza combinations, as well as other relevant data such as the total number of pizzas sold, gross sales, and the number of unique customers.

For more information, please refer to the detailed explanation of the architecture, code snippets, and necessary configurations provided in the project documentation.


# Project Documentation and Video

- [Project Documentation](https://github.com/RAJ-SUDHARSHAN/Low-Latency-Cloud-Data-Pipeline/blob/main/AWS_Architecture_explanation_doc.pdf)
- [Project Explanation Video](https://youtu.be/VBG1l7VI5yA)



