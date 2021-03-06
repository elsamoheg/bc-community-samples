# Ethereum Blockchain Connector - Microsoft Forms (Basic)

## Table of Contents

* [Table of Contents](#table-of-contents)
* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Step 1 - Create a Microsoft Form](#step-1---create-a-microsoft-form)
* [Step 2 - Deploy Ethereum PoA Network on Azure Cloud](#step-2---deploy-ethereum-poa-network-on-azure-cloud)
* [Step 3 - Deploy MailingList Smart Contract](#step-3---deploy-mailinglist-smart-contract)
* [Step 4 - Create a Logic App Connecting From Microsoft Forms to Ethereum Smart Contract](#step-4---create-a-logic-app-connecting-from-microsoft-forms-to-ethereum-smart-contract)

## Overview

By following this solution, you will learn how to:

 - Create a Microsoft Form with Office 365 Developer Subscription.
 - Deploy an Ethereum PoA network on Azure Cloud.
 - Deploy an Ethereum smart contract on a private Ethereum PoA network.
 - Create a Logic App connecting a Microsoft Form to a Ethereum smart contract.

## Prerequisites

* [Metamask Ethereum Wallet](https://metamask.io/)
* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.
* An Office 365 Developer Subscription. If you don't have one, create a [free account](https://developer.microsoft.com/en-us/office/dev-program). 

## Step 1 - Create a Microsoft Form

To create a Microsoft Form for Logic App integration, join the Office 365 Developer Program then follow the following steps:  

1\. Visit [Office Dev Center](https://developer.microsoft.com/en-us/office/profile) then click `Go to subscription` button:

![Step 1.1](https://i.imgur.com/B0nFlvG.png)

2\. Click `Forms` in the list of Apps. If there isn't one, click `Admin` then follow [this guide](https://docs.microsoft.com/en-us/office365/admin/subscriptions-and-billing/assign-licenses-to-users?view=o365-worldwide) to enable Forms for your subscription.

![Step 1.2](https://i.imgur.com/nR2o78w.png) 

3\. Click `New Form`

![Step 1.3](https://i.imgur.com/8w4pVOV.png)

4\. Edit the title and add an `Email Address` input. After a few seconds the form will be automatically saved.
 
![Step 1.4](https://i.imgur.com/lBmfEsM.png)

## Step 2 - Deploy Ethereum PoA Network on Azure Cloud

Follow [this guide](./EthereumPoA.md) to deploy an Ethereum PoA Network on Azure Cloud.

When asked for entering an `Admin Ethereum Address` during the deployment, fill in the Ethereum address of your Metamask wallet.

## Step 3 - Deploy MailingList Smart Contract

To deploy [MailingList](./contracts/MailingList.sol) smart contract on the created PoA Network, follow the following steps:

1\. Open MetaMask wallet then navigate to `Settings`

![Step 3.1](https://i.imgur.com/AW8x7R3.png)

2\. Navigate to `Security & Privacy` settings then disable privacy mode:

![Step 3.2](https://i.imgur.com/H4mezaH.png)

![Step 3.2](https://i.imgur.com/rC6BvbK.png)

3\. Navigate to `Advanced` settings, then add a new network connection to your Ethereum PoA network deployed in Step 2:

![Step 3.3](https://i.imgur.com/LbH061E.png)

The URL here should be `http://<Public IP to Your PoA Network Deployment>:8540`:

![Step 3.2](https://i.imgur.com/ZhqfAQ6.png)

Click `SAVE` then Metamask will be connecting to your PoA network

![Step 3.2](https://i.imgur.com/UgvmBIC.png)

4\. Visit [Remix IDE](http://remix.ethereum.org/). Please make sure that you are using a http connection (not https) to avoid cross-domain errors.

5\. Delete all pre-loaded example contracts then make sure the folders are empty on the left-side of Remix IDE

![Step 3.5](https://i.imgur.com/U8ydtqL.png)

6\. Click `Create New File` button on the top-left side of Remix IDE to add a new contract called `MailingList.sol`

![Step 3.6](https://i.imgur.com/6kwuW4h.png)

7\. Copy-paste the contents of [MailingList.sol](./contracts/MailingList.sol) to the created file in Remix IDE

8\. Change the compiler version to `0.3.0+commit.1d4f565a` on the right-side of Remix IDE

9\. After the selected compiler is loaded, check `Auto compile` checkbox 

![Step 3.9](https://i.imgur.com/UThDesX.png)

10\. Click `Run` tab on the right-side of Remix IDE then change the `Environment` to `Injected Web3` hereby your Metamask wallet. After reloading the IDE, your Metamask Ethereum account should appear on the list of `Account` dropdown. Next, make sure `MailingList` contract can be found at the bottom which means the contract has been successfully compiled and ready to be deployed.

![Step 3.10](https://i.imgur.com/2oTktyZ.png)

11\. Click `Deploy` button under `MailingList` contract in the `Run` tab to deploy the contract then a confirmation popup will be shown by Metamask saying you have insufficient funds. To resolve this issue, click `Edit` button next to the `GAS FEE` label: 

![Step 3.11](https://i.imgur.com/KPEqXip.png)

![Step 3.11](https://i.imgur.com/TXHru3x.png) 

12\. Click `Advanced` tab then change the `Gas Price (GWEI)` to 0 then click `SAVE` button.

![Step 3.12](https://i.imgur.com/4NN56zG.png)

13\. Now the alert message of insufficient funds should be gone. Click `CONFIRM` button to deploy the contract

![Step 3.13](https://i.imgur.com/aZgAWlA.png)

14\. After a few seconds, you will receive a notification from Metamask saying that your contract deployment is confirmed. Next, you can find the deployed `MailingList` contract at the bottom of the `Run` tab of Remix IDE.

![Step 3.14](https://i.imgur.com/filMp2b.png)

![Step 3.14](https://i.imgur.com/7obW5OC.png)

15\. Keep Remix IDE open for the integration with Logic App in the next step. 

## Step 4 - Create a Logic App Connecting From Microsoft Forms to Ethereum Smart Contract

To create a logic app connecting Microsoft Forms, Azure SQL Server and the MailingList Ethereum contract, follow the following steps:

1\. Login into Azure Portal then visit [this link](https://portal.azure.com/#create/Microsoft.EmptyWorkflow).

2\. Click `Create` button:

![Step 4.2](https://i.imgur.com/oGDbzQq.png)

3\. Fill in the form then create the Logic App resource:

![Step 4.3](https://i.imgur.com/ZA114kE.png) 

4\. After a few minutes, a notification of `Deployment succeeded` will be shown on the top-right of Azure Portal. Click `Go to resource` button to start designing your Logic App:

![Step 4.4](https://i.imgur.com/tEUWedy.png)

5\. Once you are in the created Logic App resource, click `Logic app designer` button on the left-side, then choose `Blank Logic App` template on the right-side:

![Step 4.5](https://i.imgur.com/FuSSDMW.png) 

6\. In the Logic app designer, search for `Microsoft forms trigger` then choose `When a new response is submitted`

![Step 4.6](https://i.imgur.com/FWtC0EA.png) 

7\. Click `Sign in` button then pick your Office 365 developer account. It should be an email address ending with `.onmicrosoft.com`

![Step 4.7](https://i.imgur.com/K4bMYxF.png)

![Step 4.7](https://i.imgur.com/thme6Yv.png)

8\. Change `Form id` dropdown to the title of the created form in Step 1

![Step 4.8](https://i.imgur.com/XfMua4h.png)

9\. Click `+ New step` bottom then choose `Get response details` action of `Microsoft Forms`

![Step 4.9](https://i.imgur.com/iT19kLU.png) 

10\. Focus on `Response Id` input, click `Add dynamic content` button, then choose `List of response notifications Response Id`

![Step 4.10](https://i.imgur.com/Ae5KQqV.png)

11\. The action box will turn into a `For each` box after choosing the `List of response notifications Response Id` dynamic content. Click `Add an action` button inside the `For each` box.

![Step 4.11](https://i.imgur.com/ebT7nmd.png)

12\. To anonymize the input email for GDPR compliance, choose `Generate a SHA256 Hash from a string` as the next action:

![Step 4.12](https://i.imgur.com/5ACtcGK.png)

13\. Fill in the `Data` field with `Email address` dynamic content plus a secret salt to avoid de-anonymization:

![Step 4.13](https://i.imgur.com/9ERYH8q.png)

14\. Rename the action to `HashEmailAddress:

![Step 4.14](https://i.imgur.com/aqgvjbw.png)

15\. Choose `Execute smart contract function` as the next action:

![Step 4.15](https://i.imgur.com/gIKErNq.png)

Create a connection to the Ethereum PoA network by filling in the following parameters: 

![Step 4.15](https://i.imgur.com/PRZ4w2U.png)

|Input Name|Value|
|----------|-----|
|Connection Name|Ethereum PoA|
|Ethereum RPC Endpoint|http://\<Public IP to Your Ethereum PoA Network Deployment\>:8540|
|Private Key|Open MetaMask menu<br>![Step 4.16](https://i.imgur.com/FKrUIxF.png)<br>Click the avatar of your account<br>![Step 4.16](https://i.imgur.com/OOQwnnm.png)<br>Click `EXPORT PRIVATEKEY`<br>![Step 4.16](https://i.imgur.com/rW8chSc.png)|

After a connection is made, fill in the contract call parameters:

![Step 4.15](https://i.imgur.com/Q0hIfFf.png)

|Input Name|Value|
|----------|-----|
|Contract ABI|Go to `Compile` tab of Remix IDE then click `ABI` button to copy the value for this input.<br>![Step 4.16](https://i.imgur.com/4uUYgOE.png)|
|Smart Contract Address|Go to `Run` tab of Remix IDE then click copy button next to the deployed MailingList contract to copy the value for this input.<br>![Step 4.16](https://i.imgur.com/WAFDcrO.png)|
|Smart Contract Function Name|Choose `addMailAddress`|
|hashedMailAddress|![Step 4.15](https://i.imgur.com/SPnVKGT.png)|

Next, add `Gas Price in Wei` parameter then set it to 0:

![Step 4.15](https://i.imgur.com/09pkC5A.png)

![Step 4.15](https://i.imgur.com/YTGKCAB.png)

16\. Choose `Send an email` of Office 365 Outlook as the next action for sending a receipt to the responder:

![Step 4.16](https://i.imgur.com/Y5Ju3R6.png)

17\. Fill in the parameters using dynamic contents as the following screenshot:

![Step 4.17](https://i.imgur.com/nW5JEcJ.png)

18\. Click `Save` button then click `Run` button on the top-left of Logic app designer

![Step 4.18](https://i.imgur.com/4xA4Gka.png)

19\. Open the created form in Step 1 then send a test response

![Step 4.19](https://i.imgur.com/v6eZrzL.png)

20\. Login into Office 365 Outlook with your developer subscription:  

![Step 4.20](https://i.imgur.com/O4VdOkF.png)

then you will see the receipt email in your inbox with an Ethereum transaction hash and the anonymized email address:

![Step 4.20](https://i.imgur.com/N4mkgwT.png)

to check if the response has been recorded on blockchain, go to `Run` tab of Remix IDE, query `getHashedMailAddressArray` function, then you will see the anonymized email address in the returned array:

![Step 4.20](https://i.imgur.com/yrD6sFM.png)