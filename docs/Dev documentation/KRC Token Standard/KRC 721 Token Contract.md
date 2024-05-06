# KRC721 Token Contract

This guide serves as a roadmap, navigating you through the intricacies of crafting and deploying secure, versatile, and feature-rich KRC-721 tokens that fuel innovation within the Kalp ecosystem.

## 

**Overview**

This document provides technical details and guidelines for interacting with an KRC721 token contract implemented in Go. This contract utilizes the Kalp SDK to facilitate operations within a blockchain network, enabling the creation, management, and transfer of non-fungible tokens (NFTs).

**Prerequisites**

-   Understanding of Go programming language
    
-   Basic knowledge of blockchain and NFT concepts
    
-   Installed KalpSDK environment
    
!!!Note 
    The SDK is compatible with Go version 1.19> or <1.20.
    


###

**Initialize Token Contract**

The `Initialize` method serves as a crucial first step in configuring a **Kalp-based ERC721 token contract**. It establishes the **name** and **symbol** that will be indelibly associated with the token collection, ensuring clarity and consistency throughout its lifecycle.

**Implementation (Go):**



``` js linenums="1"
func (c *TokenERC721Contract) Initialize(ctx kalpsdk.TransactionContextInterface, name string, symbol string) (bool, error) {
    // Authorization check omitted for brevity
    err := ctx.PutStateWithoutKYC(nameKey, []byte(name))
    if err != nil {
        return false, fmt.Errorf("failed to set token name: %v", err)
    }
    err = ctx.PutStateWithoutKYC(symbolKey, []byte(symbol))
    if err != nil {
        return false, fmt.Errorf("failed to set token symbol: %v", err)
    }
    return true, nil
}
```

**Parameters:**

-   `**name**` **(string):** The human-readable name that designates the token collection, often aligning with its intended use cases or branding.
    
-   `**symbol**` **(string):** A concise and recognizable symbol that serves as a shorthand identifier for the token collection, typically following conventional naming conventions (e.g., "MTK" or "KALP").
    

**Return Values:**`**(bool, error)**`**:** The method returns a boolean value indicating success or failure, accompanied by an error object if any issues arise during initialization.

### 

MintWithTokenURI Function

The `MintWithTokenURI` method holds the power to create brand-new NFTs (Non-Fungible Tokens) within the Kalp ecosystem, cementing their unique existence and linking them with rich metadata. It serves as a cornerstone for establishing ownership and unlocking the diverse possibilities that NFTs offer.



``` js linenums="1"
func (c *TokenERC721Contract) MintWithTokenURI(ctx kalpsdk.TransactionContextInterface, tokenId string, tokenURI string) (*Nft, error) {
    // Initialization and authorization checks omitted for brevity
    nft := &Nft{TokenId: tokenId, Owner: /* Owner's identity */, TokenURI: tokenURI}
    nftKey, _ := ctx.CreateCompositeKey(nftPrefix, []string{tokenId})
    nftBytes, _ := json.Marshal(nft)
    ctx.PutStateWithoutKYC(nftKey, nftBytes)
    // Balance and Transfer event logic omitted for brevity
    return nft, nil
}
```

**Parameters:**

-   `**tokenId**` **(string):** An unequivocally unique identifier assigned to the NFT, ensuring its individuality and preventing any chance of duplication.
    
-   `**tokenURI**` **(string):** A Universal Resource Identifier (URI), acting as a digital address that points to a JSON file containing comprehensive metadata about the NFT's attributes, details, and potential functionalities.
    

**Return Values:**`**(*Nft, error)**`**:** Upon successful minting, the method returns a pointer to the newly created `Nft` object, containing its essential information. It also includes an error object if any issues arise during the process.

### 

**Burn Function**

The `Burn` method wields the definitive power to permanently remove NFTs (Non-Fungible Tokens) from the Kalp ecosystem, executing an irreversible act of destruction that revokes their presence and ownership. It serves as a mechanism for managing token supply, addressing specific use cases, or even symbolizing artistic expression.



``` js linenums="1"
func (c *TokenERC721Contract) Burn(ctx kalpsdk.TransactionContextInterface, tokenId string) (bool, error) {
    // Ownership and initialization checks omitted for brevity
    nftKey, _ := ctx.CreateCompositeKey(nftPrefix, []string{tokenId})
    ctx.DelStateWithoutKYC(nftKey)
    // Remove from balance and emit Transfer event logic omitted for brevity
    return true, nil
}
```

**Parameters:**

-   `**tokenId**` **(string):** The unique identifier that pinpoints the specific NFT destined for elimination.
    

