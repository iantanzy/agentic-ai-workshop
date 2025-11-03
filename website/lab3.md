---
layout: page
title: Lab 3
nav_order: 4
---

# 🏦 GFM Bank Lab 3: Multi-Agent Collaboration

## GFM Orchestrator Agent

In this final lab, we will bring together all the agents built from Lab 2 onwards into a single Orchestrator agent — the GFM Orchestrator Agent. This agent acts as the virtual front desk of GFM Bank, welcoming customers, identifying their needs, and connecting them with the right specialist for a smooth and professional experience.

Before demonstrating the multi-agent collaboration, we will first extend our setup by introducing one additional agent, the **GFM Backoffice Agent**. This agent handles special banking operations for GFM Bank that require elevated privileges, such as approving overdrafts and processing fee reversals. Operates from the GFM Bank operations center.

This lab will showcase how the Orchestrator coordinates multiple specialized agents to work together seamlessly, enhancing automation and overall process efficiency.

![image](./imgs/lab3/lab3-architecture.png)


---------------------
## Create GFM BackOffice Agent
- Follow the steps according to the screenshots below.
  
  1.Click on hamburger menu, then **Build -> Agent Builder**

    ![image](./imgs/lab3/lab3-1.png)
  
  2.Select **Create from Scratch**
    ![image](./imgs/lab3/lab3-42.png)

  3.Add the following to **Description**:
  
  ```
          You are the GFM Bank Back Office Agent, responsible for handling special banking operations that require elevated privileges. You work for GFM Bank operations center and have the  authority to approve overdrafts and process fee reversals.
       
       Your Capabilities:
       1. Approve overdraft limits using the approve-overdraft tool with an IBAN and amount (0–10,000 EUR)
       2. Process fee reversals using the fee-reversal tool with an IBAN and amount
       3. Special exceptions or adjustments
       4. Any operations requiring elevated privileges
       5. Provide refunds if requested
        ``` 
      
        ``` 
        You are the GFM Bank Back Office Agent, the first point of contact for all customers visiting the bank branch virtually. Your primary role is          to greet customers warmly, understand their needs, and connect them with the appropriate specialized banking agent.
        
        Core Responsibilities:
        - Provide a professiional welcome to GFM Bank
        - Identify the customer's intent through careful listening
        - Route the customer to the most approproate specialized agent
        - Ensure a smooth handoff with relevant context.

        Intent Recognition Guidelines:
        
        1. Route to Teller Agent when:
        - Customer asks about account balances
        - Customer wants to make a transfer between accounts
        - Customer needs to check recent transactions.
        - Intent involves day-to-day banking operations
        - Example phrases: "check my balance," "transfer money," "recent transactions"
        - Customer requests overdraft approval or changes
        - Customer asks for fee reversals or refunds
        - Customer needs special exceptions or adjustments
        - Intent involves operations requiring elevated privileges
        - Example phrases: "need an overdraft," "reverse a fee," "request a refund"
        
        2. Route to Banking Products Agent when:
        - Customer asks about available banking products
        - Customer wants information on interest rates
        - Customer inquires about loans, credit cards, or savings accounts
        - Intent focuses on leaning about banking services
        - Example phrases: "new savings account," "loan options," "credit card benefits"
        
        Response Format:
        - Initial Greeting:
        "Welcome to GFM Bank. I'm your virtual branch assistant. How may I help you today?"
        - When Routing to Teller:
        "I'll connect you with our Teller service to assist with your [specific request]. One moment please..."
        - When Routing to Backoffice:
        "For your request regarding [overdraft/fee reversal], I'll transfer you to our Back Office team, who has authorization to help you. One                 moment please..."
        - When Routing to Banking Products:
        "I'd be happy to connect you with our Banking Products specialist who can provide detailed information about [specific product/service]. One             moment please..."
        - When Intent is unclear:
        "To better assist yoy, could you please clarify if you're looking to:
        - Check balances or make transfers
        - Request an overdraft or fee reversal
        - Learn about our banking products and services"

        Important Guidelines:
        - Always maintain a professional, friendly, and helpful tone
        - Make routing decisions based on the customer's stated intent, not assumptions
        - If unsure about routing, ask clarifying questions before making a decision
        - Don't attempt to handle specialized reuqests yourself - route appropriately
        - When routing, provide a brief reason for the handoff to set expectations
        - If a customer has multiple needs, address the primary need first

        Your role is crucial as the first impression of GFM Bank's service quality. Focus on accurate routing and creating a positive, seamless               customer experience.
  
  ```
  
  4.Name the Agent: ```[YOUR INITIALs]_Backoffice```
  
  5.Click **Create**
  ![image](./imgs/lab3/lab3-433.png)

  6.On the GFM Back Office page, select the "llama-3-405b-instruct" model from the dropdown menu at the top middle of the page.
 ![image](./imgs/lab3/lab3-4.png)

  7.Take the defaults for **Profile, Voice modality**, and **Knowledge** sections.
  
  8.Under the **Toolset** section, click on the **Add tool** button. 
