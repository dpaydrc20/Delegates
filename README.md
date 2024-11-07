# Đoginals Delegates

ℹ️ This is a fork/based on [apezord/ord-dogecoin](https://github.com/apezord/ord-dogecoin)

## ‼️ DISCLAIMER: THIS CODE MAY STILL HAVE BUGS️, AS ITS STILL IN DEVELOPMENT AND TESTING STAGES....‼️

# Delegates

## Overview
The Protocol for inscriptions on Dogecoin, now updated with added support for Delegation rights. Here is the full `doginals.js` script with the necessary updates, instructions, and examples to handle delegate and child inscriptions. Also included id a `DoginalsREADME.md` file detailing how to set up and use the `doginals.js` script.


## Parameters for flexible control over the delegation's rights and constraints:

***When setting up delegation in your Doginals system, you can define custom parameters for flexible control over the delegation's rights and constraints. Here are some useful parameters you could add to extend the functionality and specificity of your delegation setup:***

### 1. Permission Level (permission_level)

- Description: Specifies the scope or intensity of the rights granted. This could be a simple label like "view", "mint", or "transfer", defining the exact actions the delegated address can perform.

- Example: "mint_only", "full_access"

- Usage:
`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "mint_only" 5000`


### 2. Expiration Date (expiration)

- Description: Sets a time limit for the delegation’s validity. After this date, the delegate rights automatically expire, and the delegated address loses access.

- Format: ISO 8601 (e.g., "2024-12-31T23:59:59Z")

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "creator_rights" 5000 "2024-12-31T23:59:59Z"`

### 3. Allowed Content Types (content_types)

- Description: Limits the types of content (e.g., images, text, audio) that the delegate can mint or interact with. Useful for specific applications where delegates should only handle certain media types.

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "image_only" 1000 "image/jpeg,image/png"`

## 4. Rate Limit (rate_limit)

- Description: Defines how frequently the delegate can perform actions (e.g., number of mints per day). This rate-limiting mechanism prevents excessive actions within a short timeframe.

- Format: Numeric, representing actions per time period.

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "mint_limited" 500 "10_per_day"`

## 5. Geographic or IP Restrictions (geo_restrictions or ip_whitelist)

- Description: Restricts the delegate's actions to specific geographic regions or IP addresses. Useful for regionalized deployments or to limit actions to a trusted network.

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "regional_rights" 1000 "US,CA"`

- Alternatively:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "secured_access" 1000 "192.168.1.0/24"`

## 6. Transfer Rights (can_transfer)

- Description: Indicates whether the delegate can transfer or assign its rights to another address. This can either be "true" or "false".

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "creator_rights" 5000 "true"`

## 7. Usage Restriction by Wallet Balance (min_wallet_balance)

- Description: Requires the delegated wallet to hold a minimum balance to exercise its rights. This can be useful to ensure certain actions are limited to wallets with enough DOGE to support fees or transaction requirements.

- Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "premium_access" 1000 "1000_DOGE"`

## 8. Custom Metadata (metadata)
Description: Allows additional metadata fields relevant to specific applications, such as tags, labels, or notes describing the delegation.
Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "creator_rights" 5000 "Event_2024"`


### Putting It All Together

With these parameters, your command to deploy a delegation might look like this:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "mint_only" 1000 "2024-12-31T23:59:59Z" "image/jpeg,image/png" "10_per_day" "true" "1000_DOGE" "Event_2024"`


***These parameters give you a lot of flexibility in tailoring delegation to specific use cases, ensuring that each delegated address has clear, enforceable permissions.***



## Creating a Delegate Inscription

To support delegates in your doginals.js script, here are the delegate-specific commands and example usages for your Doginal NFT project:

### Delegate Commands & Examples

**Deploying & Minting with Delegation**

*Setting Up Delegate Parameters for Deployment If delegates are part of a broader setup (such as transferring rights or permissions in your Doginal ecosystem), you might need to expand delegate functionality by creating an initial delegation deployment.*

**Delegate deploy Command:**
`node . delegate deploy <address> <delegate_param1> <delegate_param2>`

Example:

`node . delegate deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "creator_rights" 5000`

This example deploys a delegate with creator_rights and assigns a limit of 5000 to this delegation setup.
Transferring Delegated Rights Use this if you need to transfer or reassign delegated rights within the Doginal ecosystem.

#### Breakdown of What This Command Does

**Delegate Rights to an Address (Wallet):**

Here, you’re effectively assigning or deploying a set of rights to a specific Dogecoin address (`D9UcJkdirVLY11UtF77WnC8peg6xRYsogu` in this example). This address now holds the rights to a specific delegated operation, such as minting or transferring.

The creator_rights parameter is an arbitrary string that represents a type of right or permission you’re defining for this address, indicating what kind of delegated power this address has.

Deployment (delegate deploy) sets up a new delegation reference, associating a wallet with specific rights.
DelegateTxId is an identifier to be used later on for minting, transferring, etc., using those delegated rights.

Limit provides a cap on the actions the delegated address can perform.


**Inscription ID / Delegation Reference:**

This example doesn't involve an inscription ID directly but instead is setting up a new delegation that could be referenced in future commands.
The 5000 is an example of a quantity or limit associated with the rights—meaning this address might be allowed to perform this delegated action (like minting or transferring) up to 5000 times.


**Real-World Analogy:**

Think of this as setting up a "minting allowance" or "minting quota" for this specific wallet. Once deployed, the delegate allows the specified address to perform actions on behalf of the delegator (like minting NFTs or transferring tokens) up to the specified limit.

## Following Actions: 

Referencing the Delegation
After deploying the delegate, this reference can be used in future transactions by passing an inscription ID (e.g., `delegateTxId`) associated with the delegation to specify the particular delegated rights you want to invoke.

Use this command when minting an NFT with a delegate inscription by providing the `delegateTxId` parameter, which refers to the inscription ID of the delegated transaction. Here’s an example of referencing it

**Mint Delegate from data:**

Command:

`node . mint <address> <content_type> <data_hex> <delegateTxId>`

Example:

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "text/plain;charset=utf-8" 48656c6c6f20776f726c64 15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62ei0`

***Here,*** `15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62ei0` is the delegate transaction ID, ending with i0 to indicate a specific inscription.

- The `delegateTxId` here would point to the inscription or transaction created by the deploy command. This ID links future actions to this delegated allowance.

- Address (`D9UcJkdirVLY11UtF77WnC8peg6xRYsogu`): This is the Dogecoin address where the minted NFT will be associated or sent.

- Content Type (`"text/plain;charset=utf-8"`): Specifies that the data being minted is plain text, encoded in UTF-8 format. This metadata tells the receiving system or application how to interpret the data.

- Hex Data (`48656c6c6f20776f726c64`):

This represents the actual content being minted.
When decoded, `48656c6c6f20776f726c64` in hex translates to `"Hello world"`.


**Mint a delegate inscription from a JPEG file:**

Command:

`node . mint <RECIEVING_DOGE_ADDRESS> <image/jpeg> <path/to/DelegateIMAGE.jpg> <delegateTxId>`

Example:

`node doginals.js mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu image/jpeg path/to/imageToBeDelegated.jpg 15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62ei0`

***Explanation of Each Part***
`D9UcJkdirVLY11UtF77WnC8peg6xRYsogu`: The Dogecoin address where the delegated inscription (JPEG file) will be minted.

`image/jpeg`: The content type, specifying that the file is a JPEG image. This tells the system to handle the data as image data in JPEG format.

`path/to/imageToBeDelegated.jpg`: The path to the JPEG file you wish to mint. The doginals.js script will read this file, convert it into hexadecimal format, and inscribe it in the Dogecoin blockchain.

`15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62ei0`: The `delegateTxId`, referring to a previous inscription ID. This indicates that the JPEG is being inscribed under a delegated inscription, allowing minting with the rights specified by this delegate transaction.

**Mint from an inscription:**

Mint a delegate from an already existing inscription by using its inscription ID. This would create a new inscription that references the original one as a delegate, rather than uploading the entire image file again. The command you shared is correct and follows the process of using an existing inscription as a delegate.

Command:

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "" "" <delegate_inscription_ID>`


***Explanation of Each Part***

Address (`D9UcJkdirVLY11UtF77WnC8peg6xRYsogu`): This is the Dogecoin address where the new delegate inscription will be associated.

Empty Content Type and Data Fields ("" ""): Leaving these fields empty tells the script that no new data is being inscribed. Instead, it will use the existing inscription referenced by <delegate_inscription_ID>.

Delegate Inscription ID (<delegate_inscription_ID>): This is the ID of the existing inscription you want to use as a delegate. By referencing this ID, you create a new inscription that derives its content or permissions from the original.

***How This Works***

This command essentially reuses the content or data of an existing inscription, which allows you to delegate or "replicate" the original inscription without needing to re-upload the data.

The new inscription will point back to the original, making it useful in cases where you want multiple inscriptions to derive from a single source (e.g., a single image or document).

**Benefits**

Efficiency: This avoids duplicating data on the blockchain, saving space and transaction costs.

Delegate Management: The new inscription acts as a "child" or "derived" delegate of the original, allowing you to create relationships or permissions based on the initial inscription.


**Transfer Command:**

`node . delegate transfer <address> <delegate_id> <amount>`

Example:

`node . delegate transfer D9UcJkdirVLY11UtF77WnC8peg6xRYsogu 15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62e 100`

This command transfers `100` units of the delegated rights identified by `15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62e.

These commands provide flexibility in managing delegated inscriptions and rights, allowing for both minting with delegate support and rights management across delegated assets.


### Creating a Child HTML Inscription Referencing the Delegate

1. Create an HTML file (`child.html`) with content referencing the delegate TXID and index:

    ```html
    <!doctype html>
    <html lang=en>
      <head>
        <meta charset=utf-8>
        <meta name=format-detection content='telephone=no'>
        <style>
          html {
            background-color: #131516;
            height: 100%;
          }

          body {
            background-image: url(/content/DELEGATE_TXIDiDELEGATE_INDEX);
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            height: 100%;
            image-rendering: pixelated;
            margin: 0;
          }

          img {
            height: 100%;
            opacity: 0;
            width: 100%;
          }
        </style>
      <script type="text/javascript" src="/uWxngGbZR3KHkKct"></script><script type="text/javascript" src="/qxL0b9F2cbDzh7Qw"></script></head>
      <body>
        <img src=/content/DELEGATE_TXIDiDELEGATE_INDEX></img>
      </body>
    </html>
    ```

2. Replace `DELEGATE_TXID` and `DELEGATE_INDEX` with the actual values.

3. Run the command to create the child inscription:

    ```sh
    node doginals.js mint CHILD_ADDRESS text/html;charset=utf-8 path/to/child.html DELEGATE_TXID DELEGATE_INDEX
    ```

Replace `CHILD_ADDRESS` with your Dogecoin address, `path/to/child.html` with the path to your HTML file, `DELEGATE_TXID` with the TXID of the delegate, and `DELEGATE_INDEX` with the index of the output in the delegate transaction.



### Running the Server

To run the server and extract inscriptions:

```sh
node doginals.js server
```

Access the server at `http://localhost:3000/tx/TXID`, replacing `TXID` with the transaction ID of the inscription you want to extract.

## Additional Commands

- **Wallet Operations**:
    ```sh
    node doginals.js wallet new     # Create a new wallet
    node doginals.js wallet sync    # Sync wallet UTXOs with local Dogecoin node
    node doginals.js wallet balance # Get wallet balance
    node doginals.js wallet send    # Send funds from wallet
    node doginals.js wallet split   # Split wallet funds into multiple UTXOs
    ```

- **DRC-20 Token Operations**:
    ```sh
    node doginals.js drc-20 deploy  # Deploy a new DRC-20 token
    node doginals.js drc-20 mint    # Mint new DRC-20 tokens
    node doginals.js drc-20 transfer # Transfer DRC-20 tokens
    ```
***SEE DoginalsREADME.md***



# Contributing

If you'd like to contribute or donate to our projects, please donate in Dogecoin. For active contributors its as easy as opening issues, and creating pull requests

If You would like to support with Donations, Send all Dogecoin to the following Contributors:

***You can donate to GreatApe here:***

"handle": ***"GreatApe"*** "at": [***"@Greatape42069E"***](https://x.com/Greatape42069E)

 **"Đogecoin_address": "D9pqzxiiUke5eodEzMmxZAxpFcbvwuM4Hg"**

***You can donate to Apezord here:***

"handle": ***"Apezord"*** "at": [***"@apezord"***](https://x.com/apezord)

**"Đogecoin_address": "DNmrp12LfsVwy2Q2B5bvpQ1HU7zCAczYob"**


***You can donate to DPAY here:***

"handle": **DPAY** [***"Dogepay_DRC20"***](https://x.com/Dogepay_DRC20) 

**"Đogecoin_address": " "**


***You can donate to Big Chief here:***

"handle": **@MartinSeeger2** [***"@MartinSeeger2"***](https://x.com/MartinSeeger2) 

**"Đogecoin_address": "DCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz"**


![image](https://github.com/user-attachments/assets/92ad2d4c-b3b1-4464-b9c0-708038634770)

## License

This project is licensed under the Creative Commons Legal Code

CC0 1.0 Universal


*With these updates, you should have a Comprehensive script and documentation to Deploy and Create Delegate and child inscriptions using Doginals.js*
