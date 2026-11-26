# devsecops-pipeline-research
DevSecOps pipeline including SAST, DAST, SCA with an app to find vulnerabilities and LLM remediation. For the project In-Depth research in Fontys semester "AV-CSP: Advanced Cyber Security" 

main reserch question:
"How can an LLM-based remediation stage be designed, justified, and evaluated within a SAST/DAST/SCA CI/CD pipeline, and which level of autonomy can it safely support?"

Sub quesstions:
"SQ1 Library: Which report formats, context, and documentation does an LLM need to correctly interpret SAST, DAST, and SCA findings?
Goal: a specification of input formats and context enrichment for the agent.
SQ2 Field: What practices, guardrails, and trust boundaries do practitioners report for AI-generated security fixes?
Goal: practitioner-derived requirements that justify the architecture's autonomy levels and controls.
SQ3 Workshop: What architecture connects scanners, the LLM agent, and the repository, and why is each design choice justified?
Goal: a working, documented proof-of-concept pipeline with justified trade-offs.
SQ4 Lab: How effective and safe is the remediation stage at each autonomy level, measured by fix rate, functional integrity, and security delta?
Goal: quantitative evidence for which autonomy level the architecture can support.
"

autonomy level used in this:
level - what does the agent - human control
L0. No autonomy (Advisory) -  AI system provides information, analysis, or recommendations. - the human writes an apply the fix
L1. Assited PR - AI can execute code fixes and open a PR in github - the human review it and make changes if it necesarilly and merge
L2. COnditional Merge - AI code fixes and make merge only if all the tests passed, re-scan and umbral - human inly if theres some fail or low confidence
L3. Without doors and guardrails - make code fixes, merge and deploy - human only monitoring after.
[table 1]

app:
https://github.com/plexicus/simplest-sast-vulnerable