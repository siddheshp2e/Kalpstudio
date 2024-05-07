# KRC1155 Token Contract

This guide serves as a roadmap, navigating you through the intricacies of crafting and deploying secure, versatile, and feature-rich KRC-1155 tokens that fuel innovation within the Kalp ecosystem.

## 

**Overview**

This document outlines the technical details and functionalities of an KRC1155 token contract implemented in Go, utilizing the Kalp SDK for blockchain operations. The KRC1155 standard enables efficient multi-token transactions and interactions, supporting both fungible and non-fungible token types within a single contract.

**Prerequisites**

-   Basic understanding of Go programming language.
    
-   Familiarity with blockchain concepts, KRC1155 token standards, and smart contract development.
    
-   KalpSDK environment set up for blockchain interaction.
    
-   The SDK is compatible with Go version 1.19> or <1.20.
    

## 

**Contract Functions**

### 

Initialize Function

Within the Kalp NFT contract, the `Initialize` method serves as a meticulous architect, establishing the foundational configurations that shape the contract's identity and functionality. It acts as a crucial starting point, ensuring essential parameters are set before any subsequent interactions can occur.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) Initialize(sdk kalpsdk.TransactionContextInterface, name string, symbol string) (bool, error) {
    // Initialization logic here
}
```

**Key Parameters:**

-   `**name**` **(string):** The chosen title that will gracefully adorn the token collection, defining its unique character within the Kalp ecosystem.
    
-   `**symbol**` **(string):** A concise and potent emblem that will serve as the collection's identifier, akin to a heraldic crest in the digital realm.
    

**Return Values:**

-   `**bool**`**:** A boolean value indicating the outcome of the initialization endeavor:
    
    -   `**true**`**:** The initialization process has successfully crafted a solid foundation, and the contract is poised for further interactions.
        
    -   `**false**`**:** Unexpected challenges have derailed the initialization attempt, requiring attention and corrective measures.
        
    
-   `**error**`**:** If obstacles arose during initialization, an error object emerges, carrying valuable insights into the nature of the difficulty.
    

### 

**Mint Function**

The `Mint` method acts as a powerful sculptor, meticulously crafting and issuing NFTs into existence. It serves as the cornerstone for NFT creation, enabling the minting of a designated number of tokens and assigning them to a specified recipient.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) Mint(sdk kalpsdk.TransactionContextInterface, account string, id uint64, amount uint64) error {
    // Minting logic here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the intended recipient who will receive the newly minted NFTs.
    
-   `**id**` **(uint64):** A numerical identifier that serves as a starting point for minting a sequence of NFTs.
    
-   `**amount**` **(uint64):** The precise number of NFTs to be minted and bestowed upon the recipient.
    

**Return Value:**`**error**`**:** In the event of unforeseen minting obstacles, an error object surfaces, shedding light on the nature of the difficulty. It is important to note that the method signature only explicitly indicates an error return type, implying a successful mint operation wouldn't return anything specific.

### 

**MintBatch Function**

The `MintBatch` method embodies the spirit of efficiency, enabling the creation and allocation of **multiple NFTs** in a single, streamlined operation. It empowers the minting of diverse NFT types, each with its unique identifier and quantity, fostering a more efficient workflow for creators and distributors.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) MintBatch(sdk kalpsdk.TransactionContextInterface, account string, ids []uint64, amounts []uint64) error {
    // Batch minting logic here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the intended recipient who will receive the minted NFTs.
    
-   `**ids**` **([]uint64):** An array of numerical identifiers, meticulously assigned to each NFT within the batch, establishing their distinct identities.
    
-   `**amounts**` **([]uint64):** An array of corresponding values, precisely indicating the quantity of NFTs to be minted for each respective identifier within the batch.
    

### 

**Burn Function**

The `Burn` method serves as a transformative force, deliberately removing NFTs from existence and reducing their overall supply. It acts as a counterbalance to minting, fostering scarcity and potentially enhancing the value of remaining tokens.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) Burn(sdk kalpsdk.TransactionContextInterface, account string, id uint64, amount uint64) error {
    // Burning logic here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the individual or entity that will relinquish their ownership of the NFTs, triggering their removal.
    
-   `**id**` **(uint64):** The unique numerical identifier that pinpoints the specific type of NFTs destined for the burning process.
    
-   `**amount**` **(uint64):** The precise quantity of NFTs to be extracted from the account and irrevocably removed from circulation.
    

### 

**BurnBatch Function**

The `BurnBatch` method embodies efficiency and precision, enabling the coordinated removal and destruction of **multiple NFT types** within a single, streamlined transaction. It serves as an optimized approach to managing NFT supply and unlocking various functionalities within the Kalp ecosystem.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) BurnBatch(sdk kalpsdk.TransactionContextInterface, account string, ids []uint64, amounts []uint64) error {
    // Batch burning logic here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the individual or entity relinquishing ownership of the NFTs, initiating their irreversible removal.
    
-   `**ids**` **([]uint64):** An array of unique numerical identifiers, meticulously pinpointing the distinct types of NFTs destined for the synchronized burning process.
    
-   `**amounts**` **([]uint64):** An array of corresponding values, precisely indicating the quantities of each respective NFT type to be extracted from the account and permanently extinguished.
    

### 

**TransferFrom Function**

The `TransferFrom` method acts as a facilitator, enabling the seamless **transfer of ownership** for designated NFTs from one account to another. It empowers vibrant secondary markets and fosters dynamic ownership experiences within the Kalp ecosystem.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) TransferFrom(sdk kalpsdk.TransactionContextInterface, sender string, recipient string, id uint64, amount uint64) error {
    // Single transfer logic here
}
```

