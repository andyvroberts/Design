## Insurance Broker view of Underwriting - CDM


### Relationship Verb Phrases
Business rules within a conceptual data model can be stated by expansion of the verb phrases, the cardinality, and the optionality of relationships.

|From|To|Business Rule|
|:-|:-|:-|
|Binding | Binding Authority | A Binding is **legal within** an active Binding Authority.<br/>*A Binding Authority delegates the Carrier authorisation for one or more Policy Bindings*.
|Binding | Cover-Holder | A Policy Binding is **completed internally** by a Cover-Holder. <br/>*A Cover-Holder performs one or more Policy Bindings.* |
|Sub Cover-Holder | Binding | A Sub Cover-Holder may have **quotes & submissions** which **result in** Policy Bindings.<br/>*A Binding may result from actions of a customer facing Sub Cover-Holder.* |


### Data Entity Definitions

|Entity|Meaning|Synonyms|
|:-|:-|-:|
|Binding Authority|A legal agreement between the Carrier and the Cover-Holder, or the Cover-Holder and the Sub Cover-Holder.<br/>The authority is specific to circumstances and defines the products, limits, territories, referral criteria, regulations, levels of assumed risk and/or the split between Carriers for any underwritten Policy. The Carrier holds the risk and must pay-out following a valid Claim.<br/>The term *"Binding Authority"* is the name given to this agreement where the Carrier is in the London Market.|Facility<br/>Binder|
|Carrier|The legal entity or organisation that holds the Risk for an insurance policy.  The Carrier must pay out after a successful Claim.  Each Carrier assesses the performance of the Underwriters through the Loss Ratio.  Bonus values may be paid to Underwriters (Brokers / Cover-Holders) who produce a lower then expected Loss ratio.|Partner<br/>Insurer<br/>Market<br/>Consortium|
|Cover-Holder|The Cover-Holder acts as the agent of the insurance partner (the Carrier), who *"delegates authority"* and responsibility for the underwriting to the Cover-Holder.<br/>The Cover-Holder also acts as an intermediary between the Carrier and the Sub Cover-Holders/Brokers.|Agent|
|Sub Cover-Holder|The customer facing counterparty who sells products. This may be a high-street Broker, a national Broker or a group sales division within an organisation.  A Sub Cover-Holder *"takes the product to market"*. <br/>If the Sub Cover-Holder is a Broker then they will have access to multiple markets so as to provide options and choices.<br/>The Sub Cover-Holder obtains quotes which may turn into a sale (new business) if taken up.  That product is *"written"* by the insurance process known as Binding.|Broker<br/>Sub-Agent
