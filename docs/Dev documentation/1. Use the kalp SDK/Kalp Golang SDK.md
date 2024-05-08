# Kalp Golang SDK 

This documentation provides an in-depth guide to the Kalp Software Development Kit (SDK), tailored for developers aiming to interact with the Kalp blockchain network.

## 

Overview

The Kalp SDK is engineered to streamline the development process for Kalp blockchain applications. It offers a suite of tools and functionalities that enable developers to efficiently read and write data, manage transactions, perform KYC checks, track payments for payable contracts, and enhance debugging through logger functionality.

## 

Key Features

The Kalp SDK empowers developers with a robust suite of functionalities designed to simplify and enhance smart contract interaction:

-   **Data Management:: Key-Value Storage:** Efficiently store and retrieve data on the blockchain using a key-value pair structure. This functionality allows persistent data management within your smart contracts.
    
-   **Transaction Handling:: Comprehensive Transaction Management:** Seamlessly submit, query, and retrieve the history of transactions associated with your smart contracts. This comprehensive suite of tools streamlines transaction management workflows.
    
-   **KYC Integration:: Integrated KYC Checks:** Enforce compliance with regulatory requirements or implement access control mechanisms by integrating KYC verification processes directly within your smart contracts.
    
-   **Payment Tracking:: Streamlined Payment Monitoring:** Effortlessly track payments initiated through your smart contracts, particularly within the context of payable contracts. This functionality facilitates accurate record-keeping and financial reconciliation.
    
-   **Debugging Support:: Enhanced Logging:** Gain valuable insights into the behavior and execution of your smart contracts through comprehensive logging capabilities. This functionality aids in debugging and troubleshooting potential issues.
    

### 

Prerequisites

Before you begin, ensure you have the following installed:

**Go Programming Language**: Kalp blockchain contracts are written in Go. Make sure you have Go installed on your system. [Download Go.](https://go.dev/doc/install)

## 

Kalp SDK Installation

Integrating the Kalp SDK into your project is a breeze. To install the Kalp-SDK, use the following Go command:

Copy

```
go get -u github.com/p2eengineering/kalp-sdk-public/kalpsdk
```

This command utilizes the `go get` package management tool within Go to download and install the Kalp SDK from the specified GitHub repository. The `-u` flag ensures you receive the latest available version.

Done! The Kalp SDK is ready to be imported and utilized within your Go project, empowering you to interact with Kalp smart contracts and leverage the platform's functionalities.

_**Note**__: The SDK is compatible with_ _**Go version 1.19**__. For newer versions of Go, update your_ `_go.mod_` _file to specify version 1.19._

## 

Examples

### 

Creating a Contract

Define a Go struct to represent your contract and embed `kalpsdk.Contract` for base functionalities.

Copy

```
type MyContract struct {
    kalpsdk.Contract
}
```

**Struct Creation:** Begin by defining a Go struct to represent your smart contract. This `struct`will serve as the foundation for encapsulating your contract's state variables, functions, and other relevant attributes.

**Embedding** `**kalpsdk.Contract**`**:** To leverage the core functionalities provided by the Kalp SDK, embed the `kalpsdk.Contract` type within your custom contract `struct`. This grants your contract access to essential features like transaction management, key-value storage, and more.

### 

Implementing the Contract Interface

Implement `Init` and `Invoke` methods for contract initialization and invocation.

Copy

```
 func (c *MyContract) Init(ctx kalpsdk.TransactionContextInterface) error {
    // Initialization logic
    return nil
}

func (c *MyContract) Invoke(ctx kalpsdk.TransactionContextInterface, data string) error {
    // Invocation logic
    return nil

```

To breathe functionality into your smart contract, implement the following crucial methods:

-   `**Init**` **Method:**
    
    -   **Purpose:** Responsible for initializing your contract's state variables and performing any actions required upon first deployment to the blockchain.
        
    -   **Signature:** `func (c *MyContract) Init(ctx kalpsdk.TransactionContextInterface) error`
        
    
-   `**Invoke**` **Method:**
    
    -   **Purpose:** Handles calls made to your contract's functions after deployment. This method orchestrates the execution of the requested actions and interactions with the blockchain.
        
    -   **Signature:** `func (c *MyContract) Invoke(ctx kalpsdk.TransactionContextInterface, data string) error`
        
    

### 

Creating and Starting Chaincode

Instantiate your contract and start the chaincode.

Copy

```
// Sample payable contract object
contract := kalpsdk.Contract{IsPayableContract: true}

// KalpSDK Logger object for enhanced operation visibility
contract.Logger = kalpsdk.NewLogger()

// New instance of KalpContractChaincode with your contract
chaincode, err := kalpsdk.NewChaincode(&MyContract{contract})
if err != nil {
    log.Panicf("Error creating KalpContractChaincode: %v", err)
}

// Start the chaincode
if err := chaincode.Start(); err != nil {
    panic(fmt.Sprintf("Error starting chaincode: %v", err))
}
```

Once your smart contract is defined and implemented, proceed with these steps to instantiate it and launch the chaincode:

-   **Contract Configuration:**
    
    -   **Payable Contract:** If your contract involves receiving payments, set the `IsPayableContract` field of the `kalpsdk.Contract` struct to `true`. This enables your contract to handle incoming payments.
        
    -   **Logger Integration:** (Optional) For enhanced visibility into chaincode execution and potential debugging assistance, consider assigning an instance of `kalpsdk.NewLogger()` to the `Logger` field of the `kalpsdk.Contract` struct.
        
    
-   **Chaincode Creation:** Create a new instance of `kalpsdk.Chaincode` by passing your custom contract struct (`MyContract`) wrapped within an instance of `MyContract`. This establishes the connection between your contract logic and the chaincode runtime environment.
    
-   **Error Handling:** Employ proper error-handling mechanisms using `if` statements and appropriate logging or panic functions (e.g., `log.Panicf`) to catch potential errors during chaincode creation and gracefully handle any issues that might arise.
    
-   **Chaincode Startup:** Once the chaincode object is created, initiate its execution by calling the `Start()` method. This method triggers the chaincode's lifecycle and activates your smart contract, making it ready to receive transactions and interact with the blockchain.
    

### 

**Start the Chaincode**

Call the `Start` function on the chaincode instance to start your chaincode.

Copy

```
if err := chaincode.Start(); err != nil {
  panic(fmt.Sprintf("Error starting chaincode: %v", err))
}
```

Call the `Start()` method on the chaincode object to initiate its execution and activate your smart contract.

**Usage:**

-   **Function Call:** `chaincode.Start()`: It directly calls the `Start()` function on the chaincode instance, signaling its readiness to commence operations.
    
-   **Error Handling:**
    
    -   `if err := chaincode.Start(); err != nil`: This conditional statement meticulously checks for errors that may arise during the chaincode's startup process.
        
    -   If an error occurs (`err != nil`), the code gracefully handles it using a panic statement, logging a descriptive message to facilitate debugging.
        
    

## 

Blockchain Data Management

This section details the core functionalities available for managing data on the blockchain.

### 

Writing to the Kalp Blockchain

This section delves into the process of writing data onto the Kalp blockchain, enabling persistent storage and facilitating diverse applications.

### 

**PutStateWithKyc**

This function allows writing data to the ledger with KYC verification, ensuring only KYC-verified users can make ledger modifications.

Copy

```
err := ctx.PutStateWithKyc("myKey", []byte("myValue"))
if err != nil {
    // Handle error
} else {
    // Data successfully written to the blockchain with KYC verification
}
```

It writes a key-value pair to the Kalp blockchain ledger, ensuring only users who have passed KYC verification can write data.

**Usage:**

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context, providing information about the current transaction and blockchain environment.
        
    -   `myKey`: A unique string key for the data being stored.
        
    -   `[]byte("myValue")`: The actual data to be written, represented as a byte array.
        
    
-   **Error Handling:** The `if err != nil` block handles potential errors encountered during data writing.
    
-   **Success Scenario:** The `else` block executes if the data is written successfully without encountering errors.
    

By leveraging `PutStateWithKyc`, you can ensure secure and compliant data storage on the Kalp blockchain, fostering trust and reliability within your applications. Remember to tailor the error handling and success logic within your code to suit your specific use case and application requirements.

### 

**PutStateWithoutKyc**

The `PutStateWithoutKyc` function within the Kalp SDK offers an alternative approach for writing data onto the blockchain ledger. Unlike its counterpart, this function **bypasses the KYC verification step**, enabling broader access to data modification capabilities:

**Functionality:**

-   **Data Writing:** Similar to `PutStateWithKyc`, this function facilitates writing a key-value pair to the blockchain ledger.
    
-   **No KYC Enforcement:** It **does not require mandatory KYC verification** before proceeding with the data storage operation. This approach can be suitable for scenarios where:
    
    -   KYC verification is not applicable or has already been performed at an earlier stage.
        
    -   The data being written has minimal privacy or security concerns.
        
    

Copy

```
err := ctx.PutStateWithoutKyc("myKey", []byte("myValue"))
if err != nil {
    // Handle error
} else {
    // Data successfully written to the blockchain without KYC verification
}
```

The usage pattern for `PutStateWithoutKyc` mirrors that of `PutStateWithKyc`:

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context.
        
    -   `key`: Specifies the unique key for the data.
        
    -   `value`: Represents the actual data to be written.
        
    
-   **Error Handling:** The `if err != nil` block handles potential errors encountered during data writing, similar to `PutStateWithKyc`.
    
-   **Success Scenario:** The `else` block executes if the data is written successfully without encountering errors.
    

By understanding the distinct functionalities of `PutStateWithKyc` and `PutStateWithoutKyc`, you can make informed decisions about data storage on the Kalp blockchain, balancing security, compliance, and accessibility according to your application's needs.

## 

Reading from the Kalp Blockchain

### 

**GetState**

The `GetState` function within the Kalp SDK empowers you to retrieve data stored on the blockchain ledger. This function acts as a key-value store lookup mechanism, allowing you to access previously written data based on its unique identifier.

**Functionality:**

-   **Data Retrieval:** This function retrieves the value associated with a specific key from the ledger.
    
-   **Key-Value Lookup:** It operates like a traditional key-value store, where each key maps to a corresponding value.
    

Copy

```
value, err := ctx.GetState("myKey")
if err != nil {
    // Handle error
} else {
    // Process the retrieved value
}
```

**Usage:**

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context, providing access to information about the current transaction and the blockchain environment.
        
    -   `"myKey"`: This string argument specifies the unique key of the data you intend to retrieve.
        
    
-   **Error Handling:** The `if err != nil` block handles potential errors that might arise during the data retrieval process. These errors could indicate issues like:
    
    -   Invalid key (key not found in the ledger)
        
    -   Network connectivity problems
        
    -   Permission issues (user not authorized to access the data)
        
    
-   **Success Scenario:**
    
-   The `else` block executes if the data retrieval is successful and no errors occur.
    
-   The `value` variable stores the retrieved data, which can be of various types depending on how it was originally stored using `PutState` functions.
    

## 

Deleting from the Kalp Blockchain

### 

**DelStateWithKyc**

The `DelStateWithKyc` function within the Kalp SDK grants authorized users the ability to remove data from the blockchain ledger, **enforcing mandatory KYC verification** before proceeding with the deletion process.

This functionality safeguards the integrity of the ledger by ensuring only authorized and verified users can modify its state:

**Functionality:**

-   **Data Deletion:** This function facilitates the removal of a key-value pair from the blockchain ledger.
    
-   **KYC Enforcement:** It mandates successful KYC verification as a prerequisite for data deletion. This verification process ensures that the user attempting to delete data is authorized to do so, adhering to security best practices and potentially complying with regulatory requirements.
    

Copy

```
err := ctx.DelStateWithKyc("myKey")
if err != nil {
    // Handle error
} else {
    // Data successfully deleted from the blockchain with KYC verification
}
```

**Usage:**

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context, providing access to information about the current transaction and the blockchain environment.
        
    -   `"myKey"`: This string argument specifies the unique key of the data you intend to delete.
        
    
-   **Error Handling:** The `if err != nil` block handles any potential errors that might arise during the KYC verification process or data deletion operation. It's crucial to implement appropriate error-handling mechanisms to gracefully address any issues and prevent unexpected behavior.
    
-   **Success Scenario:** The `else` block executes if the KYC verification is successful and the data is deleted from the ledger without errors. This block typically performs actions like logging success messages or updating internal state variables within your application.
    

### 

**DelStateWithoutKyc**

The `DelStateWithoutKyc` function within the Kalp SDK offers a way to remove data from the blockchain ledger but **bypasses mandatory KYC verification**. While it simplifies deletion, it's crucial to **approach this function with caution** due to potential security concerns:

**Functionality:**

-   **Data Deletion:** Similar to `DelStateWithKyc`, this function removes a key-value pair from the ledger.
    
-   **No KYC Enforcement:** Unlike its counterpart, it **does not require KYC verification** before proceeding with deletion. This can be suitable for specific scenarios where:
    
    -   KYC verification has already been performed at an earlier stage.
        
    -   The data being deleted is non-sensitive and deletion consequences are minimal.
        
    

Copy

```
err := ctx.DelStateWithoutKyc("myKey")
if err != nil {
    // Handle error
} else {
    // Data successfully deleted from the blockchain without KYC verification
}
```

The usage pattern mirrors `DelStateWithKyc`:

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context.
        
    -   `"myKey"`: Specifies the unique key of the data to be deleted.
        
    
-   **Error Handling:** The `if err != nil` block handles potential errors encountered during data deletion.
    
-   **Success Scenario:** The `else` block executes if the data is deleted successfully.
    

## 

**GetKYC**

The `GetKYC` function within the Kalp SDK empowers you to **verify a user's KYC (Know Your Customer) status** on the network. This functionality is essential for implementing access control mechanisms and ensuring that only verified users can perform specific actions or access sensitive data within your application.

**Functionality:**

**KYC Verification Check:** This function queries the network to determine if a particular user identified by their user ID (`userId`) has successfully completed the KYC verification process.

Copy

```
Kyced, err := ctx.GetKYC("userId")
if err != nil {
    // Handle error
} else if Kyced {
    // User has completed KYC, proceed with the desired action
} else {
    // User has not completed KYC, handle accordingly
}
```

**Usage:**

-   **Arguments:**
    
    -   `ctx`: Represents the transaction context, providing access to information about the current transaction and the blockchain environment.
        
    -   `"userId"`: This string argument specifies the user ID for whom you want to check the KYC status.
        
    
-   **Error Handling:** The `if err != nil` block handles potential errors that might arise during the KYC verification check, such as network issues or invalid user IDs.
    
-   **KYC Verification Result:** The `Kyced` boolean variable stores the result of the KYC check.
    
    -   `true`: Indicates the user has **completed KYC verification**.
        
    -   `false`: Indicates the user has **not completed KYC verification**.
        
    -   Based on the `Kyced` value, you can implement conditional logic within your application:
        
        -   If `Kyced` is `true`, proceed with actions that require KYC verification (e.g., allowing access to sensitive data or functionalities).
            
        -   If `Kyced` is `false`, handle scenarios where the user has not completed KYC verification (e.g., display an informative message, prompt the user to complete KYC, or restrict access to certain features).
            
        
    

### 

Conclusion

The Kalp-SDK offers a robust set of tools for developers building decentralized applications on the Kalp blockchain network. By leveraging the SDK's functionalities, developers can efficiently manage data, transactions, and compliance requirements, facilitating a streamlined development process.

Happy coding with the Kalp-SDK on the Kalp blockchain network!