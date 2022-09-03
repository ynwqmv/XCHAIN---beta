# Blockchain

 
## Setup
```sh
# install requirements
pip3 install -r requirements.txt

### NODES
python3 run.py 5000
python3 run.py 5001

### Register the node Neighbor
curl -X POST -H "Content-Type: application/json" -d '{
 "nodes": ["http://127.0.0.1:5001"]
}' "http://localhost:5000/nodes/register"

curl -X POST -H "Content-Type: application/json" -d '{
 "nodes": ["http://127.0.0.1:5000"]
}' "http://localhost:5001/nodes/register"


### Transactions:
curl -X POST -H "Content-Type: application/json" -d '{
 "sender": "your-adress",
 "recipient": "someone-other-address",
 "amount": 0.15
}' "http://localhost:5000/transactions/new"


### Mining:
curl -X GET http://localhost:5000/mine
curl -X GET http://localhost:5001/mine

### Consensus
curl -X GET http://localhost:5000/nodes/resolve

### Chain Compire
curl -X GET http://localhost:5000/chain
curl -X GET http://localhost:5001/chain
```
---
