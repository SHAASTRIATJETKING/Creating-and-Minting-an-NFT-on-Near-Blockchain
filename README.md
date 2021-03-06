# Creating-and-Minting-an-NFT-on-Near-Blockchain
Demonstration of Creating and Minting an NFT on Near Blockchain

# Statement of Purpose
In this Near Demo Project, we are creating a testnet wallet account on Near Blockchain for creating and minting an NFT using a NFT minting Smart Contract written using Rust Programming Language. 

In this project, 
  
  --> I am demonstrating how to create a testnet wallet account on Near Blockchain.
  
  --> I am demonstrating how to create an account on https://demo.uniqart.io/ for creating or purchasing an NFT using 200 Near tokens which we receive when we create a testnet account.
  
  --> I am demonstrating how to mint the NFT which you created or purchased on Near Blockchain with the help of NFT Minting Smart Contract.
  
# What does it mean to Minting an NFT on Near Blockchain?
To mint an NFT a Smart Contract needs to able to:

  --> Keeping track of Tokens.
  
  --> Storing information for each Token (i.e, NFT metadata).
  
  --> Linking a Token with an Onwer (In this the owner is neardemoproject.testnet).
  
# Creating a Near Wallet in testnet on Near Blockchain

Video Lecture on How to Create a Wallet in testnet on Near Blockchain

https://drive.google.com/file/d/1prIotJ2W3I6HrrNkVKz-lhEh4oKMr8Ql/view?usp=sharing

PDF Documentation on How to Create a Wallet in testnet on Near Blockchain

https://drive.google.com/file/d/1ABF5cK2cVlDUF0_t4kS9ynmwWVDDLkAG/view?usp=sharing

Near Wallet in testnet created with account name : neardemoproject.testnet

# Connecting your testnet account which you created on https://demo.uniqart.io/

This is an NFT Market place where you can create and purchase NFTs of your wish using 200 Near tokens which you received in the testnet account which you created previously.

Purchase an NFT of your wish from https://demo.uniqart.io/ by connecting your testnet wallet account.

Go through the link for checking the ownership of an NFT you purchased using your testnet account.

https://demo.uniqart.io/token/9435:1

