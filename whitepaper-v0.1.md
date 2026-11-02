# Decidra Whitepaper

Version 0.1 · Public discussion draft · 2 November 2026

Rights-aware data infrastructure and bounded service access for AI agents.

## 1. Executive summary

Decidra is building a data marketplace in which people and AI agents can discover datasets, inspect their provenance and licensing, and access approved data through controlled service interfaces. Its starting point is a working local application, rather than a token sale: DataHub normalizes business files and exposes data APIs; Marketplace adds reviewed listings, public metadata and bounded samples; a new off-chain credit pilot adds dataset entitlements, agent budgets and auditable export jobs.

The proposed role of a Decidra token is optional service-credit redemption and ecosystem coordination. Token redemption is not implemented. The application currently uses nontransferable TEST_CREDIT accounting units with no monetary value. It remains usable without holding a transferable token.

A fixed-supply prototype called Decidra Prototype, symbol DCDTEST, has been deployed on BSC Testnet, chain ID 97. Its token, allocation bundle and three vesting contracts have passed explorer source-code verification. This does not constitute an independent security audit, a mainnet launch, a production supply decision or approval of token economics.

This publication explains implemented capabilities, the deployed testnet allocation and the remaining work. It does not announce a token sale or accept payments. There is no approved token price, fundraising valuation, mainnet address, exchange listing or token-to-service conversion rate.

## 2. The problem and intended users

An agent finding a dataset needs more than a title or download link. It needs to know where the records came from, which version it is evaluating, which fields are present, what quality measurements mean and whether the license permits the intended use. A useful sample must not reveal confidential records or enable reconstruction of an entire dataset through repeated public requests.

Businesses also need private files converted into predictable, validated structures without accidentally publishing those files. Agent owners need a way to delegate a task without handing an agent a wallet key or permitting unlimited service consumption.

Decidra addresses these needs for developers, researchers, data suppliers, business workspaces and owners of data-consuming agents. Its initial domains include historical market data and structured enterprise files. It does not provide automatic trading, live order execution or investment recommendations.

## 3. What exists today

| Capability | Status at this version |
|---|---|
| CSV/XLSX/text-layer PDF normalization, validation and JSON/CSV exports | Implemented in the local DataHub application; scanned-document OCR is excluded |
| Workspace accounts, scoped/revocable API keys and usage reporting | Implemented with server-side authorization and tenant isolation |
| Seller submissions and operator publication review | Implemented; publication approval is distinct from merely uploading a file |
| Public catalog, machine-readable metadata and bounded reviewed samples | Implemented through REST/OpenAPI and read-only MCP discovery |
| Licensed-source collection and monthly topic/weekly planning tools | Implemented local workflows; source permissions and observations still require review |
| Off-chain test-credit ledger, per-key budgets and reviewed dataset access | Implemented local pilot, including an English owner/admin interface |
| Bounded agent export jobs, settlement and unused-credit release | Implemented for the test-credit export service |
| DCDTEST token and funded vesting contracts | Deployed and source-verified on BSC Testnet |
| Wallet-linked token redemption into application credits | Planned; not implemented |
| Real checkout, seller payouts, public token sale or mainnet issuance | Not enabled |

The application is currently local-only. The public availability of this document or of testnet contracts does not mean that the application is publicly hosted or production-ready. Paying customers, commercial revenue, independent pilot adoption and production uptime are not established by the current engineering evidence.

## 4. Actors and the data-rights model

- Buyers and agent owners operate in workspaces. Their keys and access grants are scoped to that workspace.
- Sellers submit data products and evidence of rights, provenance, permitted uses and limitations. Seller statements are claims to be reviewed, not automatically verified facts.
- Platform administrators review publication and grant narrowly defined test access. Their authority is an explicit backend role, not a username or an assertion sent by a browser.
- Agents use delegated API credentials to discover information or execute a bounded approved job. They receive neither an owner's wallet private key nor unrestricted purchasing authority.
- Curators and contributors are proposed future participants in quality tasks and dataset bounties. Automatic token rewards are not active.

Public metadata and samples do not grant unrestricted access to private source data. A test entitlement identifies a receiving workspace, a fixed publication revision, approved columns, an inference use and an expiry. Full-export permission requires separate operator evidence; permission to display a public sample alone is insufficient.

