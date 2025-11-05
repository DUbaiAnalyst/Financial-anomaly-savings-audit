# Financial-anomaly-savings-audit
## Project Objective & Scope
The primary objective of this project was to move beyond traditional reporting and develop a data-driven model capable of proactively detecting and quantifying two critical risks within the supply chain. By build a smart, automated system that acts like a hawk, ready to instantly sniff out two major, recurring issues in the supply chain that are draining the firm’s bank account. These are:
1.	Financial Anomalies (Overcharges): Flagging individual transactions where shipping costs were statistically unjustified. This is about flagging transactions where shipping costs were statistically out of the normal range. If Carrier A suddenly charges us triple for a route they usually run cheap, that's a massive red flag, and we catch it automatically.
2.	Operational Anomalies (Quality Risk): Identifying suppliers and products with statistically high defect rates, regardless of official inspection status. This isn't just about money, it's about our reputation, too. We're spotting suppliers whose stuff keeps breaking, failing quality checks, or showing defect rates that are totally sketch.

The ultimate goal is to provide the firm with a Savings Prioritization Hub that translates complex statistical findings into clear, actionable business insights, directly linking cost anomalies to specific accountable parties (Suppliers and Carriers). The analysis covered 100 sample shipment transactions, evaluating key fields including shipping costs, Cost per unit shipped, Defects rate, and operational fields such as, infection results, Supplier name, and Shipping carriers. The resulting dashboard allows for interactive analysis across all major dimensions, including product type, Location, etc.

## Project process

First, I had to make the data clean and structured. The initial dataset was transformed into a structured Excel Table to enable Structured References for stability. Key steps include:
1.	Using power query, columns that weren’t required were deleted, Column like the price column that only tells us how much the product is worth and not how much shipping service should cost, and it is irrelevant to what the carrier should charge us.
2.	Other column with space where standardized using snake_case conversion (e.g., shipping_costs)
3.	Also, column like shipping price, revenue generated, and other money related column were converted to Accounting from General. While other numbers like defect rate were converted to decimal.
4.	After these processes, I loaded my cleaned data table into excel, then created four (4) more column (Cost per unit shipped, Percentage Defects rates, cost anomaly flag, and quality risk flag)
5.	Metric creation: Cost per unit shipped was created to calculate our normalizes prices across varying orders. Using the formula (Shipping cost/Number of products sold). 

I move to our anomaly detection models. Two distinct statistical models were established on a dedicated Benchmarks sheet to create data-driven thresholds for flagging risks. These are:
1.	Financial Anomaly: These are the cash the firm are losing. We checked what each carrier usually charges and set the alarm for anything that was 2 times higher than their normal variation. By using a threshold formula rule which is Average + 2*STDEV.
2.	Operational Quality Risk: I set a universal, lower alarm (1.5 times normal) for defect rates. By using a threshold formula rule which is Average + 1.5*STDEV.

I lowered the danger line bar for defects rates to 1.5 of the standard deviation because the consequences of a quality failure is often more severe and less financially quantifiable than a billing error. This whole setup uses a smart formula (IF(XLOOKUP(...))) that acts like a tiny genius. It automatically knows which carrier's "normal" price to check against, making the whole thing straightforward.

## Key Prioritization Questions (KPQs)
The analysis was designed to answer the following critical questions for leadership and procurement teams:
1.	What is the quantifiable financial leakage found in the sample, and what is the potential annual savings opportunity when scaled?
2.	Where is the risk concentrated? Which Carriers and Suppliers are responsible for the highest volume of financial overcharges?
3.	Which vendors pose the highest Dual Risk (a combination of both high financial overcharges and high quality defect rates)?
4.	How can I use statistical rigor to differentiate between a normal cost fluctuation and a guaranteed overcharge?

## Insights
1. I discovered that 7% of the transactions in the sample were flagged as statistically significant anomalies, resulting in a total recoverable financial leakage of $37.88. This finding immediately proves the value of the detection model. When I extrapolate this 7% anomaly rate across the estimated 10,000 annual shipments, the immediate savings opportunity exceeds $3,800 per year in recovered, overcharged funds. This is "free money" that can be recovered by simply challenging the highlighted invoices.
2. My analysis strongly confirms that both financial and operational risks are dangerously centralized among a few key partners, which simplifies the resolution process significantly. The total overcharge amount of $37.88 is overwhelmingly concentrated in two carriers: Carrier C is responsible for the largest portion of leakage at $15.35, closely followed by Carrier A at $14.48. Addressing these two carriers' contracts is the most critical financial intervention.
3. By combining the financial and quality data, I identified Supplier 5 as the highest priority vendor requiring immediate action. Supplier 5 is the top offender for financial overcharges, contributing $8.25 to the total leakage, while simultaneously being flagged for a high volume of quality defects. This combined risk profile makes Supplier 5 the single greatest threat to both profit margins and brand reputation.
4. To ensure I was flagging guaranteed anomalies and not just normal price fluctuations, I employed two distinct thresholds using the Standard Deviation ($\text{STDEV}$)—the statistical measure of typical price variation. For Financial Overcharges, I used the $\mathbf{\text{Average} + 2 \times \text{STDEV}}$ rule, which provides 97% confidence that any flagged cost is a systematic error or rip-off. For Quality Defects, I used a more sensitive, proactive threshold of $\mathbf{1.5 \times \text{STDEV}}$. I chose a lower threshold for quality because the financial and reputational cost of shipping a faulty product is so high, it necessitates an early warning alarm to prevent failure before it becomes catastrophic.

## Conclusion and recommendation
The Supply Chain Savings Prioritization Hub successfully met its objectives by transforming raw data into clear, prioritized business intelligence. The key conclusion is that the financial and operational risks are not widespread but are dangerously centralized within a few key relationships. The $38 (7%) in savings from a mere 100 samples suggests a massive potential recovery opportunity when scaled across the entire network. If we blow that up to a year of 10,000 shipments, we're talking about $3,800+ in free money we can recover annually. 

The immediate focus must be on leveraging the dashboard's prioritization logic:
1.	Immediate Contract Renegotiation: Initiate negotiation with the top-ranked supplier, Supplier 5, as they represent the highest overall combined risk (Cost and Quality).
2.	Logistics Performance Review: Launch an immediate internal audit on the contracts, routing, and handling procedures of Carrier C and Carrier A to resolve the identified financial and operational systemic failures.
Proactive Monitoring: Integrate the anomaly detection model for continuous, real-time auditing, moving the organization from reactive problem-solving to proactive cost control.
