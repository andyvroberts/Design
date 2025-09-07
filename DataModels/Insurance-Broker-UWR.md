## Insurance Broker view of Underwriting - CDM
The conceptual data model acts as a concept map, describing how a Broker organistaion views and understands Underwriting in the context of its own counterparty relationships and high-level business processes.  

This data model was created using Information Engineering notation and follows its conventions for relationships and phrases.  
<br/>

### Relationship Phrases
Business rules within a conceptual data model can be stated by expansion of the phrases placed on entity relationships.  IE notation only expresses single direction phrasing, but a *reverse phrase* has been added for completeness in the table below.  

|From|To|Business Rule|
|:-|:-|:-|
|Binding | Binding Authority | A Binding is **legal within** an active Binding Authority.<br/>*A Binding Authority delegates the Carrier authorisation for Policy Binding*.|
|Binding|Capacity Agreement |Financial Binding **conditions depend on** the terms of the Capacity Agrement.<br/>*A Capacity Agreement specifies the finacial limits which allow Binding .* |
|Binding | Cover-Holder | A Policy Binding is **completed internally** by a Cover-Holder. <br/>*A Cover-Holder performs one or more Policy Bindings on behalf of a Carrier.* |
|Business Distribution|Transactional Model|Business Distribution can be **implemented by the** Transactional Model.<br/>*The Transactional Model includes all responsibliites for Business Distribution.*|
|Cover-Holder|Carrier|A Cover-Holder provides **volume policy placement for** a Carrier.<br/>*A Carrier provides the financial Capacity for use by a Cover-Holder.*|
|Cover-Holder|Transactional Model|A Cover-Holder has administrative **activities according to** the Transactional Model.<br/>*The Transactional Model scopes the required business processes for a Cover-Holder.*|
|Carrier|Business Team|A Carrier **targets capacity to** specific Business Teams.<br/>*A Business Team writes Policies to meet a Carriers planned targets.*|
|Delegated Model|Business Distribution|The Delegated Model defines **split responsibilities** for Business Distribution.<br/>*Business Distribution can be implemented by the Delegated Model.*|
|Sub Cover-Holder | Binding | A Sub Cover-Holder **sometimes performs** Policy Bindings on behalf of the Cover-Holder.<br/>*A Binding may result from the actions of a delegated Sub Cover-Holder.* |
|Sub Cover-Holder|Delegated Model|A Sub Cover-Holder has administrative **activities according to** the Delegated Model.<br/>*The Delegated Model scopes the required business processes for a Sub Cover-Holder.*|


### Data Entity Definitions
Descriptions of Data Entities in a conceptual model are essential to provide meaning and context.  
  
|Entity|Meaning|Synonyms|
|:-|:-|-:|
|Binding Authority|A legal agreement between the Carrier and the Cover-Holder, or the Cover-Holder and the Sub Cover-Holder.<br/>The authority is specific to circumstances and defines the products, limits, territories, referral criteria, regulations, levels of assumed risk and/or the split between Carriers for any underwritten Policy. The Carrier holds the risk and must pay-out following a valid Claim.<br/>The term *"Binding Authority"* is the name given to this agreement where the Carrier is in the London Market.|Facility,<br/>Binder|
|Business Distribution|The organisational entity where activities such as Policy Binding, issuing Documentation, and performing Policy administration is accomplished.<br/>Business Distribution is either internal to the receiving Cover-Holder (the Transactional Model) or delegated to a third party Sub Cover-Holder (the Delegated Model).||
|Business Division|||
|Business Team|A specialist team with a Business Division.  The team can play the role of Underwriter, Cover-Holder and Administrator for lines of business.<br/>For example, a FINPRO Business Team will contain Underwriting expertise within the PI (Professional Indemnity) and D&O (Directors and Officers) lines.  A Commercial team may specialise in insurance products for Commerical Properties and a Real-Estate team may do the same for non-Commercial.||
|Capacity Agreement|Occurs between the Carrier and the Underwriter to set financial risk limits for binding Policies. These are specific to the financial capacity of a Carrier, and may exist as a component within other agreements such as a Binding Authority.|Binding Authority|
|Carrier|The legal entity or organisation that holds the Risk (has the Capacity) for an insurance policy.  The Carrier must pay out after a successful Claim.  Each Carrier assesses the performance of the Underwriters through the Loss Ratio.  Bonus values may be paid to Underwriters (Brokers / Cover-Holders) who produce a lower then expected Loss ratio.|Partner,<br/>Insurer,<br/>Market,<br/>Consortium|
|Cover-Holder|The Cover-Holder acts as the agent of the insurance partner (the Carrier), who *"delegates authority"* and responsibility for the underwriting to the Cover-Holder.  Usually, the Cover-Holder provides either the processing volume or market specific expertise to Carriers, who do not have the organisational resources, but do have the financial Capacity.<br/>The Cover-Holder may act as an intermediary between the Carrier and the Sub Cover-Holders/Brokers.<br/>Usually a Cover-Holder is within an organisation which is also a Broker *and* one or more specialised Sub Cover-Holders.  Therefore, it is often important to understand the internal or external processing responsibilities defined by the Business Distrubution model.|Agent,<br/>MGA|
|Delegated Model|The Delegated Business Distribution Model outsources certain business processes to other organisations.  All resulting processes are undertaken by third parties, and information flow must be obtained through the use of the Bordereaux mechanism.<br/>Carriers *delegate authority to Cover-Holders, who then delegate authority to Sub Cover-Holders*.  The Sub Cover-Holder Underwriters bind the Policy and issue Documentation.  The Cover-Holder usaully selectively monitors some activities of the Sub Cover-Holder.|MGU<br/>Model|
|Sub Cover-Holder|The customer facing counterparty who sells products. This may be a high-street Broker, a national Broker or a group sales division within an organisation.  A Sub Cover-Holder *"takes the product to market"*. <br/>If the Sub Cover-Holder is a Broker then they will have access to multiple markets so as to provide options and choices.<br/>The Sub Cover-Holder obtains quotes which may turn into a sale (new business) if taken up.  That product is *"written"* by the insurance process known as Binding.|Broker,<br/>Sub-Agent|
|Transactional Model|The Transactional Business Distribution Model retains all business processes internally within the parent organisation.  All resulting processing and information flow are retained within internal systems.<br/>Carriers *delegate authority to the Cover-Holders*, who utilse their own Underwriting teams to perform Policy Binding and issue Documentation.|MGA<br/>Model|
