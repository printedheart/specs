#####Use Case ID: UC-SCE01
#####Use Case Name: Create Lab Report

**Level:**                     User Level Goal

**Primary Actors:**            Content Creator (Physician/ Clinician, Nurse Practioner, Pathologist) 

**Stakeholders:**              Patient, Provider

**Purpose:**                   The main intent of this use case is the creation of laboratory report.

**Pre Condition:**             Content Creator must be identified and authenticated.  

**Post Condition:**            Laboratory Report is created successfully without any conflicts.

**Frequency of Occurrence:**   High

**Priority:**                  High
__________________________________________________________
**Main Success Scenario: (Create Lab Report)**

1.	Content Creator selects a particular test order from the list of orders.
2.	System shows the contents (lab results report(s)) included in the order.
3.	Content creator selects the one or more lab result reports to create final lab report
4.	System displays the selected lab result reports and provides the user with document sharing methodology options. 
  a.	FHIR Document
  b.	FHIR DocumentReference (CDA, Pdf, FHIR Document)

**Alternate Flows** 

**Alt-1: Create FHIR Document**

1.	FHIR Document Manager (FDM) Initiate new document creation.
2.	FHIR Document Composer (FDC) creates bundle resource with assigning FHIR Document resource as root.
3.	FDC load FHIR documents specs (e.g. xsd) and map all given data elements mentioned in specs. Such as;
  i.	document identifier
 ii.	doc version
 iii.	doc creation time
 iv.	doc author
 v.	...

4.	FDC map the attester information such as time of attestation and mode of attestation.
5.	FDC may add the event information for which the document was initiated. 
6.	Finally, it maps sections of the document according to requirement of profile for particular business case.
7.	FDM generate appropriate instance of document based on FDC structure and proceed for sending via REST end point.


**Alt-2: Create FHIR DocumentReference**

1.	FHIR Reference Document Manager (FRDM) Initiate new reference document creation i.e. CDA/Pdf/FHIR Document.
2.	FHIR Reference Document Composer (FRDC) creates bundle resource with assigning FHIR Reference Document resource as root.
3.	FRDC load FHIR reference documents specs (e.g. xsd) and map all given data elements mentioned in specs. Such as;
 i.	Ref document identifier
 ii.	Ref doc version
 iii.	Ref doc location
 iv.	Ref doc author
 v.	Ref doc custodian

4.  FRDC may add service type and address with parameters.
5.	FRDC may add the contextual information such as period and facility type. 

**Open Issues**

1. Change in requirement from FHIR perspective is an issue

**FHIR Information and Exchange, XDS Profile**

FHIR Resources: DocumentReference, Patient, Practioner, Organization
XDS Profile: Sharing Laboratory Reports (XD-LAB)

_______________________________________________________________

**Reference Models:**

1. **Reference HL7 RMIM (CDA): Level-1**

![11](https://f.cloud.github.com/assets/5012182/1418557/45d9ef3c-3fb8-11e3-9438-f22327ec5528.png)

2. **Reference HL7 RMIM (CDA): Level-2**

![12](https://f.cloud.github.com/assets/5012182/1418580/d57ed8a0-3fb8-11e3-9af7-6bdbf9cca628.png)

3	**Reference HL7 RMIM (CDA): Level-3**

![13](https://f.cloud.github.com/assets/5012182/1418589/08c70bb0-3fb9-11e3-94d0-3fbca7476b29.png)

_______________________________________________________________

**FHIR Reference Model: Document Resources**

![14](https://f.cloud.github.com/assets/5012182/1418603/7a054fda-3fb9-11e3-9b91-a0b37faf616e.PNG)

_______________________________________________________________

**Reference CDA Template:**

**Content Modules for CDA Header (Level 1)**

* Document-Level Templates **"Participants and Header Relationships(recordTarget)"**
* Document-Level Templates **"Participants and Header Relationships(intendedRecipient)"** 
* Document-Level Templates **"Participants and Header Relationships(participant)"** 
* Document-Level Templates **"Participants and Header Relationships(performer)"** 

_______________________________________________________________

**Content Modules for CDA Sections (Level 2)**

* Section-Level Templates **"Laboratory Speciality Section template"**
* Section-Level Templates **"Laboratory Report Item Section template "** 

_______________________________________________________________

**Content Modules for CDA Entries  (Level 3)**

* Entry-Level Templates **"Laboratory Data Processing Entry template "**
* Entry-Level Templates **"Specimen Collection template "** 
* Entry-Level Templates **"Specimen Received template  "**
* Entry-Level Templates **"Notification Organizer template"** 
* Entry-Level Templates **"Notifiable Condition template  "** 
* Entry-Level Templates **"Case Identifier template"**
* Entry-Level Templates **"Outbreak Identifier template "** 
* Entry-Level Templates **"Laboratory Isolate Organizer template"** 
* Entry-Level Templates **"Laboratory Battery Organizer template"** 
* Entry-Level Templates **"Laboratory Observation template "**
* Entry-Level Templates **"Annotation Comment "** 

______________________________________________________________

**Reference OpenEHR Archetypes (Version 1.4):**

N/A