**Return Values:**`**(bool, error)**`**:** The method indicates its success or failure by returning a boolean value, accompanied by an error object if any issues arise during the burning process.

### 

**TransferFrom Function**

The `TransferFrom` method sits at the heart of NFT (Non-Fungible Token) movement within the Kalp ecosystem, meticulously orchestrating the transfer of ownership from one entity to another. It stands as the cornerstone for enabling seamless transactions, trading, and sharing of NFTs.



``` js linenums="1"
func (c *TokenERC721Contract) TransferFrom(ctx kalpsdk.TransactionContextInterface, from string, to string, tokenId string) (bool, error) {
    // Initialization, ownership, and approval checks omitted for brevity
    nft, _ := _readNFT(ctx, tokenId)
    nft.Owner = to
    nftKey, _ := ctx.CreateCompositeKey(nftPrefix, []string{tokenId})
    nftBytes, _ := json.Marshal(nft)
    ctx.PutStateWithoutKYC(nftKey, nftBytes)
    // Update balance keys and emit Transfer event logic omitted for brevity
    return true, nil
}
```

**Parameters:**

-   `**from**` **(string):** The current owner of the NFT, relinquishing their control.
    
-   `**to**` **(string):** The designated recipient who will assume ownership of the NFT.
    
-   `**tokenId**` **(string):** The unique identifier that unequivocally designates the specific NFT being transferred.
    

**Return Values:**`**(bool, error)**`**:** The method signals its success or failure through a boolean value, also returning an error object if any issues arise during the transfer process.

### 

**Approve Function**

The `Approve` method empowers NFT (Non-Fungible Token) owners within the Kalp ecosystem to selectively bestow transfer authority upon designated accounts, granting them the ability to move specific NFTs on behalf of the owner. This flexibility facilitates a range of collaborative and trust-based interactions.



``` js linenums="1"
func (c *TokenERC721Contract) Approve(ctx kalpsdk.TransactionContextInterface, operator string, tokenId string) (bool, error) {
    // Initialization and ownership checks omitted for brevity
    nft, _ := _readNFT(ctx, tokenId)
    nft.Approved = operator
    nftKey, _ := ctx.CreateCompositeKey(nftPrefix, []string{tokenId})
    nftBytes, _ := json.Marshal(nft)
    ctx.PutStateWithoutKYC(nftKey, nftBytes)
    // Omitted logic for emitting Approval event
    return true, nil
}
```

**Parameters:**

-   `**operator**` **(string):** The account designated to receive transfer approval for the specified NFT.
    
-   `**tokenId**` **(string):** The unique identifier that pinpoints the NFT for which authorization is being granted.
    

**Return Values:**`**(bool, error)**`**:** The method indicates success or failure through a boolean value, accompanied by an error object if any issues arise during the approval process.

### 

**SetApprovalForAll Function**

The `SetApprovalForAll` method within the Kalp ecosystem empowers NFT (Non-Fungible Token) owners to confer **blanket approval** to designated accounts (operators). This grants the operator the ability to transfer **all** of the owner's NFTs, acting as a powerful tool for managing large collections or streamlining specific use cases.



``` js linenums="1"
func (c *TokenERC721Contract) SetApprovalForAll(ctx kalpsdk.TransactionContextInterface, operator string, approved bool) (bool, error) {
    // Initialization checks omitted for brevity
    sender := /* Fetch sender's identity */
    approvalKey, _ := ctx.CreateCompositeKey(approvalPrefix, []string{sender, operator})
    approval := Approval{Owner: sender, Operator: operator, Approved: approved}
    approvalBytes, _ := json.Marshal(approval)
    ctx.PutStateWithoutKYC(approvalKey, approvalBytes)
    // Emit ApprovalForAll event logic omitted for brevity
    return true, nil
}
```

**Parameters:**

-   `**operator**` **(string):** The account designated to receive approval for managing **all** the caller's NFTs.
    
-   `**approved**` **(bool):** A flag indicating whether to **grant** (`true`) or **revoke** (`false`) approval for the operator.
    

**Return Values:**`**(bool, error)**`**:** The method signals success or failure through a boolean value, along with an error object if any issues arise during the approval process.

### 

**BalanceOf Function**

The `BalanceOf` method acts as a digital accountant within the Kalp ecosystem, meticulously cataloging NFT (Non-Fungible Token) collections. It enables you to precisely determine the number of NFTs held by a specific account, serving as a crucial tool for understanding ownership patterns, token scarcity, and personal collections.



``` js linenums="1"
func (c *TokenERC721Contract) BalanceOf(ctx kalpsdk.TransactionContextInterface, owner string) int {
    // Initialization checks omitted for brevity
    iterator, _ := ctx.GetStateByPartialCompositeKey(balancePrefix, []string{owner})
    balance := 0
    for iterator.HasNext() {
        iterator.Next()
        balance++
    }
    return balance
}
```

