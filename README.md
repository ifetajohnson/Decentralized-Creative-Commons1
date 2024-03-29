# Decentralized-Creative-Commons1
構築WEB3ベースのクリエイティブ・コモンズ・プラットフォームにより、クリエイターがコンテンツを共有し、帰属を受けることができます。
from web3 import Web3

# Connect to the Ethereum blockchain
infura_url = 'YOUR_INFURA_PROJECT_URL'
web3 = Web3(Web3.HTTPProvider(infura_url))

# Verify connection
if not web3.isConnected():
    print("Failed to connect to Ethereum network.")
else:
    print("Successfully connected to Ethereum network.")

# Set up contract
contract_address = 'YOUR_CONTRACT_ADDRESS'
contract_abi = 'YOUR_CONTRACT_ABI'

contract = web3.eth.contract(address=contract_address, abi=contract_abi)

# Function to register content
def register_content(account, private_key, content_hash):
    nonce = web3.eth.getTransactionCount(account)
    txn_dict = contract.functions.registerContent(content_hash).buildTransaction({
        'chainId': 1,
        'gas': 2000000,
        'gasPrice': web3.toWei('50', 'gwei'),
        'nonce': nonce,
    })
    signed_txn = web3.eth.account.signTransaction(txn_dict, private_key=private_key)
    result = web3.eth.sendRawTransaction(signed_txn.rawTransaction)
    print(f"Content registered. Transaction hash: {result.hex()}")

# Example usage
account = 'YOUR_ETHEREUM_ACCOUNT'
private_key = 'YOUR_ACCOUNT_PRIVATE_KEY'
content_hash = 'HASH_OF_YOUR_CONTENT'

# Register your content
register_content(account, private_key, content_hash)
