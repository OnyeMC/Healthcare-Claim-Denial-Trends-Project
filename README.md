# Healthcare-Claim-Denial-Trends-Project
## Claim Denials Project
Dealing with insurance denials can be a major burden on healthcare systems, as they can negatively impact the organization significantly. Not only do they decrease revenue for the organization, but they also take away time and resources in order to appeal the claim. Denied claims also put more financial burden on patients, significantly decreasing the patient experience. This issue is especially concerning as the number of healthcare claim denials has been increasing in recent years (Frias, 2025). Analyzing patterns in claim denials is important for identifying and resolving issues so that the healthcare organization can minimize the amount of denials. This project uses a synthetic dataset to identify trends in claim denials to find potential areas for improvement. Excel will be used to analyze the data.

## Cleaning Data
Power Query was used to clean the dataset after importing it into Excel. Although the synthetic dataset was mostly clean and had no duplicates/missing information, I wanted to make some additional changes for clarity, as well as to make the data more realistic.
* Removed unneeded columns (Allowed Amount, Follow-Up Required, AR Status)
*	Changed the Date of Service column to only display the name of the month since all claims were from 2024
*	Removed Self-Pay rows
*	Changed Claim Status & Outcome column names to Initial Claim Status and Final Claim Status, respectively
*	Replaced the Reason Code column with a new column that removes reasons for claims that have the “Paid” status initially and finally
*	Replaced the values in the Final Claim Status column with “Paid” if the Initial Claim Status column had “Paid”
*	Replaced the Paid Amount column with a column based on Final Claim Status
    *	Denied = 0
    *	Partially Paid = Initial Paid Amount value
    *	Paid = Billed Amount value
*	Added a Remaining Balance column by subtracting Paid Amount from Billed Amount
*	Changed Billed Amount/Paid Amount/Remaining Balance data types to currency & changed Procedure Code data type to text

## Data Analysis
### 1.	Claim Denial Rates
The initial and final denial rates were first calculated to examine how well the hospital was performing.
* Around 33% of claims were initially denied from May to September. After the appeal process, around 30% of denials were partially or fully resolved, making the final denial rate 22.8%. Both these denial rates are significantly higher than the industry benchmark of 16–20% initially and 2–5% finally (Corcoran, 2026). June had the highest initial denial rate, while May had the highest final denial rate. September had the lowest denial rate both initially and finally. 
* Throughout this time, the overall trend for denials decreased both initially and finally.
<img width="926" height="114" alt="image" src="https://github.com/user-attachments/assets/864fdf01-12f7-48de-9694-e4675edf9464" />

### 2.	Total Costs
The total costs due to lost revenue and administrative burden to appeal claims were also calculated to determine the financial impact on the hospital. To determine the administrative burden to appeal claims, an estimated average cost per appeal of $44 was used (Corcoran, 2026). 
* On average, the hospital lost around $12,420.80 due to denied claims and $2,182.40 from appeal costs per month. In total, the average cost per month due to denials comes to be $14,603.20.
<img width="564" height="104" alt="image" src="https://github.com/user-attachments/assets/f328d729-b6cc-44b3-b6db-d046bb6a9561" />

### 3.	Denial Reasons
The reasons why claims were denied were investigated to discover which areas in the hospital’s workflow were causing the most issues.
* On average, the top 3 biggest reasons why claims were initially denied were due to missing authorization, incorrect billing information, or patient eligibility issues. After the appeal process, these three remain the top reasons why claims are denied.
<img width="929" height="136" alt="image" src="https://github.com/user-attachments/assets/bc17b03e-bbb9-4bd8-acf9-5cbdbbe86e7f" />

### 4.	Procedure Codes & Diagnosis Codes 
Procedure & diagnosis codes were examined to find any common billing errors that may be occurring.
* On average, most denied claims due to billing errors had the CPT code 99221 (Under New or Established Patient). While the average number of denied claims decreased after appealing for most CPT codes, the average number of denials actually increased for claims with the CPT codes 99213 (Under Established Patient), 99214 (Under Established Patient), and 99223 (Under New or Established Patient), although very few claims with these codes were denied each month.
* Only three diagnosis codes were used in claims that were denied after appeal: A01.0 (Typhoid fever), A17.1 (Meningeal tuberculoma), and A16.9 (Respiratory tuberculosis unspecified, without mention of bacteriological or histological confirmation). The claims for A01.0 and A16.9 were still denied after appeal, while the claim that was originally denied with A17.1 was successfully approved. Since very few denials due to billing errors included specific diagnosis codes, the diagnosis codes are most likely not a major area of concern.
<img width="893" height="165" alt="image" src="https://github.com/user-attachments/assets/f8158513-a660-44af-9ab7-8acb103b641c" />
<img width="528" height="93" alt="image" src="https://github.com/user-attachments/assets/b64d7db9-fe9c-41e5-919a-b2929142601d" />

### 5.	Insurance Type
Finally, insurance types were examined to determine if there was a correlation between specific insurance types and eligibility or authorization issues. 
* On average, most denied claims due to a missing authorization were from patients who had Medicare. Denied claims due to eligibility issues were mostly due to patients with Medicaid.
<img width="928" height="183" alt="image" src="https://github.com/user-attachments/assets/259f4eac-d7fe-4b06-a44d-5edd2b1b814f" />

All key findings are summarized in the following dashboard:
<img width="641" height="339" alt="image" src="https://github.com/user-attachments/assets/24f1e0e4-df1e-4d27-b6b4-d7a41b238006" />

## Conclusions
Although denial rates have been declining at this hospital, improvements in several key areas can ensure that this trend continues. Since most denials are due to either missing authorization, incorrect billing information, or patient eligibility issues, improvements should focus on these key issues. Since the most common CPT codes involved in denials were all for similar conditions, it may be beneficial to provide medical coders with additional guidance on the differences between these CPT codes. The hospital may also benefit from setting up payer-specific flags. An authorization flag could be set for patients who use Medicare, and an eligibility flag for those who use Medicaid. These recommendations will ensure that fewer claims are denied in the future.

## References
1.	Abuthahir1998. Synthetic Healthcare Claims Dataset. Kaggle. https://www.kaggle.com/datasets/abuthahir1998/synthetic-healthcare-claims-dataset. 
2.	Corcoran, K. (2026, Apr 4). The Denial Dilemma: Decoding Denials, Measuring Performance, and Calculating the True Cost. Unislink Medical Billing Services | RCM. https://unislink.com/rcm-best-practices-blog/the-denial-dilemma-decoding-denials-measuring-performance-and-calculating-the-true-cost/#:~:text=The%20Calculation,expense%20caused%20by%20claim%20rework.
3.	Denomy, M. (2025, March 18). Hospital Denials Benchmarks | How to Reduce Denials for Pro Fee Charges. Medaptus. https://www.medaptus.com/blog/hospital-denials-benchmarks-how-to-reduce-denials-for-pro-fee-charges/#:~:text=How%20to%20Reduce%20Denials%20%7C%20Improving,errors%20before%20submitting%20for%20billing.
4.	Frias, A. (2025, November 4). Why Healthcare Claim Denials Are Increasing. Enable Comp. https://enablecomp.com/resource/blog/why-claim-denials-are-on-the-increase/.
