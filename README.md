# llm-guardrails
Data from the LLM Guardrails experiment used to support the article below:

***The Need for Guardrails with Large Language Models in Medical Safety-Critical Settings: An Artificial Intelligence Application in the Pharmacovigilance Ecosystem***

https://arxiv.org/abs/2407.18322


# Data Evaluation for Publication Support

## Folder structure
 - data : Contains final redacted datasets from Phase 1 and 2 of our LLM experiment

## Data File Descriptions

### LLM-Phase 1 Export
  
  **data/llmphase1_final_review.csv**
  *The source and translation fields have been redacted for github storage*
  
  This file contains the following fields:
  
  **Data Fields**
  
  - ReviewID	: Auto-generated database key
  - Case Master ID : Unique Case ID
  - Case Date	: Initial receipt date of the case
  - Reviewer_1 : username of first reviewer	
  - Reviewer_1_Time : time (in miliseconds) of first reviewer	
  - Reviewer_2 : username of second reviewer (should not equal first reviewer)	
  - Reviewer_2_Time : time (in miliseconds) of second reviewer	
  - ExamplePost	: Reviewer felt this was a good post to be highlighted to the team
  - Secondary: Source is clear	
  - Correct assessment?	
  - Translation accuracy	
  - Source has multiple meanings	
  - Source is clear	
  - Source contains contradictions	


### LLM-Phase 2 Export

  Cases that have been completely reviewed should have at minimum (2) row entries (matching on Case master ID). Each case was imported
  into the database and (2) copies were made to insure each case is reviewed twice. The business logic prevents the same user
  from being presented the same Case Master ID twice.  If a case goes through two reviews and the reviewers fail to agree,
  it is flagged for adjudciation and a 3rd party will review. In that case, there will be a 3rd copy of the case made, the fields
  were each reviewer agreed will automatically be populated for the adjudicator's case review. The adjudicator is then forced
  to make a decision on the fields where the reviewers disagreed.
  
  Cases that did not require adjudcation and have 2 reviews completed are then eligible for QC review. QC review is a randomly
  selected process, and the QC process again creates a 3rd copy of the case. All fields are duplicated for the QC reviewer, and 
  they have an opportunity to make changes or updates only to their QC version of the case review.
  
  **data/llmphase2_final_review.csv**  

  These files contain the following fields.
  
  **Data Fields**
  
  - ReviewID	: Auto-generated database key
  - Case Master ID : Unique Case ID
  - QC Case Review : True if this was a QC review of the case	
  - Adjudicated Case : True if this was the adjudicator's review of the case	
  - Case differences : When a case has been submitted as the second time in review, a count of differences between reviewers is calculated and stored here	
  - Case Date	: Initial receipt date of the case
  - Reviewer_1 : Single reviewer per case. For each Case Master ID, this should not be duplicated (require 2 different reviewers)
  - Reviewer_1_Time : time (in miliseconds) of case reviewer
  - Is Original Narartive clear?	: Ranking question scale 1-5
  - Is LLM Narartive clear?	: Ranking question scale 1-5
  - Source contains contradictions	: Yes/No Question
  - LLM contains contradictions	: Yes/No Question
  - Good example case?	: Yes/No Question
  - Completeness of LLM text	: Ranking question scale 1-5
  - Correctness of LLM text	: Ranking question scale 1-5
  - Amount of extaneous information auxillary (not drug safety related) in translated text	: Ranking question scale 1-5
  - Amount of key* (drug safety related) information in the translation not present in the source text	: Ranking question scale 1-5
  - Wrong Drug name or information 	: Yes/No Question
  - Wrong Dosage 	: Yes/No Question
  - Wrong Dates/times	: Yes/No Question
  - Incorrect/missing AE/Wrong Outcome	: Yes/No Question
  - Rechallenge/dechallenge	: Yes/No Question
  - TTO issues	: Yes/No Question
  - Non-sensical Phrases	: Yes/No Question
  - Other Errors	: Yes/No Question
  - Is the case clinically accurate?	 : Yes/No Question