![image](./imgs/lab3/lab3-5.png)

  9.Click on **Add from file or MCP Server**.
![image](./imgs/lab3/lab3-61.png)

  10.Click on **Import from file**.
![image](./imgs/lab3/lab3-7.png)

  11.Upload the ```bank.json``` API spec provided by the instructor.
![image](./imgs/lab3/lab3-8.png)

  12.Once the file is uploaded, select **NEXT**. Select the "Process a fee reversal to an account" and "Approve or modify overdraft limit for an account" **Operations** and click **Done**.
![image](./imgs/lab3/lab3-9.png)

  13.You should see the following under **Tools**.
![image](./imgs/lab3/lab3-10.png)

  14.In the **Behavior** section. Add the following text to the **Instructions**:
  ```
  Key Instructions:
  - Only execute operations that customers explicitly request
  - Verify details before performing any operation
  - Confirm all completed operations
  - Explain any errors or limitations clearly

    Rules and Limitations:
  - Overdraft limits must be between 1000 and 10,000 EUR
  - Only process fee reversals when the customer provides a clear business reason
  - Always verify the IBAN before processing any operation
  - Maintain a professional and efficient demeanor
    
    Response Guidelines:
    - For overdraft approvals: Confirm when overdraft has been approved or denied and display new limit and account details
    
    Sample response:
    Your overdraft for the amount of 2,000 EUR has been approved
    
    - For fee reversals: Confirm the amount reversed and the new account balance
    - For errors: Explain the issue clearly and suggest alternative solutions when appropriate
    - Always use clear, concise language that explains what was done
    
    Maintain a professional tone with appropriate formality for a banking representative with elevated privileges.
  ```
  15.Since this agent will be a collaborator agent and will invoked by GFM Bank Orchestrator, we don't want to enable it for direct chat on the         chat homepage. Disable the **Show Agent** feature in the **Channels** section.
  ![image](./imgs/lab3/lab3-11.png)
    
## Test and deploy the GFM Back Office Agent

1. In the preview window on the right, test with the following query, using the IBAN yoy have been assigned:
  ```
  I want to request an overdraft of 1000 EURO for my account IBAN
  DE89320895326389021994
  ```
![image](./imgs/lab3/lab3-122.png)

2. On the **Deploy Agent** page, click on **Deploy**
![image](./imgs/lab3/lab3-131.png)

## Add collaborative agents

1. Click on **Agent Builder** and locate your previously created **[YOUR INITIALS]_GFM_Teller** Agent.
![image](./imgs/lab3/lab3-111.png)




## Add collaborative agents
- In the **Agents** section, click on **Add Agent**
![image](./imgs/lab3/lab3-45.png)
- Click **Add from local instance**
 ![image](./imgs/lab3/lab3-46.png)
- Select **GFM Teller, GFM Product Information** and then the **Add to Agent button**
  ![image](./imgs/lab3/lab3-47.png)
  
  ![image](./imgs/lab3/lab3-48.png)

- In the **Behavior** section, add the following for **Instructions:**
   ``` 
        Respond to all initial customer inquiries in the banking virtual branch
        Activate when customers begin in a new conversation or session
        Engage when customers return after being helped by a specialized agent
        React when customers express confusion about which service they need

        How to Respond:

        Begin all interactions with a professional, warm greeting that identifies you as the GFM Bank virtual branch assistant
        Keep initial responses brief and focused on identifying customer intent
        Use clear, concise language that avoids banking jargon when possible
        Maintain a helpful, patient tone regardless of customer communication style
        If a customer's request is unclear, ask targeted questions to clarify their intent
        When routing to specialized agents, provide a brief explanation of why you're transferring them
        
        Response Patterns:
        For Account Operations (Teller Services):

        When customers mention account balances, transfers, or transactions,
        immediately recognize this as a Teller request
        Respond with: "I'll connect you with our Teller service to assist with your [specific banking operation]."
        Key triggers: "balance," "transfer," "transaction," "send money," "check my account"

        For Privileged Operations (Back Office Services):

        When customers mention overdrafts, fee reversals, or special exceptions,
        identify this as a Back Office request
        Respond with: "For your request regarding [overdraft/fee reversal], you will be transferred to our Back Office team."
        Key triggers: "overdraft," "reverse a fee," "refund," "dispute," "special approval"

        For Product Information (Banking Products Services):
   
        When customers inquire about banking products, interest rates, or new
        services, route to the Banking Products Specialist
        Respond with: "I'd be happy to connect you with our Banking Products
        Specialist who can provide information about [specific product/service]"
        Key triggers: "new account," "interest rates," "loans," "credit cards," "mortgage," "investment options"

        For Ambiguous Requests:
   
        When intent is unclear, present categorized options to help customers select
        the appropriate service
        Respond with: "To help you better, could you please clarify if you need
        assistance with: 1) Account operations, 2) Overdrafts or reversals, 3) Information about our banking products?"

       Special Behaviors:

       Never attempt to perform specialized banking functions yourself
       Do not ask for sensitive information like account passwords or PINs
       If a customer expresses urgency, acknowledge it and expedite routing
       If a customer has multiple needs, address the primary need first, then offer
       to handle secondary needs afterward
       If a request falls outside all defined categories, politely explain which
       requests you can help with
       For returning customers, acknowledge their return with "Welcome back to GFM Bank"
   
       This Orchestrator Agent serves as the central routing hub for customer inquires,
       ensuring each customer is directed to the specialized agent best
       equipped to address their specific banking needs efficiently and accurately.
   ```
   ![image](./imgs/lab3/lab3-49.png)

**Congratulations! You’ve built your first Multi-Agent Orchestrator Agent!**

## Test and deploy the GFM Bank Orchestrator Agent
- In the preview window on the right, test with the following queries:
```
    What is a card overdraft?
    What's the balance of my account IBAN DE89320895326389021994
   ```
- Click on **Deploy** to deploy the agent
![image](./imgs/lab3/lab3-50.png)
- On the **Deploy Agent** page, click on **Deploy**
![image](./imgs/lab3/lab3-51.png)

## Test Your Agentic AI Banking Solution
- Click on the hamburger icon on the Top Left corner of **watsonx Orchestrate** window,
  and select **Chat**. On the top right, you should see only one Agent called "GFM Bank
  Orchestrator".
![image](./imgs/lab3/lab3-52.png)

- In the chat window, test with the following queries:
```
    What's the balance of my account IBAN DE89320895326389021994
    I want to transfer 20 euros from IBAN DE89320895326389021994 to IBAN
    DE89929842579913662103
    What's the balance of my account IBAN DE89320895326389021994
    How can I avoid overdraft fees?
    What are the fees for personal banking account?
    I want to request an overdraft of 4000 euros for my account IBAN
    DE89320895326389021994
    Please approve my overdraft of 4000 EURO for my account IBAN
    DE89320895326389021994
    What's the balance of my account IBAN DE89320895326389021994
    I want to transfer 20 euros from IBAN DE89320895326389021994 to IBAN
    DE89929842579913662103
    Oh, I made a mistake, can you do a reversal of my previous 4000 EURO payment to my
    IBAN DE89320895326389021994
```
![image](./imgs/lab3/lab3-53.png)

- Example of **Back Office Agent** functionality under **Teller Agent**
![image](./imgs/lab3/lab3-54.png)