![image](https://user-images.githubusercontent.com/99475076/158056739-a4f34975-b385-4f17-9600-a0cee7cbb383.png)

Go through the link for checking the ownership of NFT using the collectibles tab on https://wallet.testnet.near.org/?tab=collectibles 

![image](https://user-images.githubusercontent.com/99475076/158056808-bf5eec00-cbd0-48db-a7fb-1dd2f3b87b76.png)

# The Tools you need to implement Smart Contract

  --> Yarn (Package Manager)
  
  --> Near-api-js (JavaScript library that utilizes the RPC to interact with NEAR Blockchain)
  
  --> Near-cli (cli tool that acts as a wrapper around near-api-js to interact with the NEAR Blockchain).
  
  --> NEAR testnet wallet account (using wallet.testnet.org)
  
  --> IDE such as Visual Studio Code.
  
# Contract Struct contains:

  The Smart Contract Struct having the following fields:
  
    --> tokens_per_owner: Allows you to keep track of the tokens owned by any account.
  
    --> token_by_id: returns all the information about a specific token.
  
    --> Token_metadata_by_id: returns just the metadata for a specific token.
  
    --> Account_id: a string that ensures there are no special or unsupported.
  
    --> Tokenid: simply a string.
  
# Initialization Functions contains:
  
  A function that can only be called one time. Typically upon deployment of a smart contract onto a near account.
  
    --> "new" method: It intializes all the contract fields defined.
    
    --> "new_default_meta" method: It intializes the contract metadata (i.e, the information about the contract itself).
    
# Contract and Token Metadata - Contract:
  
  NFT Contract Metadata - Information on the smart contract itself
  
  These are the required fields should be contain:
  
    --> Spec: version of smart contract
    
    --> Name: name of the smart contract
    
    --> Symbol: shorthand for name (USD, NEAR and, ETH).
    
 Token Metadata - Information that pertains to a specfic NFT
 
 These are the required field should be contain:
 
    --> Title: Name of an NFT
    
    --> Descriptions: Description of an NFT
    
    --> Media: Link to information that the NFT contains (image,audio,video,gif).
    
# Minting Function contains:

The minting function should do the following:
     
     --> tokens_per_owner: Add the token ID into the set of tokens that the reciever owns.
     
     --> tokens_by_id: Create a token object, and map the token ID to that token object in the tokens_by_id field.
     
     --> token_metadata_by_id: Map the token ID to its metadata.
     
The nft_mint arguments contains:
    
    --> Token_id: Custom ID given to token (string).
    
    --> metadata: metadata associated with token (object).
    
    --> Receiver_id: account that will own the NFT (string omitting special charaters).
    
# Operations of Minting Function:
  
  --> Measures intial storage being used on the smart contract.
  
  --> Specify the token struct that contains the owner ID.
  
  --> Checks for the existence of the token.
  
  --> Inserts the token id and the metadata.
  
  --> Calls an internal method that adds the token to the owner.
  
  --> Calculates the required storage which was used.
  
  --> Refunds excess storage if the user attaches too much.
  
# Deploying the Contract:

Simply run "yarn && yarn build" to run a build script.

build.sh file contains:

    #!/bin/bash
    set -e && RUSTFLAGS='-C link-arg=-s' cargo build --target wasm32-unknown-unknown --release && mkdir -p ../out && cp target/wasm32-unknown-unknown/release/*.wasm ../out/main.wasm
    
# Important Note:

If you are facing any problem or erros in running the script using yarn build command don't panic.

Simply run the below command:

    rustup target add wasm32-unknown-unknown 

Then again run the command yarn build now it wont give any error.

# Install near-cli

     use the command for installing near-cli is:
     npm install near-cli
     
# Deploying the Contract:

--> First we need to run "near login" for storing the keys onto your local machine with near-cli.
    
    near login

--> Next we need to export our NFT Contract using the below command,

    export NFT_CONTRACT_ID="your_account_name" [like neardemoproject.testnet].
    
 Important note is:
 
    Run the above command using git bash in VS Code not in PowerShell if you run in PowerShell it wont work.
    
--> Next we need to echo our NFT_CONTRACT_ID using the below command:

    echo $NFT_CONTRACT_ID
    
--> Next we need to deploy our Smart contract using the below command:

    near deploy --wasmFile out/main.wasm --accountId $NFT_CONTRACT_ID
    
# Intializing the Smart Contract

For intializing the smart contract, we need to run the below command:

    near call $NFT_CONTRACT_ID new_default_meta '{"owner_id": "'$NFT_CONTRACT_ID'"}' --accountId $NFT_CONTRACT_ID
    
# Viewing the Contract's Metadata

For viewing the Contract's Metadata we need to run the below command:

    near view $NFT_CONTRACT_ID nft_metadata
    
# Token Metadata

The Token metadata contains the following:

  --> token_id: "token-1"
  
  --> metadata: 
  
      --> title: "Jetking NFT Collection"
      
      --> description: "This is the first NFT Minting on Near Blockchain"
      
      --> media: "https://ipfs.io/ipfs/bafybeifk6lhlkoqpvu7josjpejfjtmr2x2nb3efrqhn3j4lbwdopwqoybe"
      
      --> receiver_id: "'$NFT_CONTRACT_ID'"
      
# Calling Mint Function

To call the mint function we need to run the below command:

      near call $NFT_CONTRACT_ID nft_mint '{"token_id": "token-1", "metadata": {"title": "Jetking NFT Collection","description":"This is the first NFT Minting on Near Blockchain :)","media": "https://ipfs.io/ipfs/bafybeifk6lhlkoqpvu7josjpejfjtmr2x2nb3efrqhn3j4lbwdopwqoybe"}, "receiver_id":"'$NFT_CONTRACT_ID'"}' --accountId $NFT_CONTRACT_ID --amount 0.1
      
Now check the collectibles tab of testnet wallet account which you created for viewing the NFT which you just minted using the smart contract.

![image](https://user-images.githubusercontent.com/99475076/158053052-9bb15d11-7f69-4ab5-bfce-6974d925bb44.png)

https://explorer.testnet.near.org/transactions/HjpV6PP2EW41j7EFnG2jyb91iT1cKxVvJh4NmNdLoATx



    

    

     

