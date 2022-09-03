# XCHAIN---beta
Official Implementation of XCHAIN Blockchain wrotten and published on Python Programming Language and JSON.

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

# Need to do
* Halving after each `#10000` mined blocks
* Correction the balance problems after mining.
* `Double-Spending issue fix`
* `Fee` adding
* `Node` Validation

