## UK Property: Prices Paid Data 
The UK Property Prices Paid dataset published by the UK ONS requires just a simple design for an Analytics based Dimensional Data Model.  
https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads  
https://www.gov.uk/guidance/about-the-price-paid-data#explanations-of-column-headers-in-the-ppd  

The CSV data file has this structure.

| Column | Type | Example |
|- |- |- |
|ID |GUID | {34222872-E65C-4D2B-E063-4704A8C07853} |
|Price |Double - GBP Amount| 1750000 |
|Price Date|DateTime|21/11/1998 00:00:00|
|Postcode|String - Postal Sorting Code|MK3 9AU|
|Property Type|Char |D, S, F, T, O|
|New Build Flag|Char - Yes or No |Y, N|
|Land Ownership Type|Char |F, L |
|PAON|String|Flat 3a|
|SAON|String|45|
|Street|String|Elmtree Road|
|Locality|String|Ashburnham|
|Town|String|Ashburnham|
|District|String|Waltham Under Lyme|
|County|String|Essex|
|PPD Category|Char |A|
|Record Type|Char |A, C, D|

<br/>

### Dimensional Model Introduction 
Within Relational Database Management Systems (RDBMS) such as Oracle, DB2 or SQL Server, etc, a dimensional data model is a relationaly organised table structure, optimised for aggregation and grouping operations.  The model is focused on the production of Measures for business domains, and therefore the underlying data values be can presented with differing names and formats.   

Before creating the model for the Prices Paid data, we will describe the most important Dimensional aspects and design decisions.

#### Fact
A Fact is usually some numerical value to which [Analytic functions](https://en.wikipedia.org/wiki/Analytic_function), or more commonly, Database Functions such as MAX, AVG, SUM, etc. can be applied.   
For the Price Paid data, the only fact in the file is the property **Price**.  

#### Dimension
A Dimension is additional, related, or relevent business information that is associated to a Fact.  For example, the **Month** a property was sold, or the Geographic **Region** of that property.  
For the Price Paid data, all the items except for the Price (a Fact). ID (no business meaning) and Record Type & PPD Category (technical meta-data) are Dimension values.  

#### Measure
Dimensions are used to filter (exclude or include) Facts, and performing such an operation usually creates measures.  For example, **Total Monthly Sales**.  In this case, the Price is the Fact and the Month of the Price Date is the Dimension.  
There are many possible measures that can be created.  Generally, the greater the number of dimensions, the greater the variety of measures that can be calculated.  

#### Data Marts
There are many definitions for data-marts as physical database structures, but the one characteristic they all have in common is that they contain **Subject-Specific** data.  Depending upon the requirements for the uses of Price Paid data, the mart can be modelled in several ways:  
- As a single dimensional model (semantic)
- As a small relational model (storage optimised)
- As a single de-normalised entity (a wide table for Lakehouse file formats)

<br/>

### Data Mart Design
Equally important consideration must be given to the fundamental purpose of the model and how it will be used in its physical implementation.

#### Batch Processing
In terms of use-cases, many Dimensional data models located within relational databases are directly queried by by automated processes and jobs.  These types of models usually exist for large-scale batch processing as an intermmediate stage between the source data and some product of calculated values.  A good example is the creation of multiple data marts supporting financial risk calculations.

#### Analytic Processing
Other Dimensional models are required for reporting or other end-user analytics (MI/BI).  In these cases it is common for Dimensional models to also be loaded into consumer friendly tools such as Tableau, Power BI/Fabric, Qlik, Looker, etc, where they can be given a semantic overlay to make them business domain specific. There are two main possibilities for analytics:  
1. The database will be queried directly by users (the semantic model is in the Data Mart).
2. The database will be queried by an Analytic tool (the semantic model is in the Analytic tool).

#### Dimensional vs. Dimensional (semantic)
If the Dimensions within the model require a semantic interpretation, this is often provided by business domain specific Reference or Master data.  
In the Prices Paid file, the following data items may require semantic explanation:
- Property Type (D = Detached S = Semi-Detached / T = Terraced / F = Flats, Maisonettes / O = Other)
- Land Ownership Type (L = Leasehold / F = Freehold)

For (non-human) data processing purposes, the semantic values are not required and can be ignored.  But if semantic interpretation is required, then the data model must be extended to contain the UK Property domain specific (semantic) descriptions.  


#### Analytics Decison Matrix

| Option | Processing Purpose? | Semantics Required? | Users Access DB? | Data Mart | Analytic Tool |
|- |- |- |- |- |- |
|1|Batch |No | No | Dimensional | not required |
|2|Analytics |Yes | No | Relational <br/> De-normalised | Dimensional (semantic) |
|3|Analytics |Yes | Yes | Dimensional (semantic) | Dimensional (semantic) |
|4|Analytics |No | Yes | Dimensional | not required |

Option 1 requires a data mart that is only required for processing data according to some pre-defined calculations which would be optimised by using a Dimensional model.  These processes are only intended to prepare the data for usage elsewhere.  

Option 2 requires two models.  The data mart is only required as a data store that must contain the source values.  The analytic tool will use the data mart to construct a Dimensional model with any additional semantics required to satisfy user queries.

Option 3 requires only one model, but implemented twice.  The Dimensional (semantic) model can be accessed directly through the data mart, or via an analytic tool which loads (or updates) data from the mart.

Option 4 requires a Dimensional model for users to query, but only the originally provided data is required, no semantic enrichment is neccassery.  

<br/>

### Data Processing Design
