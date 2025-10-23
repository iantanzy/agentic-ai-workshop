---
layout: page
title: Lab 2
# permalink: /lab2/
nav_order: 3
---
# 🧑‍💼 Lab 2: Agentic RAG with HDB Annual Report 
    
In this lab, we will build a HDB Annual Report agent in watsonx Orchestrate to answer questions based on a knowledge base. This agent retrieves relevant information from documents to answer user queries. This lab is suited for Business Users.


## Step by step instructions to build the HDB Agent:

1. When you launch watsonx Orchestrate, you'll be directed to this page. Click on the hamburger menu in the top left corner:

    ![image](./website/imgs/imgs_lab2&3/step1.png) 

1. Click on the down arrow next to **Build**.  Then click on **Agent Builder**:

    ![image](./imgs/imgs_lab2&3/step2.png)

1. Click on **Create agent +**:

    ![image](./imgs/imgs_lab2&3/step3.png)

1. Select "Create from scratch", give your agent a unique name (make sure to identify yourself by your initials or name, since this is a shared instance), e.g. "[Your Initial] HDB Agent", and fill in the description as shown below: 

    ```
    You are an agent who handles employee queries from the HDB Annual Report.  You provide short and crisp responses, keeping the output to 200 words or less. 
    ```  

    Click on **Create**:

    ![image](./imgs/imgs_lab2&3/hdb_step4.jpg)

## Lab 2A: Agentic RAG with HDB Annual Report 

1. We are going to build a knowledge base for the agent. Scroll down the screen to the **Knowledge** section and click on "Choose knowledge".

    ![image](./imgs/imgs_lab2&3/hdb_step5.jpg)

1. Choose "Upload files" and click "Next".

    ![image](./imgs/imgs_lab2&3/hr_step_uploadfile.png)

1. Drag and drop the [AR2020.pdf](./pdfs/AR2020.pdf) and click on **Next**:

    ![image](./imgs/imgs_lab2&3/hdb_step6.jpg)

1. Copy the following description into the **Description** section and click **Save**:

    ```
    This knowledge base contains the Housing Development Board (HDB) Annual Report for 2019. 
    ```

    ![image](./imgs/imgs_lab2&3/hdb_step7.jpg)

    The knowledge base will take some time to create. After the knowledge base is done, you will be brought back to the Agent Builder UI.

    ![image](./imgs/imgs_lab2&3/hdb_step8.jpg)

1. Click into the **Edit knowledge settings** section. You can explore the settings like: Retrieval confidence threshold, Generated response length, Response confidence threshold, Maximum Search Results and number of Citations. There is also a Dynamic mode. Click back into "Classic" and leave it as default settings by clicking on "Cancel". 

    ![image](./imgs/imgs_lab2&3/hdb_step9.jpg)

1. Scroll down to the **Behavior** section. Insert the instructions below into the **Instructions** field:

    ```
    Use your knowledge base to answer general questions about HDB Annual Report for year 2019/2020.  
    ```

    ![image](./imgs/imgs_lab2&3/hdb_step10.jpg)

1. Test your agent in the preview chat on the right side by asking the following questions and validating the responses.  They should look similar to what is shown in the screenshot(s) below:

    ```
    What are the main loans that finance HDB's operations?
    ```

    ![image](./imgs/imgs_lab2&3/hdb_step11.jpg)

1. You can try the following sample questions as well:

    ```
    Summarise the land reclamation projects ongoing and successfully completed in the past year according to AR2020
    ```
    ```
    According to the AR2020.pdf document, how many international awards were attained for the year 2019?
    ```
    ```
    List the buildings that received the BCA Construction Excellence Award 2019 (Residential Buildings – Below $1,800 /m2 Category)
    ```

    You can also try:
    1) to switch the knowlege settings to "Dynamic"
        ![image](./imgs/imgs_lab2&3/hdb_step12.jpg)

    2) to change the underlying LLM
        ![image](./imgs/imgs_lab2&3/hdb_step13.jpg)
    

    You have now built an AI Agent in under 10 minutes. Notice that you might not get all the correct answers. We will improve the search and build a better agent in Lab 2B below!

## **🎉🎉🎉Congratulations! You've built your first Agentic RAG Agent.**


## Lab 2B: Agentic RAG with Enterprise Search

In this part of the lab, we will change the source of the knowledge base and deploy the agent.

1. Click on Change source in the "Knowledge source" section
        ![image](./imgs/imgs_lab2&3/hdb_step14.jpg)

1. Select Elasticsearch and click "I understand"
        ![image](./imgs/imgs_lab2&3/hdb_step15.jpg)

1. Copy and paste in the existing Elasticsearch url we have provisioned. After filling the necessary fields, click Next.

    ```https://ceae3fbf-980c-4013-989d-d7f05210908e.bn2a2uid0up8mv7mv2ig.databases.appdomain.cloud:32577```

    Choose API Key is the authentication type. The API key will be shared with you separately.
        ![image](./imgs/imgs_lab2&3/hdb_step16.jpg)

1. Specify the Elasticsearch index and fill up the fields accordingly and click "Next". 
    ```
    hdb_docling_enriched_1500
    ```
    ![image](./imgs/imgs_lab2&3/hdb_step17.jpg)

1. In your agent, you should now see that the knowledge source has been updated to Elasticsearch 

    ![image](./imgs/imgs_lab2&3/hdb_step18.jpg)

1. In your agent preview on the right, you can try out your newly improved agent 

    ![image](./imgs/imgs_lab2&3/hdb_step19.jpg)

    - Optional: You can also edit the Welcome Message, Quick start prompts, Agent style

1. Now, you are ready to Deploy your agent. Click on Deploy in the top right corner

    ![image](./imgs/imgs_lab2&3/hdb_step20.jpg)

    - Click on Deploy after checking the agent details
    ![image](./imgs/imgs_lab2&3/hdb_step21.jpg)

1. Lets view the agent from a user perspective. Click on the hamburger menu in the top left corner and select "Chat"

    ![image](./imgs/imgs_lab2&3/hdb_step22.jpg)

    - Select your agent that you have just deployed
    ![image](./imgs/imgs_lab2&3/hdb_step23.jpg)

1. You can ask more questions or chat with your agent. Don't forget to expand "Show Reasoning" or "View Source"

    ![image](./imgs/imgs_lab2&3/hdb_step24.jpg)

    - Try out the other sample queries from: [Sample Queries](https://jordansimyj.github.io/techxperience/sample_queries.html)

## **🎉🎉🎉Congratulations! You've connected the Agentic RAG Agent with an Enterprise Search knowledge base and deployed it.**

The search results should be more accurate now.

