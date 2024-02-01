# Cofinity-X Context Schema Repository

## Overview

This repository serves as the central location for documenting and verifying the context schema for Cofinity-X. 
The context schema defines the structure and semantics of the context data used within the Cofinity-X system
in compliance to the Catena-X standard definitions for Credential formats. 


## Table of Contents

1. [Introduction](#introduction)
2. [Context Schema](#context-schema)
    - [W3C Verifiable credential schema](#w3c-verifiable-credential-schema)
    - [BusinesspartnerData Schema](#businesspartnerdata-schema)
        - [Membership Credential](#membership-credential)
        - [BPN Credential](#bpn-credential)
    - [UseCaseAgreement Schema](#usecasevc-schema)
    - [Dismantler Schema](#dismantler-schema)
    - [SummaryCredential Schema](#summary-schema)
3. [Data Types](#data-types)
4. [Relationships](#relationships)


## Introduction

The Cofinity-X system relies on a well-defined context schema to ensure accurate and meaningful interactions with users. This schema outlines the key entities, their attributes, and the relationships between them. By maintaining a clear and standardized context schema, we can achieve a higher level of accuracy in understanding and responding to user queries.


## Context Schemas

An overview of the given Schemas and Credentials in this Registry.


### W3C verifiable credential schema
 This is a clone schema from https://www.w3.org/ns/credentials/v2
 We added to avoid any production issue if w3c changes schema without any prior notice.



### BusinesspartnerData Schema

The BusinesspartnerData schema contains the **Membership** and the **BPN** Credential Schemas.

Schema Reference: [BusinesspartnerData](./v1.1/businessPartnerData)

#### BPN Credential

Property | Description
--- | ---
**id** | Id property that defines the Holder.
**type** | MUST contain "BpnCredential"
**bpn** | BPN value e.g. BPN000111222333

**Example:**
```
{
    "id": "UUID",
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        ....
    ],
    "type": ["VerifiableCredential", "BpnCredential"],
    "issuer": "<did>",
    "issuanceDate": "2021-06-16T18:56:59Z",
    "credentialSubject": {
        "id":"<did>",
        "type":"BpnCredential",
        "bpn":"bpn"
    }
}
```

 

#### Membership Credential

Property | Description
--- | ---
**id** | Id property that defines the Holder.
**type** | MUST contain "MembershipCredential"
**ex:startTime** | Datetime indicating the start time of the membership.
**memberOf** | Text indicating the group or organization the membership belongs to.
**ex:status** | Text indicating the status of the membership.
**holderIdentifier** | Identifier of the holders bpn number

**Example:**

```json
{
  "id": "UUID",
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "..."
  ],
  "type": ["VerifiableCredential", "MembershipCredential"],
  "issuanceDate": "2021-06-16T18:56:59Z",
  "expirationDate": "2022-06-16T18:56:59Z",
  "issuer": "did",
  "credentialSubject": {
    "id": "<did>",
    "type":"MembershipCredential",
    "holderIdentifier": "bpn",
    "memberOf":"Catena-X",
    "status":"Active",
    "startTime":"2021-06-16T18:56:59Z"
  }
}
```

### UseCaseVC Schema

The Schema contains the Contract Template for the UseCase Agreement
Schema Reference: [UseCaseAgreement](./v1.1/UseCaseVC)


Name | Description
--- | ---
**UseCaseAgreement** | Credential for Agreement to the UseCases

This Credential can have different Types so that it gets issued in reference to the applied UseCase:

Name | Description
--- | ---
**BehaviorTwinCredential** | Credential for Use Case Behaviour Twin
**SustainabilityCredential** | Credential for Use Case Sustainability
**QualityCredential** | Credential for Use Case Quality
**TraceabilityCredential** | Credential for Tracability
**ResiliencyCredential** | Credential for Use Case Resiliency
**PcfCredential** | Credential for Use Case PCF

**Example:**
```
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "..."
    ],    
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkCondition"],    
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",    
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN of holder", 
        "type": "SustainabilityCredential | BehaviorTwinCredential |QualityCredential ...", // UseCase Specific Entry
        "contractTemplate": "https://public.catena-x.org/contracts/<UseCase>.v1.pdf",
        "contractVersion": "1.0.0"   
    }
}
```

### Dismantler Schema

The Schema contains the Dismantler Credential Template

Schema Reference: [DismantlerSchema](./v1.1/DismantlerVC)

Property | Description
--- | ---
**id** | Id property that defines the Holder.
**type** | MUST contain "MembershipCredential"
**holderIdentifier** | Datetime indicating the start time of the membership.
**allowedVehicleBrands** | Text indicating the group or organization the membership belongs to.
**activityType** | Text indicating the status of the membership.

**Example:**
```
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "..."
    ],
    "id": "UUID",
    "issuer": "<did>",
    "type": ["VerifiableCredential", "DismantlerCredential"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",
    "credentialSubject": {
        "id": "<did>",
        "type": "DismantlerCredential", 
        "holderIdentifier": "<BPN>",
        "allowedVehicleBrands": ["CarBrand1", "CarBrand2", "CarBrand3"] 
    }
}
```


## Summary Schema

The Summary Credentials is an Credential which sums up the Owned CX Credentials in one VC.

Schema Reference: [SummarySchema](./v1.1/SummaryVC)


Property | Description
--- | ---
**id** | Id property that defines the contract template identity.
**type** | MUST contain "SummaryCredential"
**holderIdentifier** | Identifier of the holder (http://schema.org/identifier)
**items** | List of items (https://schema.org/ItemList)
**contractTemplate** | Text indicating the type of contract (https://schema.org/Text)

---

**Example**
``` json
 {
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "..."
  ],
  "id": "<credential uid>",
  "type": [
    "VerifiableCredential",
    "SummaryCredential"
  ],
  "issuer": "<did:web:issuer>",
  "issuanceDate": "2023-06-02T12:00:00Z",
  "expirationDate": "2022-06-16T18:56:59Z",
  "credentialSubject": {
    "id": "<did:web:subject>",
    "holderIdentifier": "<BPN>",
    "type": "SummaryCredential",
    "items": [
      "MembershipCredential",
      "DismantlerCredential",
      "PcfCredential",
      "SustainabilityCredential",
      "QualityCredential",
      "TraceabilityCredential",
      "BehaviorTwinCredential",
      "BpnCredential"
    ],
    "contractTemplates": "https://public.catena-x.org/contracts/"
  }
}
```


# Data Types
The context schema uses the following data types:
- `https://schema.org/Text`: Represents textual data.
- `http://schema.org/identifier`: Represents unique identifiers.
- `https://schema.org/ItemList`: Represents of a list.
- `https://schema.org/DateTime`: Represents as a Date Time
- `https://schema.org/Float`: Represents a float value.
- `https://schema.org/memberOf`: Represents a Membership to the Dataspace
- `https://schema.org/startTime`: Represents as a Date Time

## Relationships

The given Schemas in this Registry are designed for Compliance with Catena-X defined standard Credentials:

https://catena-x.net/de/standard-library

