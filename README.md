# Project Overview

In the modern data-driven landscape, businesses are transitioning from batch processing to real-time (RT) or near-real-time (NRT) data loading to gain competitive advantages through faster insights. The Data Vault 2.0 architecture, originally designed to accommodate batch data loading, now supports RT/NRT data integration seamlessly, proving its long-term value and adaptability.

This project demonstrates how to implement a real-time Data Vault on Snowflake, leveraging its robust features designed for streaming data. We'll walk through setting up a complete Data Vault environment, including data modeling, the construction of data pipelines using Snowflake's Snowpipe and Continuous Data Pipelines, and applying data virtualization to enhance data access.

## What is Data Vault?

Data Vault is a modern data modeling methodology specifically designed for data warehousing. It was developed by Dan Linstedt in the early 2000s. The architecture is highly flexible, scalable, and adaptable, making it ideal for handling large volumes of data from various sources. Data Vault is particularly well-suited for enterprises that require historical data storage, audit trails, and the ability to quickly integrate new data sources.

### Key Components of Data Vault

Data Vault modeling consists of three primary types of entities:

1. **Hubs**: These are the core entities in a Data Vault model, representing business keys. Hubs help in managing business keys and ensuring that the data model remains robust against changes in business processes.

2. **Links**: Links are used to establish relationships between Hubs or other Links. They are essential for building the network of relationships within the Data Vault and for maintaining the integrity and history of interconnected data.

3. **Satellites**: Satellites store the descriptive attributes related to Hubs and Links, capturing the context of business keys and relationships at various points in time. They allow for the storage of historical changes and provide a rich, time-variant context for the data stored in Hubs and Links.

## Data Vault Architecture
![Data Vault Refrence Architecture](images/DataVault-Architecture.png)

The data lifecycle is split into the following layers:

1. **Data Acquisition**: Data is extracted from source systems and made accessible to Snowflake.
2. **Loading & Staging**: Data is moved into Snowflake and optimized for efficient query access, maintaining its original format. This layer also involves adding technical metadata and calculating business keys.
3. **Raw Data Vault**: Stores data with no soft business rules applied, only immutable rules, to ensure the data remains as received.
4. **Business Data Vault**: Enhances the raw data with soft business rules, including potentially calculated satellites and mastered records, optimizing for business intelligence.
5. **Information Delivery**: Delivers data through consumer-oriented models, such as dimensional models or denormalized tables, tailored to the needs of end-users and supported by Snowflake’s scalable architecture.

## Environment Setup

For demonstration purposes, we use the `ACCOUNTADMIN` role, although in real-world scenarios, a robust Role-Based Access Control (RBAC) model would typically be implemented.

### Virtual Warehouses

We will create two Snowflake virtual warehouses:

1. **dv_lab_wh**: A generic warehouse used throughout this lab.
2. **dv_rdv_wh**: Dedicated to our data pipelines, specifically for Raw Data Vault objects.

Additional virtual warehouses for Business Data Vault and Information Delivery are outlined in the SQL script but are commented out to simplify the initial setup.

### Configuration Overview

The provided SQL script configures the Snowflake environment to support this project by:

- Assigning the highest privilege role to ensure all operations can be performed.
- Creating a new database and setting it as the active database for operations.
- Establishing virtual warehouses optimized for different stages of data processing.
- Defining multiple schemas to organize data at various stages of the Data Vault lifecycle, from staging to information delivery.

This configuration ensures a structured and scalable environment tailored to efficiently manage and process data.

For the full SQL script and detailed configuration steps, please refer to the [Environment Setup](sql/environment_setup.sql) in the `SQL` folder of this repository.

