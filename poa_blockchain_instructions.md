# **PROOF OF AUTHORITY (POA) TESTNET BLOCKCHAIN SETUP**

In order to create a low stakes environment to test what the potential that blockchain technology holds in store, we will create a private testnet to allow for endless experimentation. 

We will focus on the Proof of Authority (PoA) algorithm, generally used for private blockchain networks requiring prior approval of the account addresses that can approve transactions.  

We will be using the following tools:
    * Puppeth, to generate the genesis block
    * Geth, a command-line tool, to create keys, initialize nodes, and connect the nodes together
    * The Clique Proof of Authority algorithm
    
Before we can deploy any code, make sure to install the necessary packages using the following guide: [Blockchain Installation Guides](https://github.com/camdorazio/Proof-of-Authority-Dev-Chain/blob/main/blockchain-install-guide.md) 

## **Generate two New Node Accounts**

   1. Activate the environment you created with the necessary packages
   2. Create a directory which will contain your blockchain tools, then, using terminal, navigate there
   3. Create accounts for new nodes using 'geth', with the following code, which you can generate on a new instance of Terminal: 
   
            * ./geth --datadir node1 account new
            
            * ./geth --datadir node2 account new
            
   - **Take note of the passwords you choose for your nodes as well as their public account addresses, you will need them later**
   
            
        
## **Generate Genesis Block**

A genesis block is the first block of a blockchain. It is unique, in that being first, it does not reference a previous block. 

   1. First initiate puppeth with the following code:
           * ./puppeth 
        
   2. Specify the name of the network you will be working on (you can name it anything you want) 
    
   3. Choose option 2, "Configure New Genesis"'
    
   4. Choose option 1, "Create New Genesis from Scratch"
    
   5. Choose option 2, "Clique - proof-of-authority", then press enter twice to choose the default option for how long blocks should take
    
   6. Paste both account addresses (without the initial 0x) into the least of accounts to seal, then repeat. 
    
   7. When prompted to prefund accounts, write yes or no
    
   8. When prompted to specify a chain/Network ID, pick a number (**Remember this number, you will use it later**)
    
   9. Once configured, pick option 2, "Manage Existing Genesis"
    
   10. Pick option 2, "Export Genesis Configurations". You will only need the file titled "nameofnetwork.json"
    
## **Initializing and Unlocking Nodes**

To begin this process, on a Terminal window navigate to the directory containing your blockchain tools

   1. Initialize nodes with "geth", using the following code:
   
           * ./geth --datadir node1 init nameofnetwork.json
           
           * ./geth --datadir node2 init nameofnetwork.json
           
           
   2. Once initialized, in separate Terminal windows, unlock the nodes using the following code:

       * ./geth --datadir node1 --unlock "[insert node 1 public address here]" --mine --rpc --allow-insecure-unlock
       
           **You will be prompted to enter your node password to unlock it** 
       
       * ./geth --datadir node2 --unlock "[insert node 2 public address here]" --mine --port 30304 --bootnodes "[insert node1 enode here]" --ipcdisable --allow-insecure-unlock
       
           **You can find the enode information when you open your unlocked node1 terminal window, under the heading "Started P2P networking" in the following format: "enode://node_one_public_address@127.0.0.1:30303".**
             
           **You will be prompted to enter your node password to unlock it**
            
At this point the PoA blockchain should be up and running. We will now add them to MyCrypto for testing 

## **Adding Blockchain to MyCrypto**

In order to add to MyCrypto, first open up the MyCrypto App, then:

   1. On the lower left hand side of the app click on "Change Network"
   
   2. Click on "Add Custom Node" (use the network info set during the genesis set up process)
   
       * In the "Network" column, choose "Custom" and type in the chain id you chose during the genesis set up process
       
       * For URL, use "http://127.0.0.1:8545"
       
       * Click "Save & Use Custom Node"
   
   3. Connect to your custom network, then select "View and Send" on MyCrypto to begin/test a transaction
   
       * Select the "Keystore File" option
       
       * Select Wallet File and navigate to the Node1 directory to select the file stored there. **You will be prompted to enter your password to unlock your account wallent inside MyCrypto**
       
       * You should see lots and lots of money in your account (if prefunded during the genesis configuration)
       
       * Once unlocked, under the "Send Ether & Tokens", type or paste in the address for Node2, and send your desired number of ether
       
       * Click on "Send Transaction", and once the prompt pops up on the lower part of the app, click on the green "Check TX Status", then on "Logout"
       
       * Click on the blue "Check TX Status" box,  you should see the status message turn from "Pending" to "Successful"
  
   4. Voila! We have created a private blockchain!


    
    
    

