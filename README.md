# Table of Contents
1. [The Main Idea](#1-the-main-idea)
2. [Screening Results](#2-screening-results)
3. [How Does Umbra Work?](#3-how-does-umbra-work)
4. [How Do We Track the Complete Fund Flow of a Transfer Completed Through Umbra Using On-Chain Data?](#4-how-do-we-track-the-complete-fund-flow-of-a-transfer-completed-through-umbra-using-on-chain-data)
5. [Process Data](#5-process-data)
# 1.The Main Idea
Umbra is a well-known privacy address protocol. Some industrial sybil clustersmay attempt to conceal their witchcraft behaviors through Umbra. The core logic of this screening is to capture sybil clusters through the information recorded in the event logs of Umbra.Cash smart contracts on the chain. By analyzing the event logs, we can trace the fund flow paths of transactions conducted through Umbra. These fund flow paths help us identify potential clusters of industrial sybil clusters

# 2 Screening Results
The final sybil address csv  [```layerzero_sybil_node_final.csv```](https://github.com/cryptoamy/layerzero_sybil_scan/blob/main/layerzero_sybil_node_final.csv)

The report does not include specific screening code. If auditors need to review the code, they can message it in the comments, I will provide access to the private code repository.

The total number of Sybil Addresses is [**17,232**]. Detailed breakdown is as follows:    

### 2.1 We have identified [**260 clusters** ] of industrial witches (clusters with a node size greater than 20).    
https://github.com/cryptoamy/layerzero_sybil_scan_report/tree/main/result.
<img width="819" alt="image" src="https://github.com/cryptoamy/layerzero_sybil_scan_report/assets/143737437/4f1a5424-a98d-49ef-bac5-179990a31f6b">


### 2.2 The network diagrams for all 260 clusters are aggregated in a zip archive, which you can download from Google Drive to view locally.    
:https://drive.google.com/file/d/1z1RIjMUnGUMO15EUeT9Pm7pjZmZNwQT0/view?usp=share_link    
(After unzipping, you can see folders for all clusters, containing the funds flow graph and the funds flow tx details.)

### 2.3 Here are some examples of large clusters. Detailed information on the 51 large clusters (including cluster address details and fund network diagrams) can be found in this folder: **https://github.com/cryptoamy/layerzero_sybil_scan_report/tree/main/result.**    


#### 0x46cef06aaf268e1a72926f26ce0a86346d0486a6 , clusters of 3167 nodes   
Download the file from https://github.com/cryptoamy/layerzero_sybil_scan_report/blob/main/result/3167_nodes_0x46cef06aaf268e1a72926f26ce0a86346d0486a6/     
![3167_nodes_0x46cef06aaf268e1a72926f26ce0a86346d0486a6](https://github.com/cryptoamy/layerzero_sybil_scan_report/assets/143737437/5ff05d31-9798-4ada-9f36-f3b2278c8091)

#### 0xaf6c59928d4d9c495ada09f88c5d22333dec342c , clusters of 2369 nodes
![2369_nodes_0xaf6c59928d4d9c495ada09f88c5d22333dec342c](https://github.com/cryptoamy/layerzero_sybil_scan_report/assets/143737437/d8147240-4002-441d-8560-27c097942c32)
Download the file from [https://github.com/cryptoamy/layerzero_sybil_scan_report/blob/main/result/3167_nodes_0x46cef06aaf268e1a72926f26ce0a86346d0486a6/     ](https://github.com/cryptoamy/layerzero_sybil_scan_report/tree/main/result/2369_nodes_0xaf6c59928d4d9c495ada09f88c5d22333dec342c)

#### 0xafc97e407be38317bb591838b30cad92dc892013 , clusters of 918 nodes
![918_nodes_0xafc97e407be38317bb591838b30cad92dc892013](https://github.com/cryptoamy/layerzero_sybil_scan_report/assets/143737437/6b86dd18-ec0f-49d7-9d68-4c20b1bf46f9)





# 3 How does Umbra work?    
Through Umbra's event logs, although it's complex, we can still trace the entire fund flow chain. In Umbra, all transfers occur between a Sender_address (directly interacting with the Umbra smart contract) and a Withdraw_Address (the final actual recipient address), together forming the fund flow chain. If the same Sender_address has direct fund transactions with many Withdraw_Address, or if the same Withdraw_Address has direct fund transactions with many Sender_address, they will form a cluster. If the addresses in the cluster exceed a certain number, we can almost consider them the work of industrial sybil clusters    
<img width="620" alt="1" src="https://github.com/cryptoamy/layerzero_sybil_scan/assets/143737437/2dc7fa93-342d-4896-ac0e-17533ca74767">


**-->Image 1<--**    
Image source: Umbra official website: https://app.umbra.cash/faq#what-is-umbra
# 4 How do we track the complete fund flow of a transfer completed through Umbra using on-chain data?
Let's illustrate what the fund flow on-chain looks like for a transfer through Umbra with a specific example:  

**[ i ] Transfer to a stealth address (which we can also refer to as an intermediate address) through Umbra**    
**This is the process of Step 1  in [ image 1 ]**    

https://etherscan.io/tx/0x0007f7ad94bfa2ffba9d220dea7efc699554c09bdbcd668aefd784696f31556a
<img width="1073" alt="2" src="https://github.com/cryptoamy/layerzero_sybil_scan/assets/143737437/3f1d6d9b-da03-4301-86fe-1387ad63817b">

**-->Image 2<--**      


**[ ii ] Transfer ETH from the intermediate address to the final target address(the withdraw address)**    
**This is the process of Step 2 in [ image 1 ]**    

https://etherscan.io/address/0xB8C0258F5E61156dCFb61b5c39aB8A2Eb77a1250
<img width="1446" alt="3" src="https://github.com/cryptoamy/layerzero_sybil_scan/assets/143737437/8f62263b-f595-4714-8140-0b21b55e108c">

**-->Image 3<--**

**[ iii ] Finally, we obtained the complete Umbra transfer fund flow.**     
Sender Address (0x451889B0f1b6e0D2edC5d9Cb510AA23F91B4Cf04) --> Intermediate Address (0xB8C0258F5E61156dCFb61b5c39aB8A2Eb77a1250) --> Withdraw Address (0x291787bfa50Dc4097dccc03beE8aBFcb2CE24e33)


# 5 Process Data
### 5.1. Get the raw data    
a.Transcation Record of sending action from **Sender Address** to **Intermediate Address**    

b.Transcation Record of sending action from **Intermediate Address** to **Withdraw Address**  

We save the data at the folder named **umbra_cash_record/**

### 5.2. Processing Umbra data, identify potential clusters of industrial sybil clustersthrough the fund flow of all transactions. Afterwards, compile a list of sybil addresses.
a.Merge raw data  together to get fund flow of all transfer throught Umbra
b.Identify clusters with a node count greater than 10, which are considered clusters of industrial sybil clusters All addresses within these clusters are designated as sybil addresses. 

We have obtained the exported CSV file ```umbra_sybil_address.csv.```
### 5.3. Associate the sybil addresses obtained in 5.2 with the set of Layer Zero User Addresses. The intersection of these sets will be the sybil addresses among Layer Zero users.


### 5.4. Combine the Layer Zero addresses found in 5.3 with the fund flow of all transactions obtained in sector [5.2].Draw the graph of all sybil clusters.

### Here we  have obtained the exported the final sybil address csv  ```layerzero_sybil_node_final.csv```
