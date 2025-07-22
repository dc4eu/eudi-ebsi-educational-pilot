# EUDI-EBSI Educational Pilot

This repository serves as an entry point to a prototype developed by GRNET, aimed at 
enhancing the
[EUDI Wallet Reference Implementation](https://github.com/eu-digital-identity-wallet) (RI)
with support for EBSI-compliant 
Verifiable Credentials (VCs). The work addresses the objective of implementing a complete 
end-to-end flow for issuing, holding, and verifying EBSI-trusted credentials using real DIDs 
onboarded into the EBSI Pilot Registry.

## Overview

The implementation extends all three RI components (Issuer, Wallet, Verifier) while maintaining 
compatibility with their original architecture and data exchange formats. Due to language and 
tooling mismatches, EBSI functionality is encapsulated in a dedicated microservice (EBSI-Agent), 
which wraps the EBSI Hub Libraries and exposes them via a REST API. Additionally, several core 
RI libraries—such as `document-manager` and `wallet-core`—were modified to support conditional 
EBSI logic, credential enrichment, and coroutine-compatible verification handling.

## Repositories

The full prototype is organized into the following component repositories:

- **Issuer Extension**  
  ([TODO](TODO))  
  Extends the RI Issuer to delegate VC issuance to the EBSI-Agent and wrap the resulting token 
  in the standard transport structure used by the RI Wallet.

- **Wallet Extension**  
  ([https://github.com/dc4eu/eubi-ebsi-wallet-app](https://github.com/dc4eu/eubi-ebsi-wallet-app))
  Adds EBSI-aware credential verification support to the RI Wallet by parsing received credentials, 
  conditionally invoking the EBSI-Agent, and enriching internal structures with verified metadata.

- **Verifier Backend Extension**  
  ([https://github.com/dc4eu/eudi-ebsi-verifier-backend](https://github.com/dc4eu/eudi-ebsi-verifier-backend))  
  Extends the Verifier backend to extract EBSI credentials from submitted payloads and invoke the EBSI-Agent 
  for final trust validation after all local checks pass.

- **Verifier Frontend Extension**  
  ([https://github.com/dc4eu/eudi-ebsi-verifier-ui](https://github.com/dc4eu/eudi-ebsi-verifier-ui))  
  Extends the Verifier UI to align with the modified Verifier backend (see above).

- **EBSI-Agent Service**  
  ([https://github.com/dc4eu/eudi-ebsi-agent](https://github.com/dc4eu/eudi-ebsi-agent))
  A standalone Node.js microservice exposing the EBSI Hub Libraries over a RESTful interface. 
  It handles DID creation/resolution, VC/VP issuance, and verification in a technology-agnostic way.

- **Document Manager Extension**  
  ([https://github.com/dc4eu/eudi-ebsi-document-manager](https://github.com/dc4eu/eudi-ebsi-document-manager))
  Enhances the RI Wallet’s document lifecycle library with support for recognizing and processing 
  EBSI credentials, including token extraction and data enrichment workflows.

- **Wallet Core Extension**  
  ([https://github.com/dc4eu/eubi-ebsi-wallet-core](https://github.com/dc4eu/eubi-ebsi-wallet-core))  
  Introduces coroutine-based support for remote credential verification into the wallet-core library. 
  It ensures that asynchronous EBSI verification can be integrated with existing synchronous workflows.
