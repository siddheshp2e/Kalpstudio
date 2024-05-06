# How can I view the list of my Smart Contracts ?

Hey Users! Welcome to the Kalp Studio Platform.

Keeping track of your smart contracts can feel overwhelming, but it doesn't have to be. Kalp Studio is here to simplify your experience, offering a streamlined and efficient way to view and manage all your smart contracts in one place.

Smart contracts are automated contracts coded on a blockchain, facilitating secure, transparent, and decentralized transactions without intermediaries. They execute or enforce contract terms when certain conditions are met.

Let's dive into how you can view your list of smart contracts on Kalp Studio.

1. Smart Contract

Figure 1: Dashboard

Go to the smart contract section on the left menu.

Once there, you'll see a list of smart contracts. Each entry in this list is composed of several components:

Figure 2: Smart Contract List

ID: A unique identifier for the smart contract.

Name: The name given to the smart contract.

Project: The project or initiative the smart contract is part of.

Environment: The development or deployment environment of the smart contract

Status: The current state of the smart contract (e.g., Success, In Review, Pending or Failed).

Network: The blockchain network on which the smart contract operates, i.e. Testnet.

Created on: The date when the smart contract was created.

2. Tools & Filters

Figure 3: Tools & Filters

Select Network: This dropdown allows you to filter the list of smart contracts by the blockchain network they operate on. The network can be a test network.

Select Status: This dropdown lets you filter the smart contracts based on their current status. Options might include Success, In Review, Pending, or Failed helping you to find contracts that match your criteria for operational status.

Date: This filter allows you to select smart contracts based on their creation date or any significant date markers relevant to the contract's lifecycle. You can often choose from a date range picker to view contracts created.

Additional Scenarios (When the user clicks on the edit button) When you click the edit icon in the Smart Contract Details, you'll be able to edit the following fields:

Figure 4: Edit Icon

A user will only be able to use the edit icon when the smart contract is saved in drafts.

1. On selecting the edit icon against any contract, the all details present in the drafts can be changed.

2. If the status is set to success, pending or in review, the user can change only the name and description.

Smart Contract Name: Allows you to update the name of the smart contract.

Project Name: Enables you to change the project or initiative the smart contract is associated with.

Network: It lets you select or change the blockchain network on which the smart contract operates i.e. test network

Environment: You can update the environment setting of the smart contract Development, Staging, and Production.

Description: Provides a text area where you can edit or add a detailed description of the smart contract’s purpose and functionality.

Figure5: Edit Smart Contract

When you select a deployed smart contract (with a success status) from the list, you'll be presented with the Smart Contract Details section where you can gain details on your selected Smart Contract.

3. Gain Details

For more details regarding a particular Smart Contract, you can click on the smart contract details and you'll get a screen where you can change tabs between details, Transactions, and API Endpoints of the Smart Contract.

Figure 6: Smart Contract Details

Smart Contract Details The "Smart Contract Details" provide specific information about a particular smart contract in a Kalp network.

Figure 7: Smart Contract Details

ID: A blank field where the unique identifier of the smart contract will be displayed.

Environment: The stage of deployment, such as development, staging, or production.

Network: Specifies on which net the smart contract is deployed i.e. testnet.

Project: The name or identifier of the project associated with the smart contract.

Created On: The date and time the smart contract was created.

Description: A brief description of the smart contract's purpose and functionality.

The above details can be fetched from this section.

As the user switches the tab, the next section will appear.

Transaction

This section displays the all transaction details for the smart contract.

Figure 8: Transaction

ID: Each transaction may be assigned a unique identifier for reference.

Block ID: The ID of the blockchain block that contains the transaction, useful for locating it within the Kalp.

TxHash (Transaction Hash): A unique alphanumeric string that identifies each transaction. It can be used to track and verify the transaction details on the Kalp.

Created On: The date and time when the transaction was recorded on the blockchain.

Status: Shows the current state of the transaction, such as pending, success, or failed.

These details help users track the transaction activities of a smart contract.

#### 

**API Endpoint**

[](https://app.gitbook.com/o/637IdT1B51KjbiJvUYBO/s/zAA5Z6u1ZyGAxXbYfExA/welcome-to-kalp-studio-docs/getting-started/smart-contract-management/kalp-studio-how-can-i-view-the-list-of-my-smart-contracts#api-endpoint)

The "API Endpoint" tab within a smart contract interface provides users with access to the web API endpoints associated with a specific smart contract.

![](https://s3-ap-south-1.amazonaws.com/ind-cdn.freshdesk.com/data/helpdesk/attachments/production/1060006936014/original/p9ZtTccji4721UbcbXuZIVu5ofh6V6OpyQ.png?1708333151)

Figure 9: API Endpoint

​

-   **API Endpoint URL:** The base URL for making API requests to interact with the smart contract.
    

-   **Smart Contract Address:** The unique address of the smart contract on the blockchain.
    

-   **Environment:** Specifies whether the smart contract is in a development, staging, or production environment.
    

-   **Network:** The blockchain network where the smart contract is deployed.
    

The list of operations includes:

-   **HTTP Method:** The type of request (POST) used to interact with the API.
    

-   **Function:** The action or function that the API endpoint will perform.
    

-   **Route:** The specific path appended to the base URL to access a particular function or resource.
    

-   **Check Params:** A feature to validate the parameters for the API request, ensuring they meet the required format or data type before sending the request.
    

This tab is essential for developers to test and ensure that their applications can communicate correctly with the smart contract through the API.

Hope this article helped with beginning your journey on the Kalp Studio platform.