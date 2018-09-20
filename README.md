# Open API for FSP Interoperability Specification
The Open API for FSP Interoperability Specification includes the following documents.

#### General Documents
* [Glossary](#glossary)
#### Logical Documents
* [Logical Data Model](#logical-data-model)
* [Generic Transaction Patterns](#generic-transaction-patterns)
* [Use Cases](#use-cases)
#### Asynchronous REST Binding Documents
* [API Definition](#api-definition)
* [JSON Binding Rules](#json-binding-rules)
* [Scheme Rules](#scheme-rules)
#### Data Integrity, Confidentiality, and Non-Repudiation
* [PKI Best Practices](#pki-best-practices)
* [Signature](#signature)
* [Encryption](#encryption)

## Glossary
This document provides the glossary for the Open API (Application Programming Interface) for FSP (Financial Service Provider) Interoperability (hereafter cited as "the API"). Terms have been compiled from three sources:
•	ITU-T Digital Financial Services Focus Group Glossary (ITU-T),
•	Feedback from Technology Service Providers (TSPs) in the PDP work groups (PDP) and
•	Feedback from the L1P IST Reference Implementation team (RI).
Information is shared in accordance with Creative Commons Licensing.

## Logical Data Model
This document introduces the four generic transaction patterns that are supported in a logical version of the API. Additionally, all logical services that are part of the API are presented on a high-level.

## Generic Transaction Patterns
This document specifies the logical data model used by the API. Section 2 in the document lists elements used by each service. Section 3 in the document describes the data model in terms of basic elements, simple data types and complex data types.

## Use Cases
The purpose of this document is to define a set of use cases that can be implemented using the API. The use cases referenced within this document provide an overview of transaction processing flows and business rules of each transaction step as well as relevant error conditions. The primary purpose of the API is to support the movement of financial transactions between one Financial Services Provider (FSP) and another.

It should be noted that the API is only responsible for message exchange between FSPs and a Switch when a cross-FSP transaction is initiated by an End User in one of the FSPs. This can occur in either of two scenarios: 
- A bilateral scenario in which FSPs communicate with each other
- A Switch based scenario in which all communication goes through a Switch 

Reconciliation, clearing and settlement after real time transactions is out of scope for the API. Additionally, account lookup is supported by the API, but it relies on the implementation in a local market in which a third party or Switch would provide such services. Therefore, the need for effective on-boarding processes and appropriate scheme rules must be considered when implementing use cases.

## API Definition
The **API Definition** document introduces and describes **the API**. The purpose of the API is to enable interoperable financial transactions between a Payer (a payer of electronic funds in a payment transaction) located in one FSP (an entity that provides a digital financial service to an end user) and a Payee (a recipient of electronic funds in a payment transaction) located in another FSP. The API does not specify any front-end services between a Payer or Payee and its own FSP; all services defined in the API are between FSPs. FSPs are connected either (a) directly to each other or (b) by a Switch placed between the FSPs to route financial transactions to the correct FSP. 
The transfer of funds from a Payer to a Payee should be performed in near real-time. As soon as a financial transaction has been agreed to by both parties, it is deemed irrevocable. This means that a completed transaction cannot be reversed in the API. To reverse a transaction, a new negated refund transaction should be created from the Payee of the original transaction.  

The API is designed to be sufficiently generic to support both a wide number of use cases and extensibility of those use cases, However, it should contain sufficient detail to enable implementation in an unambiguous fashion.  
Version 1.0 of the API is designed to be used within a country or region; international remittance that requires foreign exchange is not supported. This version also contains basic support for the Interledger Protocol, which will in future versions of the API be used for supporting foreign exchange and multi-hop financial transactions.

This document:
- Defines an asynchronous REST binding of the logical API introduced in Generic Transaction Patterns.
- Adds to and builds on the information provided in Open API for FSP Interoperability Specification. The contents of the Specification are listed in Section **Open API for FSP Interoperability Specification**.

## Scheme Rules
This document defines scheme rules for Open API for FSP Interoperability (hereafter cited as the API) in three categories.
1.	**Business** Scheme Rules:   
a.	These business rules should be governed by FSPs and an optional regulatory authority implementing the API within a scheme.   
b.	The regulatory authority or implementing authority should identify valid values for these business scheme rules in their API policy document.   
2.	**API implementation** Scheme Rules:   
a.	These API parameters should be agreed on by FSPs and the optional Switch. These parameters should be part of the implementation policy of a scheme.   
b.	All participants should configure these API parameters as indicated by the API-level scheme rules for the implementation with which they are working.   
3.	**Security** and **Non-Functional** Scheme Rules.   
a.	Security and non-functional scheme rules should be determined and identified in the implementation policy of a scheme.   

## JSON Binding Rules
The purpose of this document is to express the data model used by **the API** in the form of JSON Schema binding rules, along with validation rules for the corresponding instances.

This document adds to and builds on the information provided in Open API for FSP Interoperability Specification. The contents of the Specification are listed in Section 1.1.
The types used in the PDP API fall primarily into three categories:
- Basic data types and Formats used
- Element types
- Complex types

The various types used in API Definition, Data Model and the Open API Specification, as well as the JSON transformation rules to which their instances must adhere, are identified in the following sections.

## PKI Best Practices
This document explains Public Key Infrastructure (PKI)  best practices to apply in **the API** deployment. See Chapter 2, PKI Background, for more information about PKI. 
The API should be implemented in an environment that consists of either:
- Financial Service Providers (FSPs) that communicate with other FSPs (in a bilateral setup) or 
- A Switch that acts as an intermediary platform between FSP platforms. There is also an Account Lookup System (ALS) available to identify in which FSP an account holder is located.

For more information about the environment, see Chapter 3, Network Topology. Chapters 4 and 5 identify management strategies for the CA and for the platform. Communication between platforms is performed using a REST (REpresentational State Transfer)-based HTTP protocol (for more information, see API Definition). Because this protocol does not provide a means for ensuring either integrity or confidentiality between platforms, extra security layers must be added to protect sensitive information from alteration or exposure to unauthorized parties.
