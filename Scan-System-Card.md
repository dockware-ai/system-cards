# Dockware Scan

## Description: <br>
Dockware Scan is a handheld mobile application (Android and iOS) that uses on-device camera and depth sensing plus cloud perception to capture shipment dimensions, identifiers, condition signals, and logistics documents (such as Bills of Lading and pick tickets)—producing a verifiable digital twin / fingerprint of each shipment that can be re-scanned later to detect deltas. <br>
Product overview: [https://www.dockware.ai/](https://www.dockware.ai/) <br>

This system is ready for commercial use. <br>

## Third-Party Community Consideration <br>
Not applicable. This system is owned and developed by Dockware, Inc. Mobile SDKs may be offered to partners under Dockware commercial terms.

### License/Terms of Use: <br>
Proprietary software licensed by Dockware, Inc. under commercial customer agreements and applicable mobile app store terms. See [https://www.dockware.ai/](https://www.dockware.ai/) for product and contact information.

### Deployment Geography: <br>
North America (NAM); expandable to Global via app distribution and customer tenants. <br>

### Release Management: <br>
Distributed as native mobile apps (public app stores and/or enterprise distribution) with Dockware-managed cloud processing. Feature updates ship through standard mobile and backend release channels. <br>

## Automation Level: <br>
* Partial Automation <br>

A human operator aims the device and initiates capture; Scan automates sensing, document parsing, dimensioning, identifier extraction, and digital-twin creation. Operators remain in control of when/what is scanned and of business decisions using the results.

## Use Case: <br>
Dock workers, drivers, shippers, receivers, and remote operators use Scan to capture freight data anywhere a smartphone can go—dimensioning handling units, reading identifiers, parsing BOL / pick-ticket documents, and recording condition—then syncing a shipment digital twin to Dockware or customer systems. Downstream parties can re-scan to validate against the original fingerprint and flag discrepancies. <br>

## Known Technical Limitations: <br>
* Dimensioning quality depends on device depth capability, scan coverage, lighting, and surface properties; transparent wrap, dark absorptive materials, or incomplete orbits reduce accuracy. <br>
* Document parsing accuracy varies with image quality, form layouts, handwriting, languages, and damage/folding of paper. <br>
* On-device capture quality varies across ARCore Android devices; iOS requires Pro-series hardware. <br>
* Final results depend on network upload to NVIDIA cloud GPU inference; offline capture may defer completed dimensions until sync. <br>
* Cross-scan delta matching assumes sufficient overlapping identifiers and geometry; unlabeled or heavily rewrapped freight may require human association. <br>

## Known Risks: <br>
* Incorrect dimensions or parsed document fields could propagate into billing, routing, or inventory systems if accepted without validation policies. <br>
* Mis-associated shipment fingerprints could cause false delta alerts or missed claims evidence. <br>
* Photos and 3D captures may include workplace bystanders or facility backgrounds; customer retention and access policies must govern workplace imagery. <br>
* Device loss/theft could expose locally cached scan artifacts if device encryption and app authentication are not enforced. <br>
* Spoofed or low-quality identifiers/documents could mislead automated fields without secondary checks. <br>

## Fail Safe In-Place: <br>
* Human-in-the-Loop — operator initiates scans; can discard captures; business systems can require review before billing/claims use <br>
* Policy Enforcement — organization authentication; status/confidence flags on results; cloud retention policies <br>
* Shut-Down — disable app features / revoke credentials / withdraw store releases <br>
* Emergency Override — N/A for physical actuators (handheld software); operator stops scanning <br>

### Release Date: <br>
06/21/2025 <br>

## Reference(s): <br>
* Dockware product site: [https://www.dockware.ai/](https://www.dockware.ai/) <br>
* Perception and document models are developed and evaluated on NVIDIA GPUs within Dockware’s ML development process <br>

## System Architecture: <br>
**Architecture Diagram:** <br>

```
Mobile device (iOS / Android)
  ├─ Camera + on-device depth / spatial sensing
  ├─ Optional on-device guidance during capture
  ├─ Document capture (BOL / pick ticket / general)
  └─ Secure upload of scan and document media
        ↓
Dockware cloud processing
  ├─ 3D reconstruction / dimensioning
  ├─ Identifier and condition extraction
  ├─ Document field extraction
  └─ Shipment digital twin + delta comparison
        ↓
Customer applications / integrations
```

Internal service topology is available under NDA. <br>

# System Input and Output <br>
## Input: <br>
**Input Type(s):** Image, Depth / 3D sensing, Text (user metadata), Document imagery <br>
**Input Format(s):** RGB camera frames; device depth / spatial captures; document photos <br>
**Input Parameters:** 2D (images), 3D (geometry / poses) <br>
**Other Properties Related to Input:** Consumer smartphone cameras and depth/spatial sensors; document images suitable for field extraction. Pre-processing includes capture guidance, document normalization, and cloud-side geometric cleanup. <br>

## Output: <br>
**Output Type(s):** Structured shipment records, Text (parsed fields, identifiers), Image (evidence), geometry summaries <br>
**Output Format:** Shipment digital twin including dimensions, identifiers, document fields (e.g., BOL / PRO / pick-ticket references, addresses), timestamps/location as configured, and links to evidence media <br>
**Output Parameters:** 1D (fields, scalars), 2D (images), 3D (dimensions / geometry) <br>
**Other Properties Related to Output:** Status and confidence/error signals; organization-scoped artifact storage; APIs to associate new scans with prior fingerprints for delta checks. <br>

**Supported Hardware Microarchitecture Compatibility:** <br>
Apple iPhone Pro-series (required for iOS); Android devices with ARCore compatibility. Perception and dimensioning inference run on NVIDIA cloud GPUs. <br>

## Fail Operation: <br>
**Functional Restrictions (e.g., Guardrails):** Authenticated tenant access; scan status states; confidence gates; discard/retry for failed captures. <br>
**Operational Restrictions (e.g., Use case restrictions):** Intended for logistics shipment and document capture by authorized workforce users—not for biometric identification, not a certified legal metrology device unless separately certified, and not a substitute for hazmat regulatory determinations without qualified human review. <br>

** Data Ingestion Source:** Near-real-time mobile capture with cloud processing on upload. <br>
** Data Ingestion Preparation Techniques:** Guided multi-view capture; document normalization; geometric filtering and alignment; identity/document field extraction. <br>

**Number of GPUs:** None on-device. NVIDIA cloud GPUs for model development and all Scan cloud inference (sized to load).

## Supported Hardware Microarchitecture: <br>
iPhone Pro-series; ARCore-compatible Android devices; NVIDIA cloud GPUs for inference and model development. <br>

## Preferred/Supported Operating System: <br>
iOS (Pro-series devices) and Android (ARCore-compatible devices); cloud services on Linux. <br>

## Hardware Specific Requirements:** <br>
**iOS:** iPhone Pro-series required. **Android:** any ARCore-compatible device. Functioning rear camera and depth/spatial sensing for full dimensioning; adequate local storage for temporary buffers; network connectivity for sync. <br>

## System Version(s): <br>
Dockware Scan — mobile app version + cloud processing version as published in release notes. <br>

*Additional content may be included here.* <br>

**Logging and Traceability:** <br>
Organization-scoped shipment scans, document results, and evidence references in Dockware cloud systems; mobile telemetry per privacy policy. <br>

**Vector Database Name:** Not used for core Scan twin storage. <br>
**Vector Database Type:** N/A <br>

## Ethical Considerations: <br>
Dockware, Inc. believes Trustworthy AI is a shared responsibility and we have established policies and practices to enable development for a wide array of AI applications. Developers and customers should work with their internal teams to ensure this system meets requirements for the relevant industry and use case and addresses unforeseen product misuse. <br>

Please report quality, risk, security vulnerabilities or AI concerns via [https://www.dockware.ai/](https://www.dockware.ai/) (Contact / Demo). <br>

This template was created by NVIDIA.

Please use this template provided in the repo as you see fit per the Creative Commons Zero (CCO) License, adopting as you see fit. If you have recommendations or questions, please file an issue. Stay tuned for regular updates to these templates from our team.