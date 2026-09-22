# Aurora — Open Credit-Market Infrastructure for Cardano

**Open infrastructure for bringing real credit markets to Cardano.**

Aurora is shared market infrastructure for Cardano credit markets. It provides the standards, software and developer tooling required to make independent credit opportunities discoverable, filterable, verifiable and accessible through common interfaces.

The infrastructure combines standardized metadata, verification, discovery and indexing, filtering and query tooling, open APIs, capital-provider standards and developer tooling around compatible Cardano lending implementations.

The resulting components are designed as reusable parts of Cardano's credit-market stack and will be released as open-source infrastructure under Apache License 2.0.

## Proposal Alignment

This repository is the primary implementation home for technical outputs defined in the Aurora Treasury Proposal. The proposal itself is maintained in the [Aurora proposal repository](https://github.com/fairway-global/aurora-proposal).

| Field | Detail |
| --- | --- |
| Treasury request | **940,000 ADA** |
| Delivery period | Approximately **5 months** |
| Delivery plan | **4 implementation milestones** |
| Lead implementer | **Fairway** |
| Technical collaborator | **Sundial** |
| Technical advisor | **Fallen Icarus (Rusty)** |
| Treasury custody | Independent **3-of-5 Aurora Treasury multisignature** |
| Treasury administrators | **James "Blockjock" Meidinger, Christian Taylor, Elder Millennial, Wilco USDM, and Kriss Baird** |
| License | **Apache License 2.0** |

## Scope

### Core Public Outputs

- **Metadata Standard** — a shared machine-readable structure for describing Aurora-compatible credit opportunities and associated metadata references.
- **Verification Framework** — an extensible framework for associating and evaluating institutional, eligibility, compliance and other proof-based information across different verification systems.
- **Aurora Discovery Engine** — open-source infrastructure for indexing compatible Loan Request UTxOs and making independent credit opportunities searchable across Cardano.
- **Filtering & Query Tooling** — common filtering and query capabilities for finding opportunities according to jurisdiction, duration, asset, ticket size, verification requirements and other standardized attributes.
- **Open APIs** — public interfaces for querying credit opportunities, metadata, verification information and relevant lifecycle data.
- **Capital Provider Profile + Reference Query Library** — open standards and reference queries for representing capital-provider requirements and translating them into reusable market queries.
- **Developer Tooling + Reference Implementation** — tooling, integration examples and reference code demonstrating how third-party applications can integrate the complete Aurora infrastructure flow.
- **Documentation + Independent Review** — technical and operating documentation backed by independent security and legal review.

Delivery culminates in an **end-to-end testnet demonstration and public open-source release under Apache License 2.0**.

The Capital Provider Profile Standard, Reference Query Library, Discovery and Filtering Specification, Market Discovery API contributions and related integration artifacts collectively form Aurora's **Capital Discovery Layer**, developed with selected technical contributions from Sundial.

### Operating Model

Aurora operates as shared market infrastructure around compatible Cardano lending implementations. Lending protocols retain their own contract logic, origination, underwriting, funding and settlement processes, while Aurora provides common standards and infrastructure for market information, discovery, filtering and verification.

Participation is optional and protocol-independent. Different lending implementations, verification systems and capital providers can use the infrastructure according to their own technical, legal, risk and eligibility requirements.

## Architecture

Aurora operates around compatible lending infrastructure without modifying its core lending contracts.

```mermaid
flowchart LR
    A["Compatible lending implementation"] --> B["Loan Request UTxO"]
    B --> C["Standardized metadata and verification references"]
    V["Verification providers and proof systems"] --> C
    C --> D["Aurora Discovery Engine"]
    D --> E["Open APIs + Filtering & Query Tooling"]
    P["Capital-provider profiles and reference queries"] --> E
    E --> F["Applications and capital providers"]
```

### Processing Flow

1. **Origination.** An originator creates a Loan Request UTxO through compatible Cardano lending infrastructure. In the proposal, this means a UTxO representing an individual funding request or credit opportunity.
2. **Metadata.** The originator may attach standardized market information and verification references. The proposal describes an enriched object as a "colored" Loan Request UTxO; this is a descriptive term, not a new ledger primitive.
3. **Indexing and verification.** The Aurora Discovery Engine identifies compatible UTxOs, organizes their metadata, and exposes relevant verification information.
4. **Discovery and evaluation.** Applications and capital providers query and filter opportunities according to their own requirements.
5. **Lifecycle visibility.** Aurora indexes relevant lifecycle information made available by compatible lending implementations, including on-chain repayment events where available.
6. **Funding and settlement.** Capital allocation, loan execution, settlement, and servicing remain with the underlying lending infrastructure and relevant market participants.

Aurora exposes information for evaluation but does not make lending, underwriting, compliance, or capital-allocation decisions.

## Design Principles

- **Protocol-independent.** Compatible lending implementations can integrate Aurora while retaining their own lending architecture.
- **Optional.** Aurora extends compatible credit markets without becoming a requirement of the underlying lending contracts.
- **Extensible.** Versioned schemas support evolving market information, jurisdictions, verification methods and participant requirements.
- **Verification-agnostic.** Different credential systems, proof systems, attestations and verification providers can coexist through common interfaces.
- **Privacy-compatible.** Verification references can support proofs, attestations and selective disclosure without requiring sensitive source data on Cardano.
- **Independently operable.** Open-source software, published interfaces and deployment documentation allow third parties to operate and extend the infrastructure.

## Planned Repository Structure

```text
.
|-- specifications/
|   |-- metadata-standard/
|   |-- verification-framework/
|   |-- capital-provider-profile/
|   `-- discovery-and-filtering/
|-- discovery-engine/
|   |-- src/
|   |-- api/
|   `-- deployment/
|-- capital-discovery/
|   |-- reference-query-library/
|   `-- integration-artifacts/
|-- developer-tooling/
|-- reference-implementation/
|-- examples/
|-- demo/
|-- docs/
|-- LICENSE
`-- README.md
```

The planned `capital-discovery/` area groups the Reference Query Library and related integration artifacts within Aurora; it is not a standalone product.

The structure may evolve during M1 architecture work. Any change must preserve the approved public deliverables, protocol independence, and third-party operability.

## Technical Demonstration

The testnet demonstration will show that a compatible Loan Request UTxO can be:

1. created through compatible lending infrastructure;
2. enriched with standardized metadata;
3. identified and indexed by the Aurora Discovery Engine;
4. discovered through an open API;
5. filtered according to published criteria;
6. associated with verification information that can be evaluated through the Verification Framework; and
7. consumed by a compatible reference application or query workflow.

The demonstration validates the end-to-end operation and interoperability of the infrastructure, from Loan Request UTxO creation and metadata through discovery, filtering, verification, and application-level consumption.

## Budget Allocation

The Treasury request is allocated to public deliverables rather than separate organizational work packages. Approximate USD values use the proposal's reference price of **US$0.20 per ADA**.

| Allocation | ADA | Approx. USD | Primary scope |
| --- | ---: | ---: | --- |
| **Core Infrastructure Development** | **800,000** | **$160,000** | Standards, Discovery Engine, APIs, filtering, tooling, reference implementation, Capital Discovery Layer, demonstration, documentation, and delivery |
| **Review, Hosting & Technical Contingency** | **140,000** | **$28,000** | Independent review, Treasury-use oversight, hosting, technical operations, and approved contingency |
| **Total** | **940,000** | **$188,000** | |

The second allocation comprises approximately **60,000 ADA** for independent security and legal review, **20,000 ADA** for independent Treasury-use audit and oversight, **30,000 ADA** for hosting and technical operations, and **30,000 ADA** for technical contingency.

## Milestone Roadmap

| Milestone | Timeline | ADA allocation | Primary outcome |
| --- | --- | ---: | --- |
| **M1: Specifications and Architecture** | Month 1 | **140,000** | Core standards and implementation architecture finalized |
| **M2: Core Build** | Months 2-3 | **320,000** | Discovery, verification, indexing, filtering, and API infrastructure operational on testnet; interim Treasury-use review published |
| **M3: Integration and Technical Demonstration** | Month 4 | **290,000** | Reference implementation, developer tooling, and complete testnet workflow demonstrated |
| **M4: Independent Review and Public Release** | Month 5 | **190,000** | Independent review completed and final open-source infrastructure released |
| **Total** | **Approximately 5 months** | **940,000** | |

Public milestone evidence and progress reports will link to the relevant specifications, source code, APIs, tooling, documentation, demonstrations, and review materials.

## Delivery Roles

| Participant | Responsibility |
| --- | --- |
| **Fairway** | Lead implementation, integration, standards development, engineering, documentation, testing, external reviews, milestone evidence, and public reporting |
| **Sundial** | Selected technical contributions to capital-provider standards, discovery and filtering specifications, reference queries, API design, integration examples, and interoperability |
| **Fallen Icarus (Rusty)** | Technical advice and architectural review related to transaction-based credit markets, Loan Request UTxO design, and eUTxO-specific implementation considerations |

These roles form one integrated Aurora implementation. They do not create separate Treasury budgets, custody arrangements, governance tracks, or ownership rights over the funded public outputs.

## Treasury Governance

The full 940,000 ADA Treasury allocation will be received into one dedicated **3-of-5 Aurora Treasury multisignature** administered by James "Blockjock" Meidinger, Christian Taylor, Elder Millennial, Wilco USDM, and Kriss Baird. All five administrators are independent of the implementation participants. Fairway, Sundial, Fallen Icarus, and other implementation contributors hold no Treasury signing keys.

Expenditure may progress only after milestone evidence is published and reviewed by the Aurora Treasury Administrators. The cumulative ceilings are **140,000 ADA** at commencement, **460,000 ADA** after M1 approval, **750,000 ADA** after M2 approval, and **940,000 ADA** after M3 approval. The Core Infrastructure Development allocation is monitored against the approved deliverables and milestone outputs, with material resource-allocation changes disclosed through milestone reporting. Use of technical contingency requires written justification, administrator authorization, and disclosure in the next public milestone report; unused contingency remains unspent Treasury ADA.

Independent oversight includes an interim expenditure and reconciliation review after M2 and a final Treasury-use audit after M4. Treasury balances and transactions remain publicly auditable. Unspent ADA is returned to the Cardano Treasury if the project terminates under the proposal's conditions.

Governance details, expenditure ceilings, remediation conditions, and submission requirements are maintained in the [Aurora proposal repository](https://github.com/fairway-global/aurora-proposal).

## Status

Aurora is ready to begin development as open-source Cardano credit-market infrastructure. Treasury-funded implementation has not started and will begin only after approval and enactment of the Treasury Withdrawal governance action and receipt of funds.

This repository is the implementation home for the standards, software, tooling and technical demonstration defined in the Aurora Treasury Proposal. Public outputs will be published here against the approved milestone schedule.

## License

Unless stated otherwise, this repository is licensed under the [Apache License 2.0](LICENSE). Treasury-funded software, standards, and reference implementations may be used, operated, modified, extended, and commercialized in accordance with that license.

## Links

- [Aurora Proposal Repository](https://github.com/fairway-global/aurora-proposal)
- [Fairway](https://fairway.global)

---

Built by [Fairway Oy](https://fairway.global) with technical collaboration from Sundial Protocol and advisory input from Fallen Icarus.
