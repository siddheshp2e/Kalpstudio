# Write the Smart Contract

## 

Overview

We require Kalp SDK to a comprehensive Golang package that simplifies the development of smart contracts on the Kalp blockchain network. It is specifically designed to enable developers to write and create Aa Kalp-blockchain-compliant smart contracts with a set of powerful functionalities.

### 

Prerequisites

-   **Golang installation and setup**
    
    A recent version of Go is recommended preferably **1.19 or earlier 1.20**. Compatibility with newer versions might not be guaranteed for all Kalp functionalities.
    
-   **Kalp Software Development Kit (SDK) Installation:**
    
    -   **Installation:** Install the Kalp SDK by following the official installation instructions provided by the Kalp team. These instructions may involve downloading a pre-built binary or building the SDK from the source code.
        
    -   **Documentation:** Familiarize yourself with the Kalp SDK documentation, which outlines available functionalities, usage examples, and best practices for interacting with the Kalp platform through your Go applications.
        
    
-   **Basic Understanding of Blockchain Fundamentals:**
    
    Possess a basic understanding of blockchain networks, including concepts like distributed ledgers, consensus mechanisms, and smart contracts.
    
-   **Go Programming Proficiency:**
    
    Prior experience and proficiency in the Go programming language are essential prerequisites for contributing to Kalp development. This includes understanding core Go syntax, data structures, control flow statements, and error-handling mechanisms.
    

## 

Set up your Development Environment

