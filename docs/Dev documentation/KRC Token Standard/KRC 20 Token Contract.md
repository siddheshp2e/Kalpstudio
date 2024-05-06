# KRC20 Token Contract

This guide serves as a roadmap, navigating you through the intricacies of crafting and deploying secure, versatile, and feature-rich KRC-20 tokens that fuel innovation within the Kalp ecosystem.

## 

**Overview**

This document outlines the technical details and functionalities of a KRC20 token contract implemented in Go. The contract leverages the Kalp SDK for operations within a blockchain network, providing a framework for issuing, transferring, and managing tokenized assets compliant with the KRC20 standard.

**Prerequisites**

-   Familiarity with the Go programming language
    
-   Basic understanding of blockchain concepts and KRC20 token standards
    
-   Installation of the Kalp SDK
    
-   The SDK is compatible with Go version 1.19> or <1.20.
    

### 

**Initialize Token Contract**

The `Initialize` function initializes a token contract with essential details, making it ready for subsequent interactions. This function must be called **prior** to any other contract functionalities to establish the token's name, symbol, and decimal places.

**Implementation (Go):**



``` js linenums="1"
// Set information for a token and initialize contract.
func (s *SmartContract) Initialize(sdk kalpsdk.TransactionContextInterface, name string, symbol string, decimals string) (bool, error) {
    // Authorization and initialization checks omitted for brevity

    err := sdk.PutStateWithoutKYC(nameKey, []byte(name))
    if err != nil {
        return false, fmt.Errorf("failed to set token name: %v", err)
    }

    // Symbol and decimals setting omitted for brevity

    return true, nil
}
```

**Parameters:**

-   `**name**` **(string):** The human-readable name of the token (e.g., "MyCoin").
    
-   `**symbol**` **(string):** The abbreviated symbol of the token (e.g., "MYC").
    
-   `**decimals**` **(string):** The number of decimal places the token utilizes (e.g., "18" for 18 decimal places representing cents).
    

**Function Breakdown:**

-   `**Initialize (sdk kalpsdk.TransactionContextInterface, name string, symbol string, decimals string) (bool, error)**`**:**
    
    -   This function accepts four arguments:
        
        -   `sdk`: Reference to the Kalp SDK for blockchain interaction.
            
        -   `name`: The token name.
            
        -   `symbol`: The token symbol.
            
        -   `decimals`: The number of decimal places for the token.
            
        
    -   **Return:** It returns a boolean value indicating success (`true`) or failure (`false`) along with any potential errors.
        
    

**Authorization:** Yes, only authorized clients (e.g., Deployer) can call the `Initialize` function. This ensures proper control over token creation and prevents unauthorized deployments.

_Authorization checks are crucial and intentionally omitted for brevity. Specific authorization mechanisms depend on the smart contract's design and deployment environment._

## 

**Token Operations**

#### 

**Mint Function**

The `Mint` function enables the creation of new tokens and subsequent additions to the minter's account balance. This operation also increases the total supply of the token in circulation.

**Implementation (Go):**



``` js linenums="1"
// Mint creates new tokens and adds them to minter's account balance.
func (s *SmartContract) Mint(sdk kalpsdk.TransactionContextInterface, amount int) error {
    // Authorization checks omitted for brevity

    if amount <= 0 {
        return fmt.Errorf("mint amount must be a positive integer")
    }

    // Update balance and total supply logic omitted for brevity

    return nil
}
```

**Parameters:**

-   `**amount**` **(int):** The positive integer value represents the number of tokens to be minted.
    

**Return Value:**

-   `**error**`**:** This function returns an error object if the minting operation fails. The error message provides details about the encountered issue.
    

#### 

**Burn Function**

The `Burn` function permanently removes a specified number of tokens from the minter's account balance, effectively reducing the total supply of tokens in circulation.

**Implementation (Go):**



```js linenums="1"
func (s *SmartContract) Burn(sdk kalpsdk.TransactionContextInterface, amount int) error {
    // Initialization and authorization checks omitted for brevity

    if amount <= 0 {
        return errors.New("burn amount must be a positive integer")
    }

    // Retrieve, update, and save the new balance and total supply logic omitted for brevity

    return nil
}
```

**Parameters:**

-   `**amount**` **(int):** The positive integer value represents the number of tokens to be burned.
    

**Return Value:**

-   `**error**`**:** This function returns an error object if the burning operation fails. The error message provides details about the encountered issue.
    

#### 

**Transfer Function**

The `Transfer` function facilitates the movement of tokens between accounts within the Kalp ecosystem. It allows the **caller** (the account initiating the transaction) to send a specified number of tokens to a **recipient** account.

**Implementation (Go):**



``` js linenums="1"
// Transfer transfers tokens from the client account to the recipient account.
func (s *SmartContract) Transfer(sdk kalpsdk.TransactionContextInterface, recipient string, amount int) error {
    // Initialization checks omitted for brevity

    err := transferHelper(sdk, clientID, recipient, amount)
    if err != nil {
        return fmt.Errorf("failed to transfer: %v", err)
    }

    // Emit Transfer event logic omitted for brevity

    return nil
}
```

