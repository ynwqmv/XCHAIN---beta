# XCHAIN-BLOCKCHAIN
Official Implementation of XCHAIN Blockchain wrotten      
and published on Python Programming Language | B

`version - 0.27.1`



# Introduction
## Proof-Of-Work Algorithm
```py 
    def proof_of_work(self, last_proof):
        """
        Simple Proof of Work Algorithm:
         - Find a number p' such that hash(pp') contains leading 4 zeros, where p is the previous p'
         - p is the previous proof, and p' is the new proof
        :param last_proof: <int>
        :return: <int>
        """
        proof = 0
        while self.valid_proof(last_proof, proof) is False:
            proof += 1
        return proof
```

## Transaction
```py

def new_transaction(self, sender, recipient, amount,balance=0):
        """
        Creates a new transaction to go into the next mined Block
        :param sender: <str> Address of the Sender
        :param recipient: <str> Address of the Recipient
        :param amount: <int> Amount
        :return: <int> The index of the Block that will hold this transaction
        """
                
        self.current_transactions.append({
            'sender': sender,
            'recipient': recipient,
            'amount': amount
        })
    
        cprint('> transaction from {} to {} registered'.format(sender, recipient), 'green')
        return self.last_block['index'] + 1

```

## Chain Validate
```py
    def valid_chain(self, chain):
        """
        Determine if a given blockchain is valid
        :param chain: <list> A blockchain
        :return: <bool> True if valid, False if not
        """
        last_block = chain[0]
        current_index = 1
        while current_index < len(chain):
            block = chain[current_index]
            # check if that block's hash is correct
            if block['previous_hash'] != self.hash(last_block):
                return False
            # check if that proof of work is correct
            if not self.valid_proof(last_block['proof'], block['proof']):
                return False
            last_block = block
            current_index += 1
        return True
```
## Genesis Block
```py
def __init__(self):
        self.chain = []
        self.current_transactions = []
        self.nodes = set() # set is a way to ensure that we won't have duplicate nodes
        # create the genesis block
        cprint('> forging genesis block...','green')
        self.new_block(previous_hash=1, proof=100)
```
## Genesis Block {JSON}
```json
{
    "chain": [
        {
            "index": 1,
            "previous_hash": 1,
            "proof": 100,
            "timestamp": 1662198349.1180427,
            "transactions": []
        },
```
## Blocks After Genesis
```json
{
            "index": 2,
            "previous_hash": "e92acd3663aafd09f8b5f42d0bcbf464f9860a411256847d747b265a70e4ba13",
            "proof": 35293,
            "timestamp": 1662198883.4122696,
            "transactions": [
                {
                    "amount": 4,
                    "recipient": "9a17a009465e4fd4a44b2f858d9858be",
                    "sender": "BLOCK MINED"
                }
            ]
        },
        {
            "index": 3,
            "previous_hash": "9a1824098eb85324a230193c3be40b481893c0dede9ea6ed810a85dc5ab15794",
            "proof": 35089,
            "timestamp": 1662198884.5207536,
            "transactions": [
                {
                    "amount": 4,
                    "recipient": "9a17a009465e4fd4a44b2f858d9858be",
                    "sender": "BLOCK MINED"
                }
            ]
        },
        {
            "index": 4,
            "previous_hash": "6341aefbd85adcb7a064c0889eb440fd9d5af0c197bdad119631845c859f3aeb",
            "proof": 119678,
            "timestamp": 1662198885.1536438,
            "transactions": [
                {
                    "amount": 4,
                    "recipient": "9a17a009465e4fd4a44b2f858d9858be",
                    "sender": "BLOCK MINED"
                }
            ]
        },

```



# Need to do
* Halving after each `#10000` mined blocks
* Correction the balance problems after mining.
* `Double-Spending issue fix`
* `Fee` adding
* `Node` Validation

