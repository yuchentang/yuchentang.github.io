---
sort: 1
---


# OLTP v.s. OLAP

Two types of data processing systems

- Online Analytical Processing (OLAP)
- Online Transaction Processing (OLTP)

The main difference between OLAP and OLTP: Processing type. 
The main distinction between the two systems is in their names: analytical vs. transactional. Each system is optimized for that type of processing.

OLAP is optimized for conducting complex data analysis for smarter decision-making. OLAP systems are designed for use by data scientists, business analysts and knowledge workers, and they support business intelligence (BI), data mining and other decision support applications.

OLTP is optimized for processing a massive number of transactions. OLTP systems are designed for use by frontline workers (e.g., cashiers, bank tellers, hotel desk clerks) or for customer self-service applications (e.g., online banking, e-commerce, travel reservations).

Different OLTP databases can be the source of aggregated data for OLAP, and they may be organized as a data warehouse. OLTP, on the other hand, uses a traditional DBMS to accommodate a large volume of real-time transactions.

|             |OLTP	 |OLAP  |
|:------------|:-----|:-----|
|Process	|It is an online transactional system. It manages database modification. |OLAP is an online analysis and data retrieving process.|
|Method	|OLTP uses traditional DBMS.	|OLAP uses the data warehouse.|
|Query	|Insert, Update, and Delete information from the database.  |Mostly select operations|
|Table	|Tables in OLTP database are normalized.  |Tables in OLAP database are not normalized.|
|Source	|OLTP and its transactions are the sources of data.  |Different OLTP databases become the source of data for OLAP.|
|Response time	|It’s response time is in millisecond.  |Response time in seconds to minutes.|
|Usefulness |It helps to control and run fundamental business tasks.  |It helps with planning, problem-solving, and decision support.|
|Purpose |Designed for real time business operations.  |Designed for analysis of business measures by category and attributes.|

# Star Schema

The star schema consists of one or more fact tables referencing any number of dimension tables.