Token possession never overrides a license, publication decision, tenant boundary or data-access restriction. An entitlement does not automatically transfer copyright or grant redistribution or AI-training rights. Dataset bodies, credentials and personal information stay off-chain. Source verification cannot establish the truth of data or the legality of its distribution.

## 5. The current credit and agent workflow

The local pilot uses TEST_CREDIT. One test credit equals 1,000,000 integer microcredits. This is an accounting scale, not a currency peg, token exchange rate or redeemable financial balance. Test credits cannot be transferred between customers, withdrawn or redeemed for money.

An administrator can issue a reasoned, capped test grant. The owner then selects an active datasets:read API key, an entitled dataset and daily/lifetime limits. The agent submits a bounded export request with an idempotency key. The system reserves the maximum charge before work, makes the result durably available, settles the actual charge and returns the unused reservation. Failed or cancelled unfinished jobs release the full reservation.

The first service is TEST_EXPORT_V1: at most 1,000 rows and a 500 KB entitlement snapshot. Its experimental charge is 1,000 microcredits per returned row. A request for at most 100 rows reserves 0.1 test credits; returning 12 rows charges 0.012 and returns 0.088. These figures demonstrate accounting behavior only. They are not measured commercial prices and have no conversion into DCDTEST.

Agent budgets count both reserved and settled usage. A request retains its original UTC daily bucket across midnight, and a lifetime limit prevents rollover from creating unlimited spending authority. Repeating the same request does not create another reservation or charge; reusing its idempotency key with a changed payload is rejected.

Owners can pause an agent or revoke its key. New jobs are blocked and the worker releases unauthorized pending reservations. Data access is rechecked for result retrieval, so a suspended publication or expired entitlement cannot be bypassed using an old job ID. Previously downloaded data cannot be retracted from a recipient's files.

Public discovery and reviewed public samples remain free. Existing private-workspace DataHub routes retain their original access and quota behavior; the pilot does not silently convert every API request or login into a billable event.

## 6. Proposed token utility and the decision to integrate

The intended sequence is owner-authorized token redemption into nontransferable service credits, followed by agent consumption of those credits. The owner would approve a bounded transaction for a transparent quote; the agent would continue using a scoped API key rather than signing transactions for every data request.

This design is conditional. Before building redemption, Decidra must measure service costs, compare the workflow against ordinary prepaid credits and establish whether transferable access or independently verifiable receipts provide useful interoperability. If an ordinary credit account meets the need with less complexity, token integration should be deferred.

Other proposed utilities are milestone-based dataset bounties, capped rewards for demonstrably useful contributions and advisory prioritization of supported topics. They are not implemented reward or governance programs. Uploading more datasets does not automatically earn tokens. Contribution rewards would require verified rights, quality, demand and anti-abuse controls, with explicit budgets.

Holding a token does not create a right to profit, dividends, fixed yield, guaranteed discounts, price appreciation, buybacks, liquidity or an exchange listing. No governance process could override privacy, licensing or security obligations, or make a centrally operated API trustless.

## 7. DCDTEST: the deployed testnet prototype

| Property | Deployed prototype |
|---|---|
| Network | BSC Testnet, chain ID 97 |
| Contract name / symbol | Decidra Prototype / DCDTEST |
| Decimals | 18 |
| Fixed initial supply | 100,000,000 DCDTEST |
| Subsequent privileged minting | No mint endpoint |
| Token ownership, pause, blacklist, transfer tax or upgrade control | None in the token contract |
| Service-credit redemption or public presale | Not included in the deployed contracts |

The token uses standard transfers and allowances. A separate allocation constructor created the token and atomically funded the three vesting escrows and two liquid reserves. Its chain guard permits testnet 97 and local simulation 31337 and rejects mainnet 56. The individual token and vesting primitives do not themselves have that chain restriction.

All five recipient roles currently use one wallet: `0xb55B69fC4ea1dBE68F9B118FE4C573E8c8842ca4`. This is a single-controller test setup. Different allocation labels do not create independent oversight, a multisig treasury or separate legal ownership.

Do not send assets to these contracts expecting service credits. No redemption mechanism is active, and the allocation bundle has no rescue function for accidental transfers.

## 8. Testnet allocation and vesting

The following is the deployed prototype configuration, not an approved mainnet allocation or an invitation to purchase tokens. All times are UTC. The common reference time T is 3 November 2026 at 14:00 UTC (21:00 Bangkok).

