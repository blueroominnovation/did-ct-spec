# `did:ct` Method Specification

CircularTrust is a blockchain platform built on Hyperledger Besu technology where actors participating in the circular economy can share information about the circularity of their products, materials or waste. It is used among multiple projects in the BlueRoom Innovation ecosystem. The role of a Circular Trust DID is to identify and get the authorization data from the holder that is doing a blockchain transaction.

## DID Method Name

The namestring that shall identify this DID method is: `ct`

A DID that uses this method MUST begin with the following prefix: `did:ct`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID, after the prefix, is specified below.

## Method Specific identifier

ct.did = "did:ct" + IDEN3 Genesis ID (Identifies a holder)

### Example

```
did:ct:zuerR5X7JKmBM6CqtLmU6a8XWJhEaW1WDe2tZapCg
```

## DID document

### Example 

```
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://schema.iden3.io/core/jsonld/auth.jsonld"
  ],
  "id": "did:ct:zuerR5X7JKmBM6CqtLmU6a8XWJhEaW1WDe2tZapCg",
  "authentication": [
    {
      "id": "did:ct:zuerR5X7JKmBM6CqtLmU6a8XWJhEaW1WDe2tZapCg?state=example_state",
      "type": "Iden3StateInfo2023",
      "published": false,
      "info": {
        "id": "did:ct:zuerR5X7JKmBM6CqtLmU6a8XWJhEaW1WDe2tZapCg",
        "state": "0000000000000000000000000000000000000000000000000000000000000000",
        "replacedByState": "0000000000000000000000000000000000000000000000000000000000000000",
        "createdAtTimestamp": "0",
        "replacedAtTimestamp": "0",
        "createdAtBlock": "0",
        "replacedAtBlock": "0"
      }
    }
  ],
  "info": {
    "documentField": "this is an example of a field in the DIDDocument"
  },
  "active": true
}
```

## CRUD Operations Definition

### Create (Register)

A new `ct` DID can be created by an authorised holder who has the API Keys calling to the endpoint https://identityhub.blueroominnovation.com/api/v1/did/identity/createDID.

### Read (Resolve)

To get a DID document from a `ct` DID, the following steps are performed:

1- Call to the https://identityhub.blueroominnovation.com/api/v1/did/identity/resolveDid endpoint, passing the input DID as parameter.

2- Internally this endpoint will get the DIDDocument related to the input DID, and will return it.

3- Return the DID Document or an error 400 depending on the response of the endpoint.

### Update 

An existing `ct` DID can be updated by an authorised holder who has the API Keys calling to the endpoint https://identityhub.blueroominnovation.com/api/v1/did/identity/updateDID.

### Delete 

An existing `ct` DID can be deleted  by an authorised holder who has the API Keys calling to the endpoint https://identityhub.blueroominnovation.com/api/v1/did/identity/deleteDID.

## Security Considerations

There are some security considerations that implementers recommended to take into consideration when implementing this specification:

### Data Forgery Prevention

Our DID method prevents forgery and falsification through the usage of Digital Signatures, Merkle Tree Proofs, and Zero Knowledge Proofs (ZKPs) such that only the identity owner can issue credentials or present credentials to third parties. The identity owner can choose to A) Only issue credentials with digital signatures or; B) Issue claims with all both digital signatures and Merkle Tree Proofs. With digital signatures, only the controller of the DID Document is capable of issuing the credentials. When adding merkle tree proofs this adds an extra layer of forgery prevention by allowing the holder of the claim to demonstrate that 1) That the credential is currently valid, and 2) The credential has not been revoked recently. Both of these elements are used to create a zero knowledge proof which is presented the verifier of the claim (unless selective disclosure of credential data is used).

### Keep DID Keys safe

Care should be used when handling private keys, if the key is compromised then an atacker may access the authentication data.

## Privacy Considerations

The syntax and construction of the `ct` DID and its associated DID Document helps to ensure that no Personally Identifiable Information (PII) or other personal data is exposed, so this method specification is conformant with DID core specification that dictates that DID documents should not include any PII.