**Parameters:**

-   `**sender**` **(string):** The blockchain address of the individual or entity relinquishing ownership of the NFTs, initiating the transfer process.
    
-   `**recipient**` **(string):** The blockchain address of the intended recipient who will receive the NFTs and assume ownership.
    
-   `**id**` **(uint64):** The unique numerical identifier pinpointing the specific type of NFTs to be transferred.
    
-   `**amount**` **(uint64):** The precise quantity of NFTs to be extracted from the sender's account and bestowed upon the recipient.
    

### 

**BatchTransferFrom Function**

The `BatchTransferFrom` method embodies efficiency and coordination, enabling the **seamless transfer of ownership for diverse NFT types** within a single, streamlined transaction. It fosters efficient exchange processes, minimizing transaction costs and enhancing user experience.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) BatchTransferFrom(sdk kalpsdk.TransactionContextInterface, sender string, recipient string, ids []uint64, amounts []uint64) error {
    // Batch transfer logic here
}
```

**Parameters:**

-   `**sender**` **(string):** The blockchain address of the individual or entity initiating the transfer, relinquishing ownership of the NFTs.
    
-   `**recipient**` **(string):** The blockchain address of the intended recipient who will assume ownership of the transferred NFTs.
    
-   `**ids**` **([]uint64):** An array of unique numerical identifiers, pinpointing the precise types of NFTs to be included in the batch transfer.
    
-   `**amounts**` **([]uint64):** A corresponding array of values, specifying the quantities of each respective NFT type to be transferred.
    

### 

**SetApprovalForAll Function**

The `SetApprovalForAll` method acts as a delegation tool, enabling **granular control over NFT management permissions**. It empowers users to grant or revoke the ability for a designated operator (often another smart contract) to transfer all their NFTs on their behalf.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) SetApprovalForAll(sdk kalpsdk.TransactionContextInterface, operator string, approved bool) error {
    // Approval logic here
}
```

**Parameters:**

-   `**operator**` **(string):** The blockchain address of the operator (typically another smart contract) to whom permissions are being granted or revoked.
    
-   `**approved**` **(bool):** A boolean value signifying the desired authorization state:
    
    -   `**true**`**:** Grants the specified operator permission to manage all of the caller's NFTs.
        
    -   `**false**`**:** Revokes any previously granted permission for the operator to manage the caller's NFTs.
        
    

### 

**IsApprovedForAll Function**