| Allocation | Tokens | Share | Cliff / release begins | Fully vested |
|---|---|---|---|---|
| Ecosystem | 35,000,000 | 35% | 3 Nov 2026, 14:00 UTC | 3 Nov 2031, 14:00 UTC |
| Development treasury | 30,000,000 | 30% | 3 May 2027, 14:00 UTC | 3 May 2031, 14:00 UTC |
| Founder/team | 20,000,000 | 20% | 3 Nov 2027, 14:00 UTC | 3 Nov 2030, 14:00 UTC |
| Financing reserve | 10,000,000 | 10% | Liquid at creation | No contract lock |
| Liquidity reserve | 5,000,000 | 5% | Liquid at creation | No contract lock |

At creation, 85,000,000 tokens were placed in funded vesting escrows and 15,000,000 were immediately transferable reserves. That 15% must not be described as locked. Allocation to a financing or liquidity reserve does not authorize a sale, establish a market or prove actual market circulation.

Vesting releases continuously in seconds after each cliff, not in monthly batches. At or before the cliff, vested value is zero; between cliff and end it is the allocation multiplied by elapsed time divided by duration, rounded down to base units; at or after the end the full allocation is vested. There is no catch-up payment for time before the cliff.

Anyone may trigger release, but payment always goes to the fixed beneficiary. The beneficiary, token, allocation, cliff and end are immutable. There is no owner-controlled replacement, rescue or upgrade. Extra tokens transferred into an escrow do not increase its grant and may remain locked. Ecosystem vesting makes a spending ceiling available to its beneficiary; contribution quality and budget approvals are not enforced by that vesting contract.

## 9. Treasury, governance and funding

The prototype treasury is controlled by the single recipient wallet disclosed above. A future operational treasury would need genuinely independent signers, published spending policies, budget limits and periodic reports. A founder holding several keys alone would not constitute independent governance. Multisig operation and token-holder voting are not implemented by these contracts.

Development funding and token issuance are separate workstreams. Grants and validation support can fund product engineering without a token sale. Potential recurring revenue would come from useful data/API services or enterprise engagements after demand and pricing have been validated. No paying-customer or financing outcome is assumed here.

Service prices must account for compute, provider charges, storage and egress, support, fixed operating costs, refunds and applicable taxes. These inputs are currently unmeasured in the credit worksheet. No public price, valuation, token-redemption rate or funding commitment is established by this paper. A financing reserve is an allocation label, not proceeds or an active offer.

## 10. Architecture and security boundaries

Decidra uses React/TypeScript, FastAPI/Python and PostgreSQL, with native local and Docker Compose paths. REST/OpenAPI is the canonical data interface. MCP is a read-only discovery adapter and does not provide unrestricted purchasing, publishing, SQL or URL-execution capabilities.

Credit accounting is off-chain and uses balanced, append-only journal postings. PostgreSQL checks complete transactions, rejects cross-tenant posting patterns, protects nonnegative workspace account balances, and prevents journal updates, deletion and truncation. The system issuance account is the negative contra account for test grants. Unique operation and idempotency constraints prevent duplicate reservations and terminal charges. Runtime roles cannot alter schema, grant platform-admin status or rewrite the journal.

The current worker performs only bounded internal exports. Work, durable result and settlement are fenced by database locks in a short transaction; a crash before commit rolls back settlement and leaves a recoverable reservation. It does not make external provider calls during the charged job. General external agent actions would require additional side-effect and recovery design.

Results are available for up to 24 hours, bounded by entitlement expiry. Access checks apply even before background cleanup runs. Expired data payloads are purged while immutable accounting and licensing metadata remain; backup retention is a separate operator responsibility. Publication review, privacy redaction and source attribution remain necessary. A database administrator can still alter database controls; this is not a permissionless or administrator-proof service.

## 11. What testnet redemption still requires

The existing ERC20 and vesting contracts do not redeem credits. A future testnet integration would require a separately reviewed redemption contract and explicit owner confirmation. Required controls include:

- Domain-, nonce-, tenant- and chain-bound expiring wallet-link signatures with replay protection.
- Versioned quotes that state the exact token amount, credit amount, expiry, fees and service obligations; a confirmed quote cannot silently change with token volatility.
- Allowlisted chain, token, contract, recipient and event verification; a supplied transaction hash or arbitrary transfer is insufficient evidence of redemption.
- Canonical confirmation and reorganization handling, unique event consumption and atomic, idempotent credit issuance.
- Bounded token authorization rather than an unlimited default allowance; documented refunds, suspended redemption and reconciliation of credits already used after an invalidated event.

These are design requirements, not claims of implemented functionality. No oracle, production exchange rate, seller settlement or real-money refund system has been selected or activated.

## 12. Roadmap and acceptance gates

| Stage | Current position | Exit evidence |
|---|---|---|
| DataHub and agent discovery | Implemented local MVP | Tenant/security tests, reviewed metadata/samples and reproducible API workflows |
| Token and vesting inventory | Current prototype deployed and source-verified | Public addresses, bytecode/source correspondence and allocation evidence |
| Off-chain credit pilot, C-001–C-004 | Implemented and locally tested | Owner UI, bounded agent jobs, grants, budgets, entitlements, concurrency/recovery checks |
| Service economics and pilot comparison, C-005 | Next work | Measured costs, actual user findings and an API-only comparison; no invented adoption |
| Isolated DCDTEST redemption, C-006 | Planned after C-005 and reviewed design/terms | Wallet replay, event duplication, chain mismatch, reorg and credit-reconciliation tests |
| Issuance readiness | Not complete | Independent security review, operational capacity, entity/jurisdiction/offer/tax decisions and treasury disclosures |
| Mainnet or exchange decision | Not scheduled | Separate explicit decision, applicable requirements and independent exchange evaluation |

There is no committed launch date. Contract source verification and a public document do not satisfy the later readiness gates. Any mainnet supply, ticker, distribution or migration would require a separate published decision. Earlier reported token/presale contracts were never identified; deploying the present prototype does not prove absence of any historical obligations.

## 13. Evidence and limits

The engineering baseline for this paper is application commit `93d28b9`, with testnet source-verification records from 2 November 2026. Recorded local validation includes 216 broad PostgreSQL/workspace regression cases, 42 focused credit/workflow cases and 16 browser cases across combined runs. The browser set includes three real PostgreSQL/worker credit flows at desktop/mobile sizes plus 13 existing token-screen cases. Counts overlap and must not be added into a total of unique tests. Additional targeted locking, export and configuration checks are documented in the release evidence.

These are developer-run local tests. They do not establish independent audit approval, production uptime, broad user adoption, legal permission or market demand. The implementation repository is currently private; publication of this paper does not assert that all application source is publicly licensed. No third-party dataset or credential is included in the whitepaper publication.

### Public testnet contract references

- [Allocation bundle source](https://testnet.bscscan.com/address/0x795112e85b53242c211c1a61e985b924b1db1b3e#code)
- [DCDTEST token source](https://testnet.bscscan.com/address/0xdbb45cbdc94d078854a0a85315b3577adadb4d41#code)
- [Ecosystem vesting source](https://testnet.bscscan.com/address/0x15f75d79ec341ae528afa0fc9182628aa836e25a#code)
- [Treasury vesting source](https://testnet.bscscan.com/address/0x9ebbb8965bc5a2c3d9dc621a8e18138aaf0cabec#code)
- [Team vesting source](https://testnet.bscscan.com/address/0x2591c82c4bc9a5ce342439e63a5b37acc26ca9f0#code)
- [Deployment transaction](https://testnet.bscscan.com/tx/0x8d3160b30322499ad59bf784995e6525c249356d5d6bf0a72205927607015af3)

Explorer source verification records compiler correspondence; it is not an independent assessment of vulnerabilities. Public addresses here identify BSC Testnet contracts only.

## 14. Risks, open decisions and document control

Demand may not justify a transferable token. Token rewards can attract fabricated usage; volatile token value may fail to fund promised services; quotes and indexing can fail; contracts and centralized systems can contain vulnerabilities. Licensing or source availability can change, and publication review does not eliminate those risks. A single-controller treasury concentrates operational risk.

No legal issuer, offering jurisdiction or production token rights are designated by this paper. Necessary entity, regulatory, tax, consumer, data-rights and security review remains outstanding before any real offer or redemption service. No DAO, DeFi or foreign-entity label is treated as a substitute for that work. No exchange relationship, listing, return or liquidity is promised.

Version 0.1 is a public discussion draft, not a purchase agreement or service-credit entitlement. Updates should preserve earlier versions and state material changes to rights, supply, control, economics or implementation status. Comments should distinguish verified implementation facts from proposals and unresolved decisions.

The next project task is C-005: measure the cost and usefulness of the existing service workflow before specifying a DCDTEST redemption rate or building the token-to-credit bridge.