**Parameters:**

-   `**owner**` **(string):** The account whose NFT holdings you wish to inspect.
    

**Return Value:**`**int**`**:** A concise integer representing the exact quantity of NFTs owned by the specified account.

### 

**OwnerOf Function**

Within the Kalp NFT landscape, the `OwnerOf` method serves as a steadfast guide, revealing the rightful owner of a specified NFT. It acts as a fundamental tool for establishing ownership, ensuring responsible transfer, and upholding accountability within this dynamic ecosystem.



``` js linenums="1"
func (c *TokenERC721Contract) OwnerOf(ctx kalpsdk.TransactionContextInterface, tokenId string) (string, error) {
    nft, err := _readNFT(ctx, tokenId)
    if err != nil {
        return "", err
    }
    return nft.Owner, nil
}
```

**Parameters:**

-   `**tokenId**` **(string):** The unique identifier that singles out the NFT for which ownership information is sought.
    

**Return Values:**

-   **Owner Account:** A string representing the account holding ownership of the inquired NFT.
    
-   **Error:** In the event of unforeseen retrieval obstacles, an error object is returned, shedding light on the nature of the difficulty.
    

### 

**GetApproved Function**

The `GetApproved` method acts as a trustworthy informant, revealing the account specifically authorized to transfer a designated NFT on behalf of its owner. It serves as a vital tool for understanding transfer permissions and managing collaborative ownership scenarios.



``` js linenums="1"
func (c *TokenERC721Contract) GetApproved(ctx kalpsdk.TransactionContextInterface, tokenId string) (string, error) {
    nft, err := _readNFT(ctx, tokenId)
    if err != nil {
        return "", err
    }
    return nft.Approved, nil
}
```

**Parameters:**

-   `**tokenId**` **(string):** The unique identifier that pinpoints the NFT for which authorization information is sought.
    

**Return Values:**

-   **Approved Account:** A string disclosing the account granted transfer authority for the queried NFT.
    
-   **Error:** In the event of retrieval obstacles, an error object is returned, clarifying the nature of the difficulty.
    

### 

**IsApprovedForAll Function**

The `IsApprovedForAll` method assumes the role of a meticulous gatekeeper, determining whether a designated account (operator) holds sweeping authority to manage **the entire collection** of NFTs belonging to a specific owner. It acts as a cornerstone for managing extensive collections and facilitating collaborative ownership structures.



``` js linenums="1"
func (c *TokenERC721Contract) IsApprovedForAll(ctx kalpsdk.TransactionContextInterface, owner string, operator string) (bool, error) {
    approvalKey, _ := ctx.CreateCompositeKey(approvalPrefix, []string{owner, operator})
    approvalBytes, err := ctx.GetState(approvalKey)
    if len(approvalBytes) < 1 {
        return false, nil
    }
    approval := new(Approval)
    _ = json.Unmarshal(approvalBytes, approval)
    return approval.Approved, err
}
```

**Parameters:**

-   `**owner**` **(string):** The account whose NFTs are potentially subject to management by an operator.
    
-   `**operator**` **(string):** The account seeking verification of their blanket approval status.
    

**Return Values:**

-   `**bool**`**:** A boolean value unequivocally indicating whether the operator holds comprehensive approval to manage the owner's entire NFT collection.
    
-   `**error**`**:** In the unlikely event of unforeseen challenges, an error object emerges, revealing the nature of the difficulty.
    

### 

**Name Function**

the `Name` method fulfills the role of a skillful archivist, divulging the distinct title bestowed upon a token collection. It serves as a fundamental means of identifying and referencing collections, fostering clarity and discoverability.



``` js linenums="1"
func (c *TokenERC721Contract) Name(ctx kalpsdk.TransactionContextInterface) (string, error) {
    bytes, err := ctx.GetState(nameKey)
    if err != nil {
        return "", err
    }
    return string(bytes), nil
}
```

**Return Values:**

-   `**string**`**:** The collection's carefully chosen name, representing its unique identity.
    
-   `**error**`**:** In the unlikely event of retrieval obstacles, an error object surfaces to illuminate the nature of the difficulty.
    

### 

**Symbol Function**

The `Symbol` method acts as a herald, disclosing the succinct and potent symbol that serves as a collection's emblematic signature. It empowers concise identification and efficient referencing, akin to a heraldic crest in the digital realm.