the `IsApprovedForAll` method acts as a transparency tool, enabling users and other smart contracts to **verify the authorization status of a designated operator**. It empowers informed decision-making and fosters trust within the Kalp ecosystem.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) IsApprovedForAll(sdk kalpsdk.TransactionContextInterface, account string, operator string) (bool, error) {
    // Check approval status here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the NFT owner whose permissions are being queried.
    
-   `**operator**` **(string):** The blockchain address of the operator whose authorization status is being investigated.
    

### 

**BalanceOf Function**

the `BalanceOf` method serves as a meticulous bookkeeper, enabling the **querying of NFT balances associated with a specific account and token type**. It provides a transparent and accessible way to ascertain digital asset ownership within the Kalp ecosystem.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) BalanceOf(sdk kalpsdk.TransactionContextInterface, account string, id uint64) (uint64, error) {
    // Balance query logic here
}
```

**Parameters:**

-   `**account**` **(string):** The blockchain address of the account whose NFT balance is being investigated.
    
-   `**id**` **(uint64):** The unique numerical identifier representing the specific type of NFTs for which the balance is sought.
    

### 

**BalanceOfBatch Function**

The `BalanceOfBatch` method embodies optimization, enabling the **efficient querying of NFT balances for multiple accounts and token types** within a single operation. It streamlines data retrieval, minimizing transaction costs and enhancing user experience within the Kalp ecosystem.

<<<<<<< HEAD
Copy
=======

>>>>>>> main

```go linenums="1"
func (s *SmartContract) BalanceOfBatch(sdk kalpsdk.TransactionContextInterface, accounts []string, ids []uint64) ([]uint64, error) {
    // Batch balance query logic here
}
```

**Parameters:**

-   `**accounts**` **([]string):** An array of blockchain addresses representing the accounts for which NFT balances are being queried.
    
-   `**ids**` **([]uint64):** An array of unique numerical identifiers, each corresponding to a specific type of NFT for which balances are sought.
    

### 

**Helper Functions**

Within the Kalp NFT smart contract, a suite of **helper functions** acts as the workhorses, meticulously handling fundamental operations. These functions encapsulate specific tasks, promoting **code modularity, reusability, and maintainability**.

-   **Minting and Burning:** Functions like `mintHelper`, `addBalance`, and `removeBalance` meticulously handle the creation and destruction of NFTs, ensuring accurate state updates and adherence to defined rules.
    
-   **Event Emissions:** Dedicated functions manage the emission of **events** like `TransferSingle`, `TransferBatch`, and `ApprovalForAll`, keeping the Kalp ecosystem informed about crucial NFT-related activities.
    

### 

**Event Structures**

The contract meticulously defines **event structures**, serving as blueprints for the information broadcasted when events occur. These structures specify the data elements associated with each event, ensuring clarity and consistency in event communication:

-   **Transfer Events:** `TransferSingle` and `TransferBatch` events capture and broadcast details surrounding NFT transfers, including the sender, recipient, NFT type, and quantity.
    
-   **Approval Events:** The `ApprovalForAll` event transmits information about changes in operator permissions, indicating which operator possesses the ability to manage the owner's NFTs.
    

### 

**Error Handling**

Robust **error handling** is a cornerstone of the contract, ensuring **graceful management of exceptions and invalid operations**. This includes:

-   **Returning informative error objects:** In case of unexpected issues, functions return error objects that precisely describe the encountered difficulty, aiding in troubleshooting and rectification.
    
-   **Validating user input:** Meticulous input validation safeguards against invalid data being submitted to the contract, preventing unintended consequences and potential exploits.
    

### 

**Security Considerations**

The contract prioritizes **security**, implementing robust mechanisms to protect NFT ownership and prevent malicious activity:

-   **Access Controls:** Granular access controls are enforced, meticulously restricting unauthorized access to critical functionalities like minting, burning, and transfers. Only authorized entities (e.g., contract owners or designated operators) can execute these actions.
    
-   **Validation of Operations:** All operations undergo rigorous validation to ensure they adhere to pre-defined rules and restrictions, safeguarding against unauthorized actions or manipulation attempts.
    
-   **Arithmetic Safety:** The contract employs safeguards to prevent **overflow and underflow attacks** during arithmetic operations, protecting against vulnerabilities that could manipulate NFT balances or lead to unexpected behavior.
    

### 

**Conclusion**

This KRC1155 contract documentation provides a comprehensive overview for developers to interact with, including minting, burning, transferring, and managing tokens. Adherence to the KRC1155 standard enables efficient multi-token management within a single contract, supporting a wide range of use cases in digital assets.