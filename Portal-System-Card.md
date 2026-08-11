# Dockware Portal

## Description: <br>
Dockware Portal is an outdoor fixed multi-camera AI system that records truck and rail passages, assembles multi-view imagery into continuous visual records, and applies computer vision to identify equipment (such as container IDs and license plates), check seal presence, detect hazard placards and visible damage, and related transit inspection attributes—producing searchable passage records and evidence imagery. <br>
Company site: [https://www.dockware.ai/](https://www.dockware.ai/) <br>

This system is ready for commercial use. <br>

## Third-Party Community Consideration <br>
Not applicable. This system is owned and developed by Dockware, Inc. Edge video analytics are accelerated with NVIDIA software and GPUs; perception models are developed by Dockware.

### License/Terms of Use: <br>
Proprietary software licensed by Dockware, Inc. under commercial customer agreements. Third-party runtime components remain under their respective licenses. Contact Dockware for licensing terms: [https://www.dockware.ai/](https://www.dockware.ai/)

### Deployment Geography: <br>
North America (NAM); expandable to Global under customer contract. <br>

### Release Management: <br>
Deployed as a managed on-premises appliance/software stack with NVIDIA GPU acceleration, plus Dockware-operated cloud processing for passage analytics. Updates are delivered through Dockware’s release process to installed sites (not as a public self-serve download). <br>

## Automation Level: <br>
* Autonomous <br>

Portal continuously monitors fixed cameras, records passages when activity is detected, builds multi-view visual records, and extracts inspection attributes without an operator per vehicle. Humans configure sites, review exceptions, and act on results in terminal workflows.

## Use Case: <br>
Intermodal terminals, yards, carriers, and logistics inspection teams use Portal to automatically capture and analyze truck and rail equipment as they pass fixed camera arrays—creating visual records and structured attributes (IDs, plates, seals, placards, damage, equipment type) for audit, claims, yard inventory, and compliance workflows. <br>

## Known Technical Limitations: <br>
* Outdoor performance varies with weather, night illumination, motion blur, and occlusion. <br>
* Multi-view assembly quality depends on installation calibration, passage speed, and scene texture. <br>
* Identifier reads (e.g., container codes, plates) degrade with dirt, damage, non-standard markings, or extreme viewing angles. <br>
* Seal, placard, and damage detection may miss subtle defects or flag benign visual patterns as false positives. <br>
* Camera network reliability and on-prem GPU capacity planning affect concurrent coverage. <br>
* Some attribute extraction paths may depend on cloud model services and inherit their latency/availability. <br>

## Known Risks: <br>
* Incorrect equipment ID or plate reads could mis-associate a passage with the wrong asset. <br>
* Missed seal absence, hazard placard, or damage signals could create false assurance if used as the sole compliance control. <br>
* False positives could trigger unnecessary stops, inspections, or claims friction. <br>
* Continuous outdoor video may include drivers, pedestrians, and plates; customers must apply appropriate privacy, retention, and access controls. <br>
* Compromise of site compute or cloud credentials could expose video archives and camera networks. <br>

## Fail Safe In-Place: <br>
* Human-in-the-Loop — exception review in operations workflows; models provide evidence, not sole legal determinations <br>
* Policy Enforcement — activity thresholds, confidence filters, camera enable/disable, retention and access policies <br>
* Shut-Down — stop on-prem services and/or pause cloud passage processing <br>
* Emergency Override — site can power down cameras or isolate the Portal host from the camera network <br>

### Release Date: <br>
08/11/2026 <br>

## Reference(s): <br>
* Dockware product site: [https://www.dockware.ai/](https://www.dockware.ai/) <br>
* Edge video path accelerated with NVIDIA GPUs / NVIDIA video analytics software <br>
* Transit perception models developed and evaluated on NVIDIA GPUs within Dockware’s ML development process <br>

## System Architecture: <br>
**Architecture Diagram:** <br>

```
Fixed outdoor camera array
        ↓
On-prem NVIDIA-accelerated ingest & recording
  ├─ Activity-based clip capture
  ├─ Optional on-edge detections
  └─ Secure media upload
        ↓
Dockware cloud analytics
  ├─ Multi-view visual record assembly
  ├─ Identity & inspection attribute extraction
  └─ Passage records + evidence for operations
```

Internal service topology, model inventory, and site BOMs are available under NDA. <br>

# System Input and Output <br>
## Input: <br>
**Input Type(s):** Image, Video <br>
**Input Format(s):** RGB camera streams and recorded passage clips <br>
**Input Parameters:** 2D (frames / assembled views); temporal video sequences <br>
**Other Properties Related to Input:** Multi-camera fixed install with site calibration across viewing angles (sides, front/rear, undercarriage as configured). Pre-processing includes activity gating and geometric multi-view assembly. <br>

## Output: <br>
**Output Type(s):** Image (assembled views, evidence frames), Video (passage clips), Structured attributes, Text (IDs, classifications) <br>
**Output Format:** Passage records with media references; detection/evidence overlays as configured; structured fields for equipment identity and inspection attributes (container ID, license plate, seal presence, hazard placards, damage, equipment category, etc.) <br>
**Output Parameters:** 1D (fields), 2D (images / localized evidence) <br>
**Other Properties Related to Output:** Cloud object storage and database records provide traceability for audit and claims. <br>

**Supported Hardware Microarchitecture Compatibility:** <br>
NVIDIA edge GPUs for on-prem accelerated video ingest; NVIDIA cloud GPUs for model development and cloud inference. <br>

## Fail Operation: <br>
**Functional Restrictions (e.g., Guardrails):** Activity thresholds before record; confidence filtering; processing timeouts; workflow pause controls. <br>
**Operational Restrictions (e.g., Use case restrictions):** Intended for logistics yard / gate / rail passage inspection on authorized private sites—not a substitute for certified scale measurement, not a sole legal determination of hazmat compliance, and not a law-enforcement product without appropriate customer controls and jurisdiction review. <br>

** Data Ingestion Source:** Real-time camera ingest with near-real-time cloud analytics after each passage. <br>
** Data Ingestion Preparation Techniques:** Activity-based recording; frame sampling; calibrated multi-view assembly; perception preprocessing for identity and inspection attributes. <br>

**Number of GPUs:** Edge NVIDIA GPU(s) on each Portal host sized to camera count; NVIDIA cloud GPUs for model development and cloud inference (sized to deployment).

## Supported Hardware Microarchitecture: <br>
NVIDIA edge GPU platform for accelerated video analytics; NVIDIA cloud GPUs for model development and cloud inference; multi-camera IP network; x86_64 Linux server. <br>

## Preferred/Supported Operating System: <br>
Linux (on-prem appliance/software stack); Linux cloud workers. <br>

## Hardware Specific Requirements:** <br>
NVIDIA GPU capacity matched to concurrent cameras; stable outdoor mounts and networking; site calibration; disk buffering for clips; outbound cloud connectivity. Detailed BOM available under NDA / customer SOW. <br>

## System Version(s): <br>
Dockware Portal — release channel identified by Dockware release tag. <br>

*Additional content may be included here.* <br>

**Logging and Traceability:** <br>
On-prem operational logs; cloud media keys and passage records. Access via site and cloud identity controls. Video may include plates and persons—retain per customer policy. <br>

**Vector Database Name:** Not used for core Portal passage storage. <br>
**Vector Database Type:** N/A <br>

## Ethical Considerations: <br>
Dockware, Inc. believes Trustworthy AI is a shared responsibility and we have established policies and practices to enable development for a wide array of AI applications. Developers and customers should work with their internal teams to ensure this system meets requirements for the relevant industry and use case and addresses unforeseen product misuse—especially continuous outdoor video, license-plate data, and workplace imagery. <br>

Please report quality, risk, security vulnerabilities or AI concerns via [https://www.dockware.ai/](https://www.dockware.ai/) (Contact / Demo). <br>

This template was created by NVIDIA.

Please use this template provided in the repo as you see fit per the Creative Commons Zero (CCO) License, adopting as you see fit. If you have recommendations or questions, please file an issue. Stay tuned for regular updates to these templates from our team.