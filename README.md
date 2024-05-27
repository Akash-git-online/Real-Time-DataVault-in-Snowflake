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

## Data Vault - Architecture
![Data Vault Refrence Architecture](image/DataVault-Architecture.png)