-   Download and install the appropriate Golang binary for your operating system from the official Golang download page:  [**https://go.dev/doc/install**](https://go.dev/doc/install). Follow the provided installation instructions to ensure proper integration with your system.
    
-   Set up your Go workspace, with the following process:
    
    -   **GOPATH:** Set the `GOPATH` environment variable to define your preferred location for storing Go source code, compiled packages, and downloaded dependencies. It's recommended to choose a dedicated directory outside your system directories (e.g., `/home/your_username/go`).
        
    -   **PATH Update:** Add the `$GOPATH/bin` directory to your system's `PATH` environment variable. This allows you to execute Go commands (like `go build`, `go run`) from any terminal location without specifying the full path.
        
    

## 

Creating and Starting Chaincode

1.  Create a new directory for your project.
    
    1.  Execute the following command to create a new directory named `my-smart-contract`
        
    2.  Change the directory into the newly created project directory.
        
    



```go linenums="1"
$ mkdir my-smart-contract
$ cd my-smart-contract
```

1.  Initialize a new Go module: Within the `my-smart-contract` directory, run the following command to initialize a new Go module named `my-smart-contract`:
    



```go linenums="1"
$ go mod init my-smart-contract
```

1.  Getting Started with Kalp-SDK: Use the `go get` command to download and install the Kalp SDK library:
    



```go linenums="1"
$ go get -u github.com/p2eengineering/kalp-sdk-public/kalp
```

**Response:**



```go linenums="1"
go: downloading golang.org/x/exp v0.0.0-20240222234643-814bf88cf225
go: downloading golang.org/x/sys v0.17.0
go: downloading google.golang.org/grpc v1.62.0
go: downloading golang.org/x/net v0.21.0
go: downloading google.golang.org/genproto/googleapis/rpc v0.0.0-20240221002015-b0ce06bbee7c
go: downloading google.golang.org/genproto v0.0.0-20240221002015-b0ce06bbee7c
go: downloading github.com/go-openapi/spec v0.20.14
go: downloading github.com/go-openapi/swag v0.22.9
go: downloading google.golang.org/genproto v0.0.0-20240213162025-012b6fc9bca9
go: downloading golang.org/x/mod v0.15.0
go: added github.com/go-openapi/jsonpointer v0.20.2
go: added github.com/go-openapi/jsonreference v0.20.4
go: added github.com/go-openapi/spec v0.20.14
go: added github.com/go-openapi/swag v0.22.9
go: added github.com/gobuffalo/envy v1.10.2
go: added github.com/gobuffalo/packd v1.0.2
go: added github.com/gobuffalo/packr v1.30.1
go: added github.com/golang/protobuf v1.5.3
go: added github.com/hyperledger/fabric-chaincode-go v0.0.0-20240124143825-7dec3c7e7d45
go: added github.com/hyperledger/fabric-contract-api-go v1.2.2
go: added github.com/hyperledger/fabric-protos-go v0.3.3
go: added github.com/joho/godotenv v1.5.1
go: added github.com/josharian/intern v1.0.0
go: added github.com/konsorten/go-windows-terminal-sequences v1.0.3
go: added github.com/mailru/easyjson v0.7.7
go: added github.com/p2eengineering/kalp-sdk-public v0.0.0-20240118070807-283512298976
go: added github.com/rogpeppe/go-internal v1.12.0
go: added github.com/sirupsen/logrus v1.9.3
go: added github.com/xeipuuv/gojsonpointer v0.0.0-20190905194746-02993c407bfb
go: added github.com/xeipuuv/gojsonreference v0.0.0-20180127040603-bd5ef7bd5415
go: added github.com/xeipuuv/gojsonschema v1.2.0
go: added golang.org/x/exp v0.0.0-20240222234643-814bf88cf225
go: added golang.org/x/mod v0.15.0
go: added golang.org/x/net v0.21.0
go: added golang.org/x/sys v0.17.0
go: added golang.org/x/text v0.14.0
go: added google.golang.org/genproto v0.0.0-20240213162025-012b6fc9bca9
go: added google.golang.org/genproto/googleapis/rpc v0.0.0-20240221002015-b0ce06bbee7c
go: added google.golang.org/grpc v1.62.0
go: added google.golang.org/protobuf v1.32.0
go: added gopkg.in/yaml.v2 v2.4.0
go: added gopkg.in/yaml.v3 v3.0.1
```

1.  Create a new Go source file`.go` within your project directory. This file will house the core logic of your smart contract. Utilize your preferred text editor or IDE to create the file and ensure it's saved with the `.go` extension.
    



```go linenums="1"
package main

import (
    "fmt"
    "github.com/p2eengineering/kalp-sdk-public/kalpsdk"
)

type SmartContract struct {
     kalpsdk.Contract
}

func (sc *SmartContract) ExecuteTransaction() {
    // Implement the logic for executing transactions
    fmt.Println("Executing transaction...")
}

func (c *SmartContract) Init(ctx kalpsdk.TransactionContextInterface) error {
// Initialization logic return nil
}
```

This newly created file will encompass the following core elements:

-   **Package Declaration:** `package main`: This line specifies that the code within this file belongs to the `main` package, which is the entry point for your smart contract application.
    
-   **Imports:**
    
    -   `fmt`: This import statement allows you to utilize the `fmt` package, providing functionalities for formatted printing and input/output operations.
        
    -   `github.com/p2eengineering/kalp-sdk-public/kalpsdk`: This import statement brings the Kalp SDK library into your project, granting access to the necessary functionalities for interacting with the Kalp blockchain ecosystem.
        
    
-   **Smart Contract Definition:** `type SmartContract struct { ... }`: This part defines a custom struct named `SmartContract` which serves as the blueprint for your smart contract. It embeds the `kalpsdk.Contract` type, inheriting functionalities offered by the Kalp SDK framework.
    
-   **Transaction Execution Function:** `func (sc *SmartContract) ExecuteTransaction() { ... }`: This function, named `ExecuteTransaction`, represents the core logic that will be executed whenever a transaction interacts with your smart contract. Customize this function to encapsulate the specific business logic your smart contract is designed to handle.
    
-   **Initialization Function:** `func (c *SmartContract) Init(ctx kalpsdk.TransactionContextInterface) error { ... }`: This function, named `Init`, serves as the initialization entry point for your smart contract. It typically defines any setup tasks or initialization logic required for your smart contract to function correctly. It takes a `kalpsdk.TransactionContextInterface` argument, providing access to contextual information about the ongoing transaction.
    

1.  Create `main.go` file in the following way.
    



```go linenums="1"
package main

import (
	"log"

	"github.com/p2eengineering/kalp-sdk/kalpsdk"
)

func main() {

	contract := kalpsdk.Contract{IsPayableContract: true}

	contract.Logger = kalpsdk.NewLogger()
	chaincode, err := kalpsdk.NewChaincode(&SmartContract{contract})
	contract.Logger.Info("My KAPL SDK sm4")

	// Create a new instance of your KalpContractChaincode with your smart contract
	// chaincode, err := kalpsdk.NewChaincode(&SmartContract{kalpsdk.Contract{IsPayableContract: true}})
	// kalpsdk.NewLogger()
	if err != nil {
		log.Panicf("Error creating KalpContractChaincode: %v", err)
	}

	// Start the chaincode
	if err := chaincode.Start(); err != nil {
		log.Panicf("Error starting chaincode: %v", err)
	}
```

The `main.go` file stands as the conductor that orchestrates the initialization and execution of your smart contract within the Kalp blockchain environment. It serves as the entry point for your application, bringing your carefully crafted smart contract logic to life. Here's a detailed explanation of its structure:

-   **Necessary Imports:**
    
    -   `**log**` **package:** This package empowers you to issue logging messages, providing valuable insights into the execution flow and potential errors for debugging purposes.
        
    -   `**github.com/p2eengineering/kalp-sdk/kalpsdk**` **package:** This import statement grants access to the essential Kalp SDK functionalities for interacting with the blockchain network and managing your smart contract.
        
    
-   **The** `**main**` **Function:** This function serves as the starting point for your application when it's executed. It undertakes the following crucial tasks:
    
-   **Contract Configuration:**
    
    -   `**contract := kalpsdk.Contract{IsPayableContract: true}**`**:** This line initializes a new `Contract` object, defining key properties of your smart contract. The `IsPayableContract: true` setting designates that your contract will be capable of receiving payments from users.
        
    -   `**contract.Logger = kalpsdk.NewLogger()**`**:** This statement creates a new logger instance and assigns it to the contract, enabling you to generate logging messages for tracking events and debugging.
        
    
-   **Chaincode Instantiation:**
    
    -   `**chaincode, err := kalpsdk.NewChaincode(&SmartContract{contract})**`**:** This line constructs a new instance of the `KalpContractChaincode` type. It integrates your custom `SmartContract` implementation, effectively bridging your contract logic with the Kalp SDK framework.
        
    -   `**contract.Logger.Info("My KAPL SDK sm4")**`**:** This statement logs an informative message using the logger, indicating that the chaincode is initialized and ready to commence operations.
        
    
-   **Crucial Error Handling:**`**if err != nil { ... }**` **blocks:** These conditional blocks diligently check for potential errors during chaincode creation and startup. If errors occur, the `panicf` the function is invoked, terminating execution with an informative error message. This assertive error handling safeguards the integrity of your application and facilitates debugging efforts.
    
-   **Chaincode Activation:**`**if err := chaincode.Start(); err != nil { ... }**`**:** This block calls the `Start()` function on the instantiated chaincode, triggering the execution of your smart contract within the Kalp blockchain environment. Once again, error handling is incorporated to gracefully address any issues that might impede chaincode startup.
    

!!! Note "Payment Tracking for Payable Contracts" 
    Pass your contract_ `_struct_` _as an argument to the_ `_NewChaincode_` _function and specify whether the contract is payable or not. 
    **This places the external dependencies** for your smart contract into a local `vendor` directory.




```go linenums="1"
$ go mod vendor
```

1.  **Folder Structure**: After Executing the above command the folder Structure shows up as below:
    



```go linenums="1"
Folder name
├──vendor
├──go.mod
├──go.sum
├──main.go
└── contract
    └── contract.go
```

1.  Save your changes.
    

## 

**Implementation Steps with Kalp SDK**

1.  **Define a New Go Struct:** Represent your contract with a new Go struct and embed the `kalpsdk.Contract` struct to inherit base contract functionalities.
    



```go linenums="1"
type MyContract struct {
kalpsdk.Contract
}
```

1.  **Implement the Contract Interface:** Define the `Init` and `Invoke` methods for initialization logic and invocation handling.
    



```go linenums="1"
func (c *MyContract) Init(ctx kalpsdk.TransactionContextInterface) error {
// Initialization logic return nil
}
func (c *MyContract) Invoke(ctx kalpsdk.TransactionContextInterface, data string) error {
// Invoke logic return nil
}

```

----------

#### 

3. Blockchain Data Management

This section details the core functionalities available for managing data on the blockchain:

**Writing to the Blockchain:**

-   `**PutStateWithKyc**`**:** This function facilitates writing data onto the blockchain ledger. Crucially, it enforces mandatory KYC (Know Your Customer) verification as part of the write operation, ensuring compliance with regulatory requirements or specific platform policies.
    
-   `**PutStateWithoutKyc**`**:** This function enables writing data to the blockchain ledger. Unlike its counterpart, it bypasses the KYC verification step, potentially catering to situations where regulatory constraints are not applicable or KYC checks have already been performed at an earlier stage.
    

**Reading from the Blockchain:**

-   `**GetState**`**:** This function retrieves the data from the blockchain ledger. It allows querying the current state of the ledger to obtain information relevant to your application's needs.
    

**Deleting from the Blockchain:**

-   `**DelStateWithKyc**`**:** This function enables deleting data from the blockchain ledger. Similar to `PutStateWithKyc`, it enforces mandatory KYC verification before proceeding with the deletion operation.
    
-   `**DelStateWithoutKyc**`**:** This function allows the deleting data from the blockchain ledger. Just as with `PutStateWithoutKyc`, it bypasses the KYC verification step, potentially catering to specific scenarios where deletion is permitted without additional verification.
    

## 

Sample Code Examples

### 

Writing to the Blockchain

### 

**PutStateWithKyc**



```go linenums="1"
err := ctx.PutStateWithKyc("myKey", []byte("myValue")) 
if err != nil {
  // Handle error 
 } else {
  // Data successfully written to the blockchain with KYC verification
 }
```

### 

**PutStateWithoutKyc**



```go linenums="1"
err := ctx.PutStateWithoutKyc("myKey", []byte("myValue"))
if err != nil {
    // Handle error
} else {
    // Data successfully written to the blockchain without KYC verification
}
```