**Parameters:**

-   `**recipient**` **(string):** The unique identifier of the recipient account that will receive the tokens.
    
-   `**amount**` **(int):** The positive integer value representing the number of tokens to be transferred.
    

**Return Value:**

-   `**error**`**:** This function returns an error object if the transfer operation fails. The error message provides details about the encountered issue, such as insufficient funds or an invalid recipient address.
    

#### 

**BalanceOf Function**

The `BalanceOf` function serves as a key tool for retrieving the token balance associated with a specific account within the Kalp ecosystem. It provides a reliable and transparent way to query account holdings.

**Implementation (Go):**



``` js linenums="1"
// BalanceOf returns the balance of the given account.
func (s *SmartContract) BalanceOf(sdk kalpsdk.TransactionContextInterface, account string) (int, error) {
    // Initialization checks omitted for brevity

    balanceBytes, err := sdk.GetState(account)
    if err != nil {
        return 0, fmt.Errorf("failed to read from world state: %v", err)
    }

    balance, _ := strconv.Atoi(string(balanceBytes))

    return balance, nil
}
```

**Parameters:**

-   `**account**` **(string):** The unique identifier of the account whose balance is to be queried.
    

**Return Value:**

-   `**int**`**:** The function returns an integer value representing the token balance of the specified account.
    
-   `**error**`**:** If an error occurs during the balance retrieval process, the function returns an error object along with a descriptive error message.
    

#### 

**Approval Function**

The `Approve` function empowers the caller (the account initiating the transaction) to grant **spending authorization** to another account, designated as the **spender**. This allows the spender to **withdraw tokens** from the caller's account **multiple times** up to a **predefined maximum amount**. This functionality underpins various use cases within decentralized applications (dApps) built on the Kalp blockchain.

**Implementation (Go):**



``` js linenums="1"
// Approve allows the spender to withdraw from the calling client's token account.
func (s *SmartContract) Approve(sdk kalpsdk.TransactionContextInterface, spender string, value int) error {
    // Initialization checks omitted for brevity

    // Create allowanceKey and update the state with the value
    allowanceKey, _ := sdk.CreateCompositeKey(allowancePrefix, []string{owner, spender})
    err := sdk.PutStateWithoutKYC(allowanceKey, []byte(strconv.Itoa(value)))
    if err != nil {
        return fmt.Errorf("failed to update state of smart contract for key %s: %v", allowanceKey, err)
    }

    // Emit Approval event logic omitted for brevity

    return nil
}
```

**Parameters:**

-   `**spender**` **(string):** The unique identifier of the account authorized to withdraw tokens.
    
-   `**value**` **(int):** The positive integer value representing the **maximum allowable withdrawal amount**.
    

**Return Value:**

-   `**error**`**:** The function returns an error object if the approval process fails. The error message provides details about the encountered issue, such as invalid parameters, permission errors, or issues with underlying SDK functions.
    

#### 

**Allowance Function**

The `Allowance` function serves as a vital tool for **retrieving the remaining allowance** granted to a specific **spender** by the **owner** of a token account. This information is crucial for understanding the **authorized spending capacity** of the spender and ensuring proper control over token transfers within the Kalp ecosystem.

**Implementation (Go):**



``` js linenums="1"
func (s *SmartContract) Allowance(sdk kalpsdk.TransactionContextInterface, owner string, spender string) (int, error) {
    // Initialization checks omitted for brevity
    allowanceKey, _ := sdk.CreateCompositeKey(allowancePrefix, []string{owner, spender})
    allowanceBytes, err := sdk.GetState(allowanceKey)
    if err != nil {
        return 0, fmt.Errorf("failed to read allowance: %v", err)
    }
    if allowanceBytes == nil {
        return 0, nil // No allowance set
    }
    allowance, _ := strconv.Atoi(string(allowanceBytes))
    return allowance, nil
}
```

**Parameters:**

-   `**owner**` **(string):** The unique identifier of the account that owns the tokens.
    
-   `**spender**` **(string):** The unique identifier of the account authorized to withdraw tokens.
    

**Return Values:**

-   `**int**`**:** The function returns an integer value representing the **remaining number of tokens** that the spender is authorized to withdraw from the owner's account.
    
-   `**error**`**:** If an error occurs during the retrieval process, the function returns an error object along with a descriptive message explaining the encountered issue.
    

#### 

**TransferFrom Function**

The `TransferFrom` function empowers a designated **spender** to initiate token transfers **on behalf of the owner**, enabling a flexible and controlled mechanism for token movement within the Kalp ecosystem. It's particularly useful in scenarios where third-party services or applications need to manage tokens for users.

**Implementation (Go):**



``` js linenums="1"
func (s *SmartContract) TransferFrom(sdk kalpsdk.TransactionContextInterface, from string, to string, value int) error {
    // Initialization checks omitted for brevity

    // Retrieve and check the allowance of the spender
    // Decrease the allowance
    // Perform the transfer using `transferHelper`
    // Logic omitted for brevity

    return nil
}
```

**Parameters:**

-   `**from**` **(string):** The unique identifier of the account owning the tokens to be transferred.
    
-   `**to**` **(string):** The unique identifier of the recipient account that will receive the tokens.
    
-   `**value**` **(int):** The positive integer value representing the number of tokens to be transferred.
    

**Return Value:**

-   `**error**`**:** The function returns an error object if the transfer process fails. The error message provides details about the encountered issue, such as insufficient allowance, invalid parameters, or other potential errors.
    

#### 

**Token Information Function**

The `Name` function serves as a fundamental tool for accessing the **descriptive name** associated with a token within the Kalp ecosystem. This information is crucial for identifying and understanding the token's purpose and characteristics within various applications and interactions.

**Implementation (Go):**



``` js linenums="1"
func (s *SmartContract) Name(sdk kalpsdk.TransactionContextInterface) (string, error) {
     // Initialization checks omitted for brevity
    bytes, err := sdk.GetState(nameKey)
    if err != nil {
        return "", fmt.Errorf("failed to get token name: %v", err)
    }
    return string(bytes), nil

```

**Return Values:**

-   `**string**`**:** The function returns a string value representing the token's name. This name typically aligns with the token's intended use cases and branding.
    
-   `**error**`**:** If an error occurs during the retrieval process, the function returns an error object along with a descriptive message explaining the issue, such as potential database errors or invalid access attempts.
    

#### 

**Symbol Function**

The `Symbol` function acts as a dedicated tool for retrieving the **unique symbol** associated with a token within the Kalp ecosystem. This symbol serves as a concise and recognizable identifier, enabling efficient communication and exchange across various applications and interfaces.

**Implementation (Go):**



``` js linenums="1"
func (s *SmartContract) Symbol(sdk kalpsdk.TransactionContextInterface) (string, error) {
     // Initialization checks omitted for brevity
    bytes, err := sdk.GetState(symbolKey)
    if err != nil {
        return "", fmt.Errorf("failed to get Symbol: %v", err)
    }
    return string(bytes), nil
}
```

**Return Values:**

-   `**string**`**:** The function returns a string value representing the token's symbol. This symbol typically adheres to conventional shorthand conventions for clarity and consistency (e.g., "MTK," "KALP").
    
-   `**error**`**:** If an error occurs during retrieval, the function returns an error object along with a descriptive message detailing the issue, aiding in troubleshooting and issue resolution.
    

#### 

**TotalSupply Function**

The `TotalSupply` function serves as a vital tool for retrieving the **total number of tokens** that have been **created and issued** within the Kalp ecosystem. This information provides a crucial metric for understanding the overall **token distribution and scarcity**, which are fundamental aspects of token economics and market dynamics.

**Implementation (Go):**



``` js linenums="1"
func (s *SmartContract) TotalSupply(sdk kalpsdk.TransactionContextInterface) (int, error) {
     // Initialization checks omitted for brevity
    totalSupplyBytes, err := sdk.GetState(totalSupplyKey)
    if err != nil {
        return 0, fmt.Errorf("failed to retrieve total token supply: %v", err)
    }
    if totalSupplyBytes == nil {
        return 0, nil // No tokens minted yet
    }
    totalSupply, _ := strconv.Atoi(string(totalSupplyBytes))
    return totalSupply, nil
}
```

**Return Values:**

-   `**int**`**:** The function returns an integer value representing the **total number of tokens** currently in circulation within the Kalp ecosystem.
    
-   `**error**`**:** If an error occurs during the retrieval process, the function returns an error object along with a descriptive message detailing the encountered issue, such as potential storage errors or invalid access attempts.
    

#### 

**Helper Functions**

Included are several helper functions for internal logic, such as `transferHelper`, `add`, `sub`, and `checkInitialized`, which ensures the correct execution of token operations and state management.

----------

### 

**Error Handling**

All operations include detailed error reporting to ensure developers can diagnose and resolve issues during integration and interaction with the contract.

### 

**Events**

The contract emits events for significant actions such as transfers and approvals, facilitating off-chain applications and services to react to contract state changes.

### 

**Security Considerations**

-   Ensure proper access control is enforced, particularly for sensitive operations like `Mint` and `Burn`.
    
-   Validate input parameters to mitigate risks such as reentrancy attacks and overflow/underflow vulnerabilities.
    

### 

**Conclusion**

This KRC20 token contract implemented in Go, utilizing the KalpSDK, provides a comprehensive suite of functionalities for managing digital assets on a blockchain network. The documentation outlined above offers a detailed guide for developers to integrate and leverage these capabilities within their applications.