## S0142 Settlement Data - File Acquisition
### Overview  
All UK power (a.k.a. electricity) generation and consumption operates within a regulated industry.  Companies which Generate usually sell power to Suppliers, who in turn sell power to all Consumers (households or other companies).  

The majority of selling & purchasing is undertaken in advance of actual generation, and can be undertaken up to 1 hour before the actual generation period (known as a settlement period).  Currently a settlement period is 30 minutes in duration (although this may change to 15 minutes to align with Europe at some point in the future).

Because power must be generated and consumed simultaneously in real-time via the grid, the actual MWh purchased and sold may fluctuate from the numbers used in the prior sales and purchase agreemenents.  The process known as Balancing and Settlement can only be executed as a backwards-looking activity in order to give time for the actual generation and consumption figures to be gathered (meter readings of various types) and sent to the Elexon settlement IT system.  This system, known as the SAA (Settlement Administration Agent) then produces data outputs which provides accurate MWh values to enable correct financial settlement between energy market participants.  

</br>

### Requirements 
Acquire the S0142 data files.    
In BSC (Balancing and Settlement Code) parlance, these files are the SAA-I014 Settlement Administration Agent, Interface 14, sub-flows 1 & 2.  Or more commonly called the *settlement report*.  The S0142 files are generated daily, for a number of differing Settlement run types.  They are generated as multi-record format data files and made availiable via an API.

The Elexon SAA has 2 Data APIs:
- Daily File List GET
- Single named File GET

</br>

| # | Functional Requirement |
|:-------------|:--------------|
| FR-1 | Retrieve the daily S0142 files from the Elexon SAA API. |
| FR-2 | Do not ingest duplicate files. |
| FR-3 | Maintain a viewable log of the files that have been ingested. |
| FR-4 | Retain the following information within the file names: </br> Settlement Date / Settlement Run Type / SAA Run Date. |

| # | Non-Functional Requirement |
|:-------------|:--------------|
| NFR-1 | Only use Serverless infrastructure to allow hosting in public cloud environments. |
| NFR-2 | Any failure in API communication should be automatically recovered/retried to avoid the need for manual intervention. |
| NFR-3 | Execution and Storage costs should be minimised, therefore process duplication & complexity constraints may be relaxed. |
| NFR-4 | Duplicate files should not be created and stored. |
| NFR-5 | There are no performance demands, apart from those imposed by Serverless HTTP timeouts. |  


</br>

### Logical Design  
Being agnostic of any technology or design patterns, the logical design is represented by the diagram:  

![Logical Design Diagram](images/acquisition-Logical.svg)

### Azure Component Design



