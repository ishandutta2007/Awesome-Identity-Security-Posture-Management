# Awesome-Identity-Security-Posture-Management

# Top Identity Security Posture Management (ISPM) Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Identity Hygiene, Entitlement Analysis & Self-Hosted Posture Assessment*  
**Last updated: November 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Identity Security Posture Management (ISPM)**. These tools enable organizations to continuously assess the security posture of human, machine, and non-human identities—identifying excessive privileges, orphaned accounts, toxic permission combinations, and policy violations before attackers can exploit them.

**Examples** include CrowdStrike Falcon Next-Gen Identity Security, Spera Security, Authomize, Silverfort, Tenable Identity Exposure, Rezonate, Entro Security, Veza, ConductorOne, and Oort (the category leaders).

**Open-source emphasis**: ISPM is a domain where the **commercial market is consolidating rapidly** (Authomize acquired by Delinea, Spera by Okta, Ermetic by Tenable), but open-source tooling is **genuinely viable for cloud entitlement analysis and identity graph construction**. **PMapper** (Principal Mapper) is the standout for AWS privilege escalation detection—it builds a graph of IAM principals and trust policies, then answers "who can reach admin access and by what route" with the highest detection rate among common open-source options . **Cloudsplaining** parses AWS IAM policies to flag least-privilege violations with risk-prioritized HTML reports . **Cartography** consolidates infrastructure assets into a Neo4j graph spanning AWS, Azure, GCP, Okta, GitHub, and Kubernetes—enabling cross-boundary questions no scanner anticipates . The critical caveat: **no open-source project matches the cross-IdP, cross-SaaS identity posture visibility** of dedicated ISPM platforms like Rezonate or Spera—those connect to multiple identity providers and SaaS applications to provide unified posture scoring .

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[CrowdStrike Falcon Next-Gen Identity Security](https://www.crowdstrike.com/)**  
  Unified identity protection combining ISPM, ITDR, and identity-based attack path analysis; covers AD, Entra ID, Okta, and 150+ SaaS applications with AI-powered behavioral detection.

- **[Spera Security](https://www.spera.io/)**  
  Identity security posture management platform; **acquired by Okta** (December 2023) for identity-driven breach prevention and posture assessment across cloud and SaaS.

- **[Authomize](https://www.authomize.com/)**  
  Identity security platform providing cross-environment visibility into identity posture and entitlements; **acquired by Delinea**, with its Open-ITDR framework remaining open-source.

- **[Silverfort](https://www.silverfort.com/)**  
  Identity security platform with **Runtime Access Protection** for inline posture enforcement; provides identity inventory, authentication firewall, and risk-based policy enforcement across AD and cloud IdPs.

- **[Tenable Identity Exposure](https://www.tenable.com/)**  
  AD security monitoring and identity posture assessment; **CAUTION**: CVE-2026-106126 (critical RCE) reported October 2026—verify patch status before deployment.

- **[Rezonate](https://www.rezonate.io/)**  
  Identity security posture management focused on **cloud identity and access risks**; provides visibility into entitlements, privilege escalation paths, and identity misconfigurations across cloud infrastructure.

- **[Entro Security](https://www.entro.security/)**  
  Non-human identity security platform; focuses on service accounts, API keys, and machine identities—discovering, monitoring, and governing NHI posture.

- **[Veza](https://www.veza.com/)**  
  Identity and access security platform using a **canonical identity graph** to visualize who can access what; provides posture assessment, entitlement analysis, and access governance across cloud and on-premises systems.

- **[ConductorOne](https://www.conductorone.com/)**  
  Identity security and governance platform with automated access reviews, entitlement management, and posture visibility across SaaS and cloud applications.

- **[Oort](https://www.oort.io/)**  
  Identity security platform focused on **identity threat detection and posture management**; provides visibility into identity risks across cloud IdPs and SaaS applications.

## Open-Source GitHub Projects

### Cloud Entitlement & Privilege Escalation Analysis

- **[PMapper (Principal Mapper)](https://github.com/nccgroup/PMapper)**  
  The **leading open-source tool for AWS privilege escalation analysis** (AGPL-3.0) . Builds a graph of IAM principals and the edges between them—analyzing trust policies, resource-based policies, and the specific API calls that enable escalation. Answers queries like "which principals can reach administrative access and by what route." **Comparative testing shows the highest privilege escalation detection rate** among common open-source options. **Best for security teams** wanting to find actual escalation paths rather than just flagging risky-looking policies—but it is command-line and query-oriented with no polished report .

- **[Cloudsplaining](https://github.com/salesforce/cloudsplaining)**  
  Open-source **AWS IAM policy analyzer** (Apache-2.0) from Salesforce . Parses IAM policies to identify **least-privilege violations**—flagging resource exposure, privilege escalation potential, credential exposure, and data exfiltration capability. Produces a **risk-prioritized HTML report** designed to be shared as a work queue. Supports offline analysis of downloaded policy documents and an exclusions file for accepted risks. **Best for teams wanting readable, prioritized findings**—but it is AWS-only and policy-level analysis (does not resolve full effective permissions across role chains) .

- **[policy_sentry](https://github.com/salesforce/policy_sentry)**  
  Open-source **least-privilege IAM policy generator** (MIT) . Inverts the usual workflow: you declare the resources and access levels a workload needs, and it generates a least-privilege IAM policy with correct actions and resource ARNs. Exists because writing least-privilege policies by hand is tedious enough that engineers reach for wildcards. **Best for preventing over-privilege at the source**—but it is generation, not enforcement; nothing stops someone editing the result .

### Identity Graph & Cross-Boundary Analysis

- **[Cartography](https://github.com/lyft/cartography)**  
  Open-source **infrastructure asset and relationship graph** (Apache-2.0) from Lyft . Consolidates infrastructure assets and their relationships into a **Neo4j graph**, spanning AWS, Azure, GCP, Okta, GitHub, Kubernetes, and more. You write Cypher queries to answer questions no scanner anticipated—e.g., which cloud roles are reachable from a GitHub repository through a CI integration. **Best for cross-domain blast-radius investigation and custom posture queries**—but you operate Neo4j, write your own queries, and there is no out-of-the-box prioritization .

- **[ScoutSuite](https://github.com/nccgroup/ScoutSuite)**  
  Open-source **multi-cloud security auditing tool** (GPL-2.0) from NCC Group . Collects configuration data across AWS, Azure, GCP, Alibaba Cloud, and Oracle Cloud, producing a browsable offline HTML report including a substantial IAM section. **Best for assessment engagements** where you want a comprehensive multi-cloud posture snapshot—but it is auditor-oriented rather than pipeline-integrated, and the IAM analysis is configuration-level rather than privilege-escalation-path analysis .

### Additional Strong Open-Source Options

- **[Bastion](https://github.com/nirjxr26/Bastion)** — Self-hosted IAM platform with dynamic RBAC, policy simulator, ML-based login risk scoring, and full audit visibility (MIT-style) . **Best for teams wanting a self-hosted IAM foundation with posture visibility**—but it is an IAM platform rather than a dedicated ISPM tool, and it is newer with a smaller community.
- **[Hanzo IAM](https://github.com/hanzoai/iam)** — Open-source AI-first IAM with OAuth 2.0, OIDC, SAML, SCIM, WebAuthn, RBAC, and multi-tenancy (Apache-2.0) . **Best for organizations wanting a full IAM platform** with posture-relevant features like SCIM provisioning and RBAC—but it is identity infrastructure, not a posture scanner.
- **[WSO2 Identity Server](https://github.com/wso2/product-is)** — Enterprise-grade open-source IAM (Apache-2.0) recognized as a Digital Public Good; supports OAuth2, OIDC, SAML, SCIM 2.0, FIDO2, adaptive MFA, and RBAC . **Best for organizations wanting a mature IAM foundation**—but it is not a dedicated ISPM tool for entitlement analysis.

**Frameworks for building custom systems**: For **AWS privilege escalation analysis**, PMapper is the mature open-source leader . For **least-privilege policy auditing and generation**, Cloudsplaining and policy_sentry . For **cross-domain identity and infrastructure graphs**, Cartography . For **multi-cloud configuration posture**, ScoutSuite . **No open-source project matches the cross-IdP, cross-SaaS posture visibility** of Rezonate, Spera, or Veza—those are commercial platforms that connect to multiple identity providers and SaaS applications for unified scoring . Choose based on whether you need cloud entitlement analysis (PMapper, Cloudsplaining), identity graphs (Cartography), or a self-hosted IAM foundation (Bastion, WSO2).

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- ISPM platforms handling identity and entitlement data must comply with organizational security policies and privacy regulations; **self-hosted solutions place full responsibility for graph accuracy, query maintenance, and data freshness on the operator**.
- **Open-source ISPM is capable at the cloud entitlement and graph layers but fundamentally limited for cross-IdP posture**—PMapper and Cloudsplaining provide production-grade AWS analysis , and Cartography provides cross-domain graphs . However, **no open-source project matches the cross-IdP, cross-SaaS identity posture visibility** of dedicated commercial ISPM platforms . **Tenable Identity Exposure has a known critical CVE** (October 2026) . Choose based on whether you need AWS entitlement analysis (PMapper), policy generation (policy_sentry), or identity graphs (Cartography).
- Verify license terms for commercial use; PMapper uses AGPL-3.0 , Cloudsplaining uses Apache-2.0 , policy_sentry uses MIT , Cartography uses Apache-2.0 , and ScoutSuite uses GPL-2.0 .

---

**Made for identity security architects, cloud security engineers, and organizations assessing identity posture.**  
Let's make identity security posture management more open at the cloud entitlement and graph layers, but with clear eyes about the cross-IdP visibility gaps that commercial platforms still fill.