``` js linenums="1"
func (c *TokenERC721Contract) Symbol(ctx kalpsdk.TransactionContextInterface) (string, error) {
    bytes, err := ctx.GetState(symbolKey)
    if err != nil {
        return "", err
    }
    return string(bytes), nil
}
```

**Return Values:**

-   `**string**`**:** The collection's meticulously chosen symbol, acting as its concise identifier and resonant emblem.
    
-   `**error**`**:** Should retrieval obstacles arise, an error object emerges to shed light on the nature of the difficulty.
    

### 

**TokenURI Function**

Returns the metadata URI of an NFT.

**Parameters:**

-   `tokenId` (string): Unique identifier for the NFT.
    

**Function: TokenURI**



``` js linenums="1"
func (c *TokenERC721Contract) TokenURI(ctx kalpsdk.TransactionContextInterface, tokenId string) (string, error) {
    nft, err := _readNFT(ctx, tokenId)
    if err != nil {
        return "", err
    }
    return nft.TokenURI, nil
}
```

**Returns:** (string, error) - Metadata URI and error if any.

### 

**TotalSupply Function**

the `TokenURI` method plays the role of a trusty navigator, leading explorers to a digital harbor brimming with an NFT's rich metadata. It serves as a fundamental gateway to an NFT's unique traits, captivating imagery, and captivating stories.



``` js linenums="1"
func (c *TokenERC721Contract) TotalSupply(ctx kalpsdk.TransactionContextInterface) int {
    iterator, _ := ctx.GetStateByPartialCompositeKey(nftPrefix, []string{})
    totalSupply := 0
    for iterator.HasNext() {
        iterator.Next()
        totalSupply++
    }
    return totalSupply
}
```

**Parameters:**

-   `**tokenId**` **(string):** The distinct identifier that pinpoints the specific NFT whose secrets await revelation.
    

**Return Values:**

-   `**string**`**:** The metadata URI, a web address leading to a wellspring of descriptive details, vibrant visuals, and captivating stories.
    
-   `**error**`**:** In the unlikely event of retrieval obstacles, an error object emerges, casting light on the nature of the difficulty.
    

### 

**Helper Methods**

#### 

**checkInitialized Function**

the `checkInitialized` method serves as a vigilant sentinel, safeguarding system integrity and ensuring the contract is in a fit state for operation. It acts as a crucial checkpoint, guaranteeing all essential setup procedures have been meticulously completed before transactions and interactions can commence.

**Returns:**

-   `**bool**`**:** A boolean value indicating the initialization status of the contract:
    
    -   `**true**`**:** The contract has been successfully initialized and is ready for use.
        
    -   `**false**`**:** The contract has not yet undergone initialization and remains inoperable.
        
    
-   `**error**`**:** If unforeseen challenges arise during the check, an error object surfaces, providing valuable insights into the nature of the difficulty.
    

### 

**Error Handling**

The Kalp NFT contract prioritizes **exceptional user experience** by meticulously incorporating error-handling mechanisms. This ensures:

-   **Clear and actionable feedback:** When operations encounter roadblocks or invalid inputs are provided, informative error messages are conveyed, empowering users to rectify mistakes and navigate the system effectively.
    
-   **Reduced risk:** By pinpointing the source of errors, developers and system operators can swiftly identify and address potential issues, mitigating operational risks and safeguarding the system's integrity.
    

### 

**Events**

The contract leverages **events** as potent messengers, broadcasting crucial information about significant actions to external applications and services. This fosters:

-   **Real-time monitoring:** Off-chain applications can remain keenly aware of contract state changes, such as NFT transfers or approvals, enabling them to react dynamically and provide users with up-to-date information.
    
-   **Enhanced user experience:** By staying abreast of contract events, external applications can trigger relevant functionalities, such as updating user interfaces or executing automated tasks, enriching the overall user experience.
    

### 

**Security Considerations**

Security remains paramount within the Kalp NFT ecosystem. To safeguard the contract and its users, the following measures are implemented:

-   **Granular access control:** Sensitive operations, such as minting NFTs with custom URIs or burning existing ones, are subject to **rigorous access control mechanisms**. This ensures that only authorized individuals or processes can execute these actions, safeguarding against unauthorized modifications and potential misuse.
    
-   **Input validation:** To thwart common vulnerabilities, the contract meticulously **validates all user-provided input parameters**. This involves verifying data formats and ensuring adherence to predefined constraints, effectively preventing malicious actors from exploiting unintended loopholes within the system.
    

### 

**Conclusion**

This KRC721 token contract provides a comprehensive set of functionalities for managing NFTs, including the creation, transfer, and querying of ownership and metadata. The above documentation offers a detailed guide for developers to effectively interact with and integrate these capabilities within their applications or platforms.