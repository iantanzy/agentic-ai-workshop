---
layout: default
title: Finance Lab 2
parent: Finance Labs
nav_order: 2
---
<!-- ---
layout: page
title: Finance Lab 2
# permalink: /lab2/
nav_order: 3
--- -->
# 🏦 Finance Agent: Automate finance oriented tasks with Agentic AI. (Lab 2: Adding Knowledge Base)

## Use Case Description

In lab 1b, we will add knowledge to our Finance agent in watsonx Orchestrate, and enable it to answer questions based on a knowledge base.

1. Scroll down the screen to the **Knowledge** section:
   ![alt text](../../imgs/imgs_b/Finance_b_step_1.png)

2. Click on **Upload files**. Then click on **Next**:
   ![alt text](../../imgs/imgs_b/Finance_b_step_2.png)

3. Drag and drop the <a href="../pdfs/Late%20Payment%20Policy.pdf" target="_blank" rel="noopener">Late Payment Policy.pdf</a> and click on **Upload**:
   ![alt text](../../imgs/imgs_b/Finance_b_step_3.png)

4. Fill the description as shown below and click on **Save**:
```
This knowledge source is about late payment policy
```
   ![alt text](../../imgs/imgs_b/Finance_b_step_4.png)

5. Wait until the file has been uploaded successfully and double check that it is now shown in the **Knowledge** section:
   ![alt text](../../imgs/imgs_b/Finance_b_step_5.png)

6. Scroll to the **Behaviour** section and update the **Instructions** field:
```
when user asks invoices for a specific contact, get the contact id from list contacts before running list invoices tool one by one for each page.
when asked about pending invoices, iterate over all pages of list invoices tool and find the pending invoices from the whole list. Do not ask for user input. Provide all invoice information such as contact, amount paid or due and due date. Format the answer nicely.
Pending account receivables are those where Type is ACCREC and Status is AUTHORIZED.
The payment policy is in knowledge tool.
```
   ![alt text](../../imgs/imgs_b/Finance_b_step_6.png)

7. Test your agent in the preview chat on the right side by asking the following questions and validating the responses. They should look similar to what is shown in the screenshot(s) below:
```
for which invoices, accounts receivable are pending?
```
![alt text](../../imgs/imgs_b/Finance_b_test_1.png)

```
Based on the payment policy, what action should i take for City Limousines?
```
![alt text](../../imgs/imgs_b/Finance_b_test_2.png)

```
what about Bayside Club?
```
![alt text](../../imgs/imgs_b/Finance_b_test_3.png)