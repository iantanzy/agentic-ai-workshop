---
layout: page
title: Lab 2b
parent: Lab 2
nav_order: 2
---

# 🏦 GFM Bank Lab 2b: Integrating with External Tools

## GFM Teller Agent

In this lab, we will be building the GFM Teller Agent. This Agent assists customers with everyday banking tasks such as balance inquiries and money transfers. Responds only to what is asked, avoiding assumptions or proactive actions.

![image](./imgs/lab2b/lab2b-architecture.png)

### Create GFM Teller Agent

1. Click on hamburger menu, then **Build -> Agent Builder**

    ![image](./imgs/lab2b/step1.png)

2. On the next screen, click on **Create Agent**

    ![image](./imgs/lab2b/step2.png)

3. Follow the steps according to the screenshot below
    - Select **Create from scratch**
    - Name the agent: *[Your_Initial]_GFM_Teller*
    - Add the following to **Description**
    
    ```
    You are a GFM Bank Teller Agent, responsible for providing accurate, professional assistance with banking transactions such as balance inquiries and transfers. You respond strictly to what the customer asks, without assumptions or suggestions.

    You can:
    Check account balances using the balance-inquiry tool with an IBAN
    Process money transfers using the iban-transfer tool with source IBAN, destination IBAN, and amount
    You format balance responses using structured output, including a clean list or table of recent transactions to improve readability.

    Route to Back Office Agent when:
    Customer requests overdraft approval or changes
    Customer asks for fee reversals or refunds
    Customer needs special exceptions or adjustments
    Intent involves operations requiring elevated privileges
    Customer uses example phrases: "need an overdraft," "reverse a fee," "request a refund"
    ```

4. Click **Create**

    ![image](./imgs/lab2b/step3.png)

5. Once created, you would land in the agent building page. First, select the "llama-3-405b-instruct" model from the dropdown menu at the top middle of the page.

    ![image](./imgs/lab2b/step4.png)

6. Click on the **Toolset** in the left hand navigation to scroll to the Toolset section. Then, click on the **Add tool** button.

    ![image](./imgs/lab2b/step5.png)

7. Click **Add from file or MCP server**.

     ![image](./imgs/lab2b/step6.png)

8. Click **Import from MCP server**

     ![image](./imgs/lab2b/step7.png)

9. Click **Add MCP server**  

     ![image](./imgs/lab2b/step8.png)

10. Follow the steps according to the screenshot below
    - Fill the Server name and Description in as the screenshot. 
    - Ensure Connection is selected to **None**
    - Install Command : ```uvx mcp-proxy https://fund-transfer-mcp-tool20.1soswfjkmeox.us-south.codeengine.appdomain.cloud/sse/```, and 
    - Click **Connect**

    Once connection is successful, click **Done**

     ![image](./imgs/lab2b/step9.png)

11. It will bring you back to the *Import or remove tools from MCP server* page. Here, it lists the tools available in this newly added server. Toggle **ON** the following tools:
    - **teller-tool:get_balance** tool.
    - **teller-tool:transfer_money** tool.

    Then, click "X" at the top right to exit this screen.

    ![image](./imgs/lab2b/step10.png)

12. Now, you should see these tools added under **Tools**:

    ![image](./imgs/lab2b/step11.png)

13. Scroll to the the **Behaviour** section and add the following to **Instructions**:

    ```
    Respond only to what the customer explicitly asks for — never anticipate or suggest next steps
    Do not assume intent — ask for clarification if the inquiry or request is unclear
    Use clear, concise language with a professional tone

    For transfer requests, do the following:
    Confirm and process the transfer
    Report success or failure, including the new transfer if successful
    For insufficient funds, report failure without suggesting overdrafts unless explicitly asked

    For balance inquiries:
    Display the current balance
    Display overdraft limit if available
    Display recent transactions formatted as a table or bulleted list
    End the response — do not suggest further actions

    When presenting recent transactions for Balance Inquiry, use the following format:
    Customer: "What's my account balance for A002?"
    Agent:
    Your current balance is 500 EUR.
    Your overdraft limit is 200 EUR.

    Recent Transactions:
    | Date        | Type      | Amount    | Description        |
    |------------|----------|----------|------------------------|
    | May 16 | Withdrawal | -50 EUR | ATM Withdrawal |
    | May 15 | Deposit | +200 EUR | Direct Deposit |
    | May 13 | Purchase | -30 EUR | Grocery Store |
    ```

    ![image](./imgs/lab2b/step12.png)
    
14. Since this agent will be a collaborator agent and will be invoked by GFM Bank Orchestrator Agent, we don't want to enable it for direct chat on the chat homepage. Scroll down to **Channels** section and disable the **Home page** feature.

    ![image](./imgs/lab2b/step13.png)

### Test the GFM Teller Agent

1. In the preview window on the right, test with the following query:

    ```
    What is the balance of my IBAN <IBAN_Number>?
    ```
    ```
    Transfer 100 from <IBAN_Number> to <IBAN_Number>
    ```

    > **Note:** the balance values need not be the exact same with screenshot

    ![image](./imgs/lab2b/step14.png)


**Congratulations! You've built an agent that employs tools from an MCP server!**