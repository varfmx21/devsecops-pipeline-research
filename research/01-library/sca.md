# SCA
## What is 
Software composition analysis (SCA) process of analyzing software—most commonly software built from open-source components—to ensure that the components are up-to-date, secure and in license compliance.
### Tools
Snyk Open Source - Commercial (free tier) - MOderate high - SAST (Snyk Code), Containers, IaC, Secrets, DAST - Large enterprises needing deep IDE integration and strict RBAC governance
Trivy - 100% Open Source (Apache 2.0, completely free) - High (flags every CVE in manifest/image regardless of usage) - Containers, IaC, Kubernetes, Secrets, Licenses, SBOMs - DevOps engineers wanting a fast, free, air-gapped, or scriptable CI scanner
Aikido Security - Commercial (generous free tier; predictable flat-rate tiers) - Very Low (auto-triage suppresses ~80–90% of unexploitable alerts) - SAST, Containers, IaC, Secrets, Cloud (CSPM), DAST, Malware - Lean DevSecOps teams wanting consolidated AppSec + minimal alert fatigue
### ANother sca + sbom
theres other practice to use sbom generation and scan this with some tool sca to found vulenrabilities
Syft - this is a tool to generate a sbom 
grype - this can use to scan sboms
### comparition table sca directly and sca + sbom
                    sca directly             |           sca + sbom
industry adoption | most common | standard in big enterprise with madurity
cicd simplicity | easy | medium
new cve's  | re scan the pipeline | instantily usign the sbom to scan
uditory | doesnt leave with standard evidence | oficial inventory artifact ready for clients and audits
link: https://appsecsanta.com/sca-tools/syft-vs-trivy