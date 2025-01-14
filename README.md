# Hyperledger Fabric Empty Smart PDC Contract Set

An empty Hyperledger Fabric smart contract set using Typescript.

## Get started

Launch this smart contract set in the SettleMint Blockchain Transformation platform under the `Smart Contract Sets` section. This will automatically link it to your own blockchain node and make use of the private keys living in the platform.

## Prerequisites

1. Update `collection_config.json` with the right MSPId's of your network.
2. Update `.env` `CC_SIGNATURE_POLICY` to match the MSPId's of your network.

## Usage

Creating an asset:

There are two ways to create an asset:

```bash
export ASSET_PROPERTIES=$(echo -n "{\"objectType\":\"ValuableAsset\",\"assetID\":\"asset1\",\"color\":\"green\",\"size\":20,\"appraisedValue\":100}" | base64 | tr -d \\n)
BTP_SERVICE_TOKEN=<your-access-token> ./lib/btp-chaincode-lifecycle/chaincode.sh invoke 'CreateAsset' --transient "{ \"asset_properties\": \"${ASSET_PROPERTIES}\"}"
```

Or let the api do the base64 encoding for you:

```bash
BTP_SERVICE_TOKEN=<your-access-token> ./lib/btp-chaincode-lifecycle/chaincode.sh invoke 'CreateAsset' --transient '{ "asset_properties": { "objectType": "ValuableAsset", "assetID": "asset1", "color": "green", "size": "20", "appraisedValue": "100" }}'
```

Query the newly created asset:

```bash
BTP_SERVICE_TOKEN=<your-access-token> ./lib/btp-chaincode-lifecycle/chaincode.sh query 'ReadAsset' --arguments 'asset1'
```

Here your access token is an application access token or a personal access token scoped to the nodes you wish to interact with.
