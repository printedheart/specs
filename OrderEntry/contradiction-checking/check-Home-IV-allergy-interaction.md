#####Use Case ID: UC-OES19
#####Use Case Name: Check Home IV-Allergy Interaction

**Level:**                     User Level Goal

**Primary Actors:**            Doctor/ Physician/ Clinician 

**Stakeholders:**              Order Entry User

**Purpose:**                   The main intent of this use case is to perform drug-allergy interaction checking during non-medication order process.

**Pre Condition:**             Doctor/ Physician/ Clinician must be identified and authenticated.  

**Post Condition:**            There is no drug-allergy interaction.

**Frequency of Occurrence:**   High

**Priority:**                  High
__________________________________________________________
**Main Success Scenario: (Check Home IV-Allergy Interaction)**

1.	Physician selects the new medication order option and selects MRNO (or any other identification criteria) from the list.
2.	System shows the relevant data including weight of the patient, allergies and history.
3.	Physician after observing the status of patient fill in prescription for home IV.
4.	Physician specifies the dosage of the home IV.
5.	System will check for invalid and missing information.
6.	System checks if the prescribed medications have some drug-allergy interactions among them.
7.	System responds with no interaction.
8.	Physicians will save the order.
9.	System will perform following actions.
    * It will record the time stamp of the ordered medication.
    * It will set the medication status to active.
    * It will send the prescription to pharmacy and will respond with non-medication order ID.
    
**Sub-Flow:**

1.	System responds with interaction among the patient allergies and the prescribed home IV.
2.	Physician will prescribe some alternative home IV.
3.	The step 3 in main scenario of events is then executed.

_______________________________________________________________
**Open Issues**

-NA-
_______________________________________________________________
**Reference Hl7 V3 Interaction Identifiers (Domain: Pharmacy):**

COCT_RM260003UV
_______________________________________________________________
**Reference CCHIT Criteria:**

FN 07.01

_______________________________________________________________
**Reference Hl7 RMIM (Domain: Pharmacy):** [More Details](http://www.hl7.org/implement/standards/product_brief.cfm?product_id=306)

![image](https://f.cloud.github.com/assets/4283040/1396587/6b5025ac-3c6a-11e3-9dde-be0c8aaf690c.png)

_______________________________________________________________
**Reference FHIR Resource:** [More Details](http://www.hl7.org/implement/standards/fhir/resourcelist.html)

![image](https://f.cloud.github.com/assets/4283040/1396598/c3fbb838-3c6a-11e3-8a50-5c0f711ab777.png)

_______________________________________________________________
**Reference CDA Template:** [More Details](http://www.hl7.org/Special/committees/structure/index.cfm)

-NA-
_______________________________________________________________
**Reference OpenEHR Archetypes (Version 1.4):** [More Details](http://www.openehr.org/ckm/)

Procedure (openEhr Archetype)
```Archetype
archetype (adl_version=1.4)
	openEHR-EHR-EVALUATION.adverse_reaction.v1
concept
	[at0000]	-- Adverse Reaction
language
	original_language = <[ISO_639-1::en]>
	translations = <
		["de"] = <
			language = <[ISO_639-1::de]>
			author = <
				["name"] = <"Jasmin Buck, Sebastian Garde">
				["organisation"] = <"University of Heidelberg, Central Queensland University">
			>
		>
		["ar-sy"] = <
			language = <[ISO_639-1::ar-sy]>
			author = <
				["name"] = <"Mona Saleh">
				["email"] = <"monasaleh01@live.com">
			>
		>
	>
description
	original_author = <
		["name"] = <"Heather Leslie">
		["organisation"] = <"Ocean Informatics">
		["email"] = <"heather.leslie@oceaninformatics.com">
		["date"] = <"2010-11-08">
	>
	details = <
		["ar-sy"] = <
			language = <[ISO_639-1::ar-sy]>
			purpose = <"*To record information about any harmful, desirable or unexpected reaction to a substance or agent, including:
- immune mediated reactions Types I-IV (including true allergic reactions and hypersensitivities), and 
- non-immune mediated reactions (including pseudoallergic reactions, side effects, intolerances, drug toxicities (eg Gentamicin), drug-drug interactions, food-drug interactions, drug-disease interactions and idiosyncratic reactions).

To record information about previous exposures to a substance, allowing a persisting and evolving summary of adverse reaction events to build up over time.

To record additional information that will support and inform a clinical assessment of the propensity of an individual to experience an adverse reaction if exposed to a specific substance, class of substance or agent in the future.(en)">
			use = <"*Use to record all information about the presence of adverse reaction/s (including an allergic reaction/s)  to a substance to support direct clinical care of an individual; as part of a managed Adverse Reaction list; to enable safe exchange of information about adverse reactions; and to assist computerised knowledge-based activities such as clinical decision support and alerts.

Use to provide a single place within the health record to record a range of clinical statements about adverse reactions, including:  
-  record cumulative information about each exposure to a known substance, class of substance or agent; and 
-  record a clinician's opinion that administration of, or exposure to, a substance or agent is absolutely contraindicated.

This archetype has been designed to allow recording of information about a more generic substance, class of substance or agent, and then allow more specific details to be recorded including identification of the specific substance on a per exposure basis, including links to other parts of the health record where further details may be located. Note:  it is possible on second or subsequent exposures to a previously identified substance for a reaction not to occur and this archetype allows for these events to be closely linked in a way that will assist in determining if the adverse reaction has been incorrectly identified.

Design of this archetype has been deliberatly focused on identifying a pragmatic, core data set that will be suitable for most common use clinical scenarios but permits extension of the model when additional detail is required through incorporation of additional archetypes in the 'Additional Reaction Detail', 'Additional Exposure Detail', and 'Reporting Details' slots. Examples of clinical situations where the extension will be required are for a detailed immunology assessment, for reporting to regulatory bodies or clinical trial use.

A data element for Substance Category has not been modelled as this should be able to be derived from any coded entry for Substance/Agent and be used in decision support activities. A coded Category is not adequate to support decision support if Substance/Agent is only entered via free text.

The act of recording an adverse reaction in the health record implies there is a potential hazard for the individual if they are exposed to the same substance/agent in the future - a relative contraindication. If a clinician considers that it is not safe for the individual to be deliberately re-exposed to the substance/agent again, for example, following a manifestation of anaphylaxis, the 'Absolute contraindication' data flag should be recorded as ‘True’. Note: Conversely, a statement about ‘Severity’ of propensity (with possible values such as Mild, Moderate and Severe) has deliberately not been modelled explicitly. Predicting or estimating the grade of possible severity of a future reaction is not safe to record and persist in data, except where it is absolutely clear that the risk of deliberate re-exposure is unacceptable and highly likely to cause significant harm, such as a previous manifestation of anaphylaxis, and in this case the ‘Absolute contraindication’ data flag should be used. 

Valuable first-level information that could be presented to the clinician when they need to assess propensity for future reactions are:
- statements about previous clinical manifestations following exposure,
- source of the information/reporter, and
- a flag for absolute contra-indication. 
Second-level information can be drawn from each exposure event and links to additional detailed information such as history, examination and diagnoses stored elsewhere in the record, if it is available.

A formal Adverse Reaction Report to regulatory bodies is a document that will contain a broad range of information in addition to the specific details of the adverse reaction. The report will be comprised of this Adverse Reaction archetype plus a variable number of others - for example, demographics, weight, medication and problem/diagnosis.(en)">
			keywords = <"*reaction(en)", "*allergy(en)", "*allergic(en)", "*adverse(en)", "*event(en)", "*effect(en)", "*sensitivity(en)", "*intolerance(en)", "*hypersensitivity(en)", "*side effect(en)", "*toxicity(en)", "*interaction(en)", "*drug(en)", "*food(en)", "*medication(en)", "*agent(en)", "*substance(en)", "*immune(en)", "*non-immune(en)", "*chemical(en)">
			misuse = <"*Not to be used for recording the absence (or negative presence) of a reaction to 'any substances' or to identified substances – use the EVALUATION.exclusion family of archetypes to express a positive statement of Adverse Reaction exclusion. 

Not to be used for recording that no information was able to be obtained about the Adverse Reaction status of a patient. Use the EVALUATION.absent_information family of archetypes to record that a positive statement that information was not able to be obtained, for example, if a non-cooperative patient refuses to answer questions.

Not to be used to record adverse events, including failures of clinical process, interventions or products. For example: abnormal use or mistakes/errors made in administration of an agent or substance; mislabelling; harm or injury caused by an intervention or procedure; overdose etc.

Not to be used for recording alerts.

Not to be used for recording failed therapy.(en)">
			copyright = <"© openEHR Foundation">
		>
		["de"] = <
			language = <[ISO_639-1::de]>
			purpose = <"*To record information about any harmful, desirable or unexpected reaction to a substance or agent, including:
- immune mediated reactions Types I-IV (including true allergic reactions and hypersensitivities), and 
- non-immune mediated reactions (including pseudoallergic reactions, side effects, intolerances, drug toxicities (eg Gentamicin), drug-drug interactions, food-drug interactions, drug-disease interactions and idiosyncratic reactions).

To record information about previous exposures to a substance, allowing a persisting and evolving summary of adverse reaction events to build up over time.

To record additional information that will support and inform a clinical assessment of the propensity of an individual to experience an adverse reaction if exposed to a specific substance, class of substance or agent in the future.(en)">
			use = <"*Use to record all information about the presence of adverse reaction/s (including an allergic reaction/s)  to a substance to support direct clinical care of an individual; as part of a managed Adverse Reaction list; to enable safe exchange of information about adverse reactions; and to assist computerised knowledge-based activities such as clinical decision support and alerts.

Use to provide a single place within the health record to record a range of clinical statements about adverse reactions, including:  
-  record cumulative information about each exposure to a known substance, class of substance or agent; and 
-  record a clinician's opinion that administration of, or exposure to, a substance or agent is absolutely contraindicated.

This archetype has been designed to allow recording of information about a more generic substance, class of substance or agent, and then allow more specific details to be recorded including identification of the specific substance on a per exposure basis, including links to other parts of the health record where further details may be located. Note:  it is possible on second or subsequent exposures to a previously identified substance for a reaction not to occur and this archetype allows for these events to be closely linked in a way that will assist in determining if the adverse reaction has been incorrectly identified.

Design of this archetype has been deliberatly focused on identifying a pragmatic, core data set that will be suitable for most common use clinical scenarios but permits extension of the model when additional detail is required through incorporation of additional archetypes in the 'Additional Reaction Detail', 'Additional Exposure Detail', and 'Reporting Details' slots. Examples of clinical situations where the extension will be required are for a detailed immunology assessment, for reporting to regulatory bodies or clinical trial use.

A data element for Substance Category has not been modelled as this should be able to be derived from any coded entry for Substance/Agent and be used in decision support activities. A coded Category is not adequate to support decision support if Substance/Agent is only entered via free text.

The act of recording an adverse reaction in the health record implies there is a potential hazard for the individual if they are exposed to the same substance/agent in the future - a relative contraindication. If a clinician considers that it is not safe for the individual to be deliberately re-exposed to the substance/agent again, for example, following a manifestation of anaphylaxis, the 'Absolute contraindication' data flag should be recorded as ‘True’. Note: Conversely, a statement about ‘Severity’ of propensity (with possible values such as Mild, Moderate and Severe) has deliberately not been modelled explicitly. Predicting or estimating the grade of possible severity of a future reaction is not safe to record and persist in data, except where it is absolutely clear that the risk of deliberate re-exposure is unacceptable and highly likely to cause significant harm, such as a previous manifestation of anaphylaxis, and in this case the ‘Absolute contraindication’ data flag should be used. 

Valuable first-level information that could be presented to the clinician when they need to assess propensity for future reactions are:
- statements about previous clinical manifestations following exposure,
- source of the information/reporter, and
- a flag for absolute contra-indication. 
Second-level information can be drawn from each exposure event and links to additional detailed information such as history, examination and diagnoses stored elsewhere in the record, if it is available.
A formal Adverse Reaction Report to regulatory bodies is a document that will contain a broad range of information in addition to the specific details of the adverse reaction. The report will be comprised of this Adverse Reaction archetype plus a variable number of others - for example, demographics, weight, medication and problem/diagnosis.(en)">
			keywords = <"*reaction(en)", "*allergy(en)", "*allergic(en)", "*adverse(en)", "*event(en)", "*effect(en)", "*sensitivity(en)", "*intolerance(en)", "*hypersensitivity(en)", "*side effect(en)", "*toxicity(en)", "*interaction(en)", "*drug(en)", "*food(en)", "*medication(en)", "*agent(en)", "*substance(en)", "*immune(en)", "*non-immune(en)", "*chemical(en)">
			misuse = <"*Not to be used for recording the absence (or negative presence) of a reaction to 'any substances' or to identified substances – use the EVALUATION.exclusion family of archetypes to express a positive statement of Adverse Reaction exclusion.
Not to be used for recording that no information was able to be obtained about the Adverse Reaction status of a patient. Use the EVALUATION.absent_information family of archetypes to record that a positive statement that information was not able to be obtained, for example, if a non-cooperative patient refuses to answer questions.
Not to be used to record adverse events, including failures of clinical process, interventions or products. For example: abnormal use or mistakes/errors made in administration of an agent or substance; mislabelling; harm or injury caused by an intervention or procedure; overdose etc.
Not to be used for recording alerts.
Not to be used for recording failed therapy.(en)">
			copyright = <"© openEHR Foundation">
		>
		["en"] = <
			language = <[ISO_639-1::en]>
			purpose = <"To record information about any harmful, desirable or unexpected reaction to a substance or agent, including:
- immune mediated reactions Types I-IV (including true allergic reactions and hypersensitivities), and 
- non-immune mediated reactions (including pseudoallergic reactions, side effects, intolerances, drug toxicities (eg Gentamicin), drug-drug interactions, food-drug interactions, drug-disease interactions and idiosyncratic reactions).
To record information about previous exposures to a substance, allowing a persisting and evolving summary of adverse reaction events to build up over time.
To record additional information that will support and inform a clinical assessment of the propensity of an individual to experience an adverse reaction if exposed to a specific substance, class of substance or agent in the future.">
			use = <"Use to record all information about the presence of adverse reaction/s (including an allergic reaction/s)  to a substance to support direct clinical care of an individual; as part of a managed Adverse Reaction list; to enable safe exchange of information about adverse reactions; and to assist computerised knowledge-based activities such as clinical decision support and alerts.
Use to provide a single place within the health record to record a range of clinical statements about adverse reactions, including:  
-  record cumulative information about each exposure to a known substance, class of substance or agent; and 
-  record a clinician's opinion that administration of, or exposure to, a substance or agent is absolutely contraindicated.
This archetype has been designed to allow recording of information about a more generic substance, class of substance or agent, and then allow more specific details to be recorded including identification of the specific substance on a per exposure basis, including links to other parts of the health record where further details may be located. Note:  it is possible on second or subsequent exposures to a previously identified substance for a reaction not to occur and this archetype allows for these events to be closely linked in a way that will assist in determining if the adverse reaction has been incorrectly identified.
Design of this archetype has been deliberatly focused on identifying a pragmatic, core data set that will be suitable for most common use clinical scenarios but permits extension of the model when additional detail is required through incorporation of additional archetypes in the 'Additional Reaction Detail', 'Additional Exposure Detail', and 'Reporting Details' slots. Examples of clinical situations where the extension will be required are for a detailed immunology assessment, for reporting to regulatory bodies or clinical trial use.
A data element for Substance Category has not been modelled as this should be able to be derived from any coded entry for Substance/Agent and be used in decision support activities. A coded Category is not adequate to support decision support if Substance/Agent is only entered via free text.
The act of recording an adverse reaction in the health record implies there is a potential hazard for the individual if they are exposed to the same substance/agent in the future - a relative contraindication. If a clinician considers that it is not safe for the individual to be deliberately re-exposed to the substance/agent again, for example, following a manifestation of anaphylaxis, the 'Absolute contraindication' data flag should be recorded as ‘True’. Note: Conversely, a statement about ‘Severity’ of propensity (with possible values such as Mild, Moderate and Severe) has deliberately not been modelled explicitly. Predicting or estimating the grade of possible severity of a future reaction is not safe to record and persist in data, except where it is absolutely clear that the risk of deliberate re-exposure is unacceptable and highly likely to cause significant harm, such as a previous manifestation of anaphylaxis, and in this case the ‘Absolute contraindication’ data flag should be used. 
Valuable first-level information that could be presented to the clinician when they need to assess propensity for future reactions are:
- statements about previous clinical manifestations following exposure,
- source of the information/reporter, and
- a flag for absolute contra-indication. 
Second-level information can be drawn from each exposure event and links to additional detailed information such as history, examination and diagnoses stored elsewhere in the record, if it is available.
A formal Adverse Reaction Report to regulatory bodies is a document that will contain a broad range of information in addition to the specific details of the adverse reaction. The report will be comprised of this Adverse Reaction archetype plus a variable number of others - for example, demographics, weight, medication and problem/diagnosis.">
			keywords = <"reaction", "allergy", "allergic", "adverse", "event", "effect", "sensitivity", "intolerance", "hypersensitivity", "side effect", "toxicity", "interaction", "drug", "food", "medication", "agent", "substance", "immune", "non-immune", "chemical">
			misuse = <"Not to be used for recording the absence (or negative presence) of a reaction to 'any substances' or to identified substances – use the EVALUATION.exclusion family of archetypes to express a positive statement of Adverse Reaction exclusion.
Not to be used for recording that no information was able to be obtained about the Adverse Reaction status of a patient. Use the EVALUATION.absent_information family of archetypes to record that a positive statement that information was not able to be obtained, for example, if a non-cooperative patient refuses to answer questions.
Not to be used to record adverse events, including failures of clinical process, interventions or products. For example: abnormal use or mistakes/errors made in administration of an agent or substance; mislabelling; harm or injury caused by an intervention or procedure; overdose etc.
Not to be used for recording alerts.
Not to be used for recording failed therapy.">
			copyright = <"© openEHR Foundation">
		>
	>
	lifecycle_state = <"CommitteeDraft">
	other_contributors = <"John Bennett, NEHTA, Australia", "Sharmila Biswas, Dr Sharmila Biswas GP, Australia", "Rong Chen, Cambio Healthcare System, Sweden", "Stephen Chu, NEHTA, Australia (Editor)", "Matthew Cordell, NEHTA, Australia", "David Evans, Queensland Health, Australia", "Shahla Foozonkhah, Ocean Informatics, Australia", "Joanne Foster, School of Nursing & Midwifery, QLD University of Technology & Nursing Informatics Australia, Australia", "Jacquie Garton-Smith, Royal Perth Hospital and DoHWA, Australia", "Sarah Gaunt, NEHTA, Australia", "Andrew Goodchild, NEHTA, Australia", "Heather Grain, Llewelyn Grain Informatics, Australia", "Trina Gregory, cpc, Australia", "Grahame Grieve, Australia", "Sam Heard, Ocean Informatics, Australia", "Andrew James, University of Toronto, Canada", "Julie James, Blue Wave Informatics LLP, United Kingdom", "Ivor Jones, Queensalnd Helath, Australia", "Mary Kelaher, NEHTA, Australia", "Diane Kirkham, NEHTA, Australia", "Robert L'egan, NEHTA, Australia", "Jobst Landgrebe, ii4sm, Switzerland", "Heather Leslie, Ocean Informatics, Australia (Editor)", "Hugh Leslie, Ocean Informatics, Australia", "Rikard Lovstrom, Swedish Medical Association, Sweden", "Sarah Mahoney, Australia", "Mike Martyn, The Hobart Anaesthetic Group, Australia", "David McKillop, NEHTA, Australia", "Ian McNicoll, Ocean Informatics, United Kingdom", "Chris Mitchell, RACGP, Australia", "Stewart Morrison, NEHTA, Australia", "Jörg Niggemann, Compugroup, Germany", "Chris Pearce, Melbourne East GP Network, Australia", "General Practice Computing Group, Australia", "Camilla Preeston, Royal Australian College of General Practitioners, Australia", "Margaret Prichard, NEHTA, Australia", "Jodie Pycroft, Adelaide Northern Division of General Practice Ltd, Australia", "Cathy Richardson, NEHTA, Australia", "Robyn Richards, NEHTA - Clinical Terminology, Australia", "Thilo Schuler, Australia", "Peter Scott, Medical Objects, Australia", "Elena Shabanova, UMMSSOft, Russian Federation", "Elizabeth Stanick, Hobart Anaesthetic Group, Australia", "Hwei-Yee Tai, Tan Tock Seng Hospital, Singapore", "John Taylor, NEHTA, Australia", "Gordon Tomes, Australian Institute of Health and Welfare, Australia", "Richard Townley-O'Neill, NEHTA, Australia", "Kylie Young, The Royal Australian College of General Practitioners, Australia">
	other_details = <
		["references"] = <"Adverse Reaction, draft archetype, National eHealth Transition Authority [Internet]. NEHTA Clinical Knowledge Manager. Authored: 08 Nov 2010. Available at: http://dcm.nehta.org.au/ckm/OKM.html#showarchetype_1013.1.868_7 (accessed Jan 16, 2012).
Allergy, clinical element model, GE/Intermountain Healthcare. Clinical Element Model Search. Available at: http://intermountainhealthcare.org/cem/Pages/Detail.aspx?NCID=520861661&k=allergy (accessed Jan 16, 2012).
Edwards IR, Aronson JK. Adverse drug reactions: definitions, diagnosis, and management. Lancet. 2000 Oct 7;356(9237):1255-9. PubMed PMID: 11072960. 
Horsfield P, Sibeko S. Representation in Electronic Patient Records of Allergic Reactions, Adverse Reactions, and Intolerance of Pharmaceutical Products [Internet]. London, UK: National Health Service; 2006 Sep 07 [cited 2011 Jun 21]; Available at https://svn.connectingforhealth.nhs.uk/svn/public/nhscontentmodels/TRUNK/ref/NPfIT/Allergy_ADR_Intolerance%20v%201.2Final.doc.
Long R, Bentley S. SCG Guidance on the Representation of Allergies and Adverse Reaction Information Using NHS Message Templates [Internet]. London, UK: National Health Service; 2008 Apr 30 [cited 2011 Jun 21]; Available at http://www.connectingforhealth.nhs.uk/systemsandservices/data/scg/scg0001.pdf.
Microsoft. Design Guidance: Displaying Adverse Drug Reaction Risks [Internet]. 2009 January 28 [cited 2011 Jun 21]; Available at www.mscui.net/DesignGuide/DisplayingAllergies.aspx.

Microsoft. Design Guidance: Recording Adverse Drug Reaction Risks [Internet]. 2009 March 27 [cited 2011 Jun 21]; Available at www.mscui.net/DesignGuide/RecordingAllergies.aspx.

Mosby. Mosby's Pocket Dictionary of Medicine, Nursing and Health Professions. 6th Edition. USA: Mosby Elsevier; 2010
National E-Health Transition Authority. Adverse Reactions (Data Specifications) Version 1.1 [Internet]. Sydney, Australia: NEHTA; 2008 Feb 29 [cited 2011 Jun 21]; Available at http://www.nehta.gov.au/component/docman/doc_download/453-adverse-reaction-data-specification-v11.
Riedl MA, Casillas AM. Adverse drug reactions: types and treatment options. Am Fam Physician. 2003 Nov 1;68(9):1781-90. Review. PubMed PMID: 14620598.
Royal Australian College of General Practitioners. Fact Sheet: Allergies & Adverse Reactions (Draft). 2010.
Thien FC. Drug hypersensitivity. Med J Aust. 2006 Sep 18;185(6):333-8. Review. PubMed PMID: 16999678.">
		["MD5-CAM-1.0.1"] = <"260699D2EFDE4F7C7BC3C6C501A51A61">
	>
definition
	EVALUATION[at0000] matches {	-- Adverse Reaction
		data matches {
			ITEM_TREE[at0001] matches {	-- Tree
				items cardinality matches {1..*; unordered} matches {
					ELEMENT[at0002] matches {	-- Substance/Agent
						value matches {
							DV_TEXT matches {*}
						}
					}
					ELEMENT[at0004] occurrences matches {0..1} matches {	-- Absolute Contraindication?
						value matches {
							DV_BOOLEAN matches {
								value matches {True}
							}
						}
					}
					ELEMENT[at0049] occurrences matches {0..1} matches {	-- Future Use
						value matches {
							DV_TEXT matches {*}
						}
					}
					ELEMENT[at0006] occurrences matches {0..1} matches {	-- Overall Comment
						value matches {
							DV_TEXT matches {*}
						}
					}
					CLUSTER[at0009] occurrences matches {0..*} matches {	-- Reaction Event
						items cardinality matches {1..*; unordered} matches {
							ELEMENT[at0010] occurrences matches {0..1} matches {	-- Specific Substance/Agent
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0011] occurrences matches {0..*} matches {	-- Manifestation
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0016] occurrences matches {0..1} matches {	-- Reaction Type
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0021] occurrences matches {0..1} matches {	-- Certainty
								value matches {
									DV_CODED_TEXT matches {
										defining_code matches {
											[local::
											at0022, 	-- Suspected
											at0023, 	-- Probable
											at0024]	-- Confirmed
										}
									}
								}
							}
							ELEMENT[at0012] occurrences matches {0..1} matches {	-- Reaction Description
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0027] occurrences matches {0..1} matches {	-- Onset of Reaction
								value matches {
									DV_DATE_TIME matches {*}
								}
							}
							ELEMENT[at0028] occurrences matches {0..1} matches {	-- Duration of Reaction
								value matches {
									DV_DURATION matches {*}
								}
							}
							allow_archetype CLUSTER[at0029] occurrences matches {0..*} matches {	-- Additional Reaction Detail
								include
									archetype_id/value matches {/openEHR-EHR-CLUSTER\.anatomical_location(-[a-zA-Z0-9_]+)*\.v1/}
							}
							ELEMENT[at0018] occurrences matches {0..1} matches {	-- Exposure Description
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0020] occurrences matches {0..1} matches {	-- Earliest Exposure
								value matches {
									DV_DATE_TIME matches {*}
								}
							}
							ELEMENT[at0025] occurrences matches {0..1} matches {	-- Duration of Exposure
								value matches {
									DV_DURATION matches {*}
								}
							}
							allow_archetype CLUSTER[at0019] occurrences matches {0..*} matches {	-- Additional Exposure Detail
								include
									archetype_id/value matches {/openEHR-EHR-CLUSTER\.amount(-[a-zA-Z0-9_]+)*\.v1|openEHR-EHR-CLUSTER\.medication_admin(-[a-zA-Z0-9_]+)*\.v1|openEHR-EHR-CLUSTER\.timing(-[a-zA-Z0-9_]+)*\.v1/}
							}
							ELEMENT[at0040] occurrences matches {0..1} matches {	-- Clinical Management Description
								value matches {
									DV_TEXT matches {*}
								}
							}
							ELEMENT[at0031] occurrences matches {0..*} matches {	-- Multimedia
								value matches {
									DV_MULTIMEDIA matches {
										media_type matches {[openEHR::]}
									}
								}
							}
							allow_archetype CLUSTER[at0041] occurrences matches {0..*} matches {	-- Reporting Details
								include
									archetype_id/value matches {/.*/}
							}
							ELEMENT[at0032] occurrences matches {0..1} matches {	-- Reaction Comment
								value matches {
									DV_TEXT matches {*}
								}
							}
						}
					}
				}
			}
		}
		protocol matches {
			ITEM_TREE[at0042] matches {	-- Tree
				items cardinality matches {0..*; unordered} matches {
					ELEMENT[at0044] occurrences matches {0..1} matches {	-- Reaction Reported?
						value matches {
							DV_BOOLEAN matches {
								value matches {True, False}
							}
						}
					}
					ELEMENT[at0048] occurrences matches {0..1} matches {	-- Report Comment
						value matches {
							DV_TEXT matches {*}
						}
					}
					ELEMENT[at0045] occurrences matches {0..*} matches {	-- Adverse Reaction Report
						value matches {
							DV_URI matches {*}
						}
					}
					ELEMENT[at0047] occurrences matches {0..1} matches {	-- Supporting Clinical Record Information
						value matches {
							DV_EHR_URI matches {*}
						}
					}
				}
			}
		}
	}


ontology
	term_definitions = <
		["ar-sy"] = <
			items = <
				["at0000"] = <
					text = <"التفاعل الضائر">
					description = <"*A harmful or undesirable, unexpected effect associated with exposure to any substance or agent, including food, plants, animals, venom from animal stings, or a medication at therapeutic or sub-therapeutic doses.(en)">
				>
				["at0001"] = <
					text = <"*Tree(en)">
					description = <"*@ internal @(en)">
				>
				["at0002"] = <
					text = <"*Substance/Agent(en)">
					description = <"*Identification of a substance, agent, or a class of substance, that is considered to be responsible for the Adverse Reaction.(en)">
					comment = <"*Substance/Agent should be coded with a terminology, where possible.(en)">
				>
				["at0004"] = <
					text = <"*Absolute Contraindication?(en)">
					description = <"*Is administration of this Substance/Agent absolutely contraindicated in this individual?(en)">
					comment = <"*A flag indicating that a clinician has identified a propensity for a serious reaction upon further exposure to the Substance/Agent. Record as True if the clinician recommends that deliberate or voluntary exposure to, or administration of, the Substance/Agent should be prevented in future.(en)">
				>
				["at0006"] = <
					text = <"*Overall Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction as a whole, not captured in other fields.(en)">
				>
				["at0009"] = <
					text = <"*Reaction Event(en)">
					description = <"*Details about each Adverse Reaction Event.(en)">
				>
				["at0010"] = <
					text = <"*Specific Substance/Agent(en)">
					description = <"*Specific identification of the actual Substance/Agent considered to be responsible for the Adverse Reaction event.(en)">
					comment = <"*Coding of the specific Substance/Agent with a terminology is preferred, where possible. For example, a medication trade name or identification of a specific food.(en)">
				>
				["at0011"] = <
					text = <"*Manifestation(en)">
					description = <"*Clinical manifestation of the Adverse Reaction expressed as a single word, phrase or brief description, e.g. nausea or rash.(en)">
					comment = <"*Manifestation should be coded with a terminology, where possible. The values entered here may be used to display on an application screen as part a list of adverse reactions, as recommended in the NHS CUI guidelines.(en)">
				>
				["at0012"] = <
					text = <"*Reaction Description(en)">
					description = <"*Narrative description of the Adverse Reaction.(en)">
				>
				["at0016"] = <
					text = <"فئة التفاعل">
					description = <"*The type of Adverse Reaction as determined by the clinician.(en)">
				>
				["at0018"] = <
					text = <"*Exposure Description(en)">
					description = <"*Description about exposure to the Substance/Agent.(en)">
				>
				["at0019"] = <
					text = <"*Additional Exposure Detail(en)">
					description = <"*Additional detail about exposure/s for this Adverse Reaction event, including structured medication amount/frequency/route information.(en)">
				>
				["at0020"] = <
					text = <"*Earliest Exposure(en)">
					description = <"*Record of the date and/or time of the earliest or initial exposure to the Substance/Agent.(en)">
				>
				["at0021"] = <
					text = <"*Certainty(en)">
					description = <"*Degree of certainty, as assessed by a clinician, that the specific Substance/Agent was the cause of the Adverse Reaction.(en)">
				>
				["at0022"] = <
					text = <"*Suspected(en)">
					description = <"*Possibly the causative agent.(en)">
				>
				["at0023"] = <
					text = <"*Probable(en)">
					description = <"*Likely to be the causative agent, but not confirmed by testing or rechallenge.(en)">
				>
				["at0024"] = <
					text = <"*Confirmed(en)">
					description = <"*Confirmed as the causative agent, by testing or rechallenge.(en)">
				>
				["at0025"] = <
					text = <"مدة التعرض">
					description = <"*The amount of time of exposure to the Substance/Agent.(en)">
				>
				["at0027"] = <
					text = <"تاريخ بداية التفاعل">
					description = <"التاريخ و الوقت الذي بدأ فيه التفاعل.">
				>
				["at0028"] = <
					text = <"مدة التفاعل">
					description = <"مدة التفاعل.">
				>
				["at0029"] = <
					text = <"*Additional Reaction Detail(en)">
					description = <"*Additional detail about the Adverse Reaction, including anatomical location.(en)">
				>
				["at0031"] = <
					text = <"*Multimedia(en)">
					description = <"*Inclusion of any multimedia file to support the recording of the Adverse Reaction event.(en)">
					comment = <"*For example, a photo of a rash or presentation with angioneurotic oedema.(en)">
				>
				["at0032"] = <
					text = <"*Reaction Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction event not captured in other fields.(en)">
				>
				["at0040"] = <
					text = <"*Clinical Management Description(en)">
					description = <"*Narrative description of the clinical management provided.(en)">
				>
				["at0041"] = <
					text = <"*Reporting Details(en)">
					description = <"*Further details required for reporting to regulatory bodies.(en)">
				>
				["at0042"] = <
					text = <"*Tree(en)">
					description = <"*@ internal @(en)">
				>
				["at0044"] = <
					text = <"*Reaction Reported?(en)">
					description = <"*Was the Adverse Reaction reported to a regulatory body?(en)">
				>
				["at0045"] = <
					text = <"*Adverse Reaction Report(en)">
					description = <"*Link to an Adverse Reaction Report sent to a regulatory body.(en)">
				>
				["at0047"] = <
					text = <"*Supporting Clinical Record Information(en)">
					description = <"*Link to further information about the presentation and findings that exist elsewhere in the health record, including allergy test reports.(en)">
					comment = <"*For example, presenting symptoms, examination findings, diagnosis etc.(en)">
				>
				["at0048"] = <
					text = <"*Report Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction Report, including the reason for non-reporting, if required.(en)">
				>
				["at0049"] = <
					text = <"*Future Use(en)">
					description = <"*Narrative description of clinician instructions or advice related to future exposure to, or administration of, the Substance/Agent.(en)">
				>
			>
		>
		["en"] = <
			items = <
				["at0000"] = <
					text = <"Adverse Reaction">
					description = <"A harmful or undesirable, unexpected effect associated with exposure to any substance or agent, including food, plants, animals, venom from animal stings, or a medication at therapeutic or sub-therapeutic doses.">
				>
				["at0001"] = <
					text = <"Tree">
					description = <"@ internal @">
				>
				["at0002"] = <
					text = <"Substance/Agent">
					description = <"Identification of a substance, agent, or a class of substance, that is considered to be responsible for the Adverse Reaction.">
					comment = <"Substance/Agent should be coded with a terminology, where possible.">
				>
				["at0004"] = <
					text = <"Absolute Contraindication?">
					description = <"Is administration of this Substance/Agent absolutely contraindicated in this individual?">
					comment = <"A flag indicating that a clinician has identified a propensity for a serious reaction upon further exposure to the Substance/Agent. Record as True if the clinician recommends that deliberate or voluntary exposure to, or administration of, the Substance/Agent should be prevented in future.">
				>
				["at0006"] = <
					text = <"Overall Comment">
					description = <"Additional narrative about the Adverse Reaction as a whole, not captured in other fields.">
				>
				["at0009"] = <
					text = <"Reaction Event">
					description = <"Details about each Adverse Reaction Event.">
				>
				["at0010"] = <
					text = <"Specific Substance/Agent">
					description = <"Specific identification of the actual Substance/Agent considered to be responsible for the Adverse Reaction event.">
					comment = <"Coding of the specific Substance/Agent with a terminology is preferred, where possible. For example, a medication trade name or identification of a specific food.">
				>
				["at0011"] = <
					text = <"Manifestation">
					description = <"Clinical manifestation of the Adverse Reaction expressed as a single word, phrase or brief description, e.g. nausea or rash.">
					comment = <"Manifestation should be coded with a terminology, where possible. The values entered here may be used to display on an application screen as part a list of adverse reactions, as recommended in the NHS CUI guidelines.">
				>
				["at0012"] = <
					text = <"Reaction Description">
					description = <"Narrative description of the Adverse Reaction.">
				>
				["at0016"] = <
					text = <"Reaction Type">
					description = <"The type of Adverse Reaction as determined by the clinician.">
					comment = <"Coding of the reaction type is preferred, where possible. Examples: Immune mediated - Types I-IV (including allergy and hypersensitivity); Non-immune mediated - including pseudoallergic reaction, side effect, intolerance, drug toxicity, drug-drug interaction, food-drug interaction, drug-disease interaction and idiosyncratic reaction.">
				>
				["at0018"] = <
					text = <"Exposure Description">
					description = <"Description about exposure to the Substance/Agent.">
				>
				["at0019"] = <
					text = <"Additional Exposure Detail">
					description = <"Additional detail about exposure/s for this Adverse Reaction event, including structured medication amount/frequency/route information.">
				>
				["at0020"] = <
					text = <"Earliest Exposure">
					description = <"Record of the date and/or time of the earliest or initial exposure to the Substance/Agent.">
				>
				["at0021"] = <
					text = <"Certainty">
					description = <"Degree of certainty, as assessed by a clinician, that the specific Substance/Agent was the cause of the Adverse Reaction.">
				>
				["at0022"] = <
					text = <"Suspected">
					description = <"Possibly the causative agent.">
				>
				["at0023"] = <
					text = <"Probable">
					description = <"Likely to be the causative agent, but not confirmed by testing or rechallenge.">
				>
				["at0024"] = <
					text = <"Confirmed">
					description = <"Confirmed as the causative agent, by testing or rechallenge.">
				>
				["at0025"] = <
					text = <"Duration of Exposure">
					description = <"The amount of time of exposure to the Substance/Agent.">
				>
				["at0027"] = <
					text = <"Onset of Reaction">
					description = <"Record of the date and/or time of the onset of the Adverse Reaction.">
				>
				["at0028"] = <
					text = <"Duration of Reaction">
					description = <"The amount of time that the Adverse Reaction was present.">
				>
				["at0029"] = <
					text = <"Additional Reaction Detail">
					description = <"Additional detail about the Adverse Reaction, including anatomical location.">
				>
				["at0031"] = <
					text = <"Multimedia">
					description = <"Inclusion of any multimedia file to support the recording of the Adverse Reaction event.">
					comment = <"For example, a photo of a rash or presentation with angioneurotic oedema.">
				>
				["at0032"] = <
					text = <"Reaction Comment">
					description = <"Additional narrative about the Adverse Reaction event not captured in other fields.">
				>
				["at0040"] = <
					text = <"Clinical Management Description">
					description = <"Narrative description of the clinical management provided.">
				>
				["at0041"] = <
					text = <"Reporting Details">
					description = <"Further details required for reporting to regulatory bodies.">
				>
				["at0042"] = <
					text = <"Tree">
					description = <"@ internal @">
				>
				["at0044"] = <
					text = <"Reaction Reported?">
					description = <"Was the Adverse Reaction reported to a regulatory body?">
				>
				["at0045"] = <
					text = <"Adverse Reaction Report">
					description = <"Link to an Adverse Reaction Report sent to a regulatory body.">
				>
				["at0047"] = <
					text = <"Supporting Clinical Record Information">
					description = <"Link to further information about the presentation and findings that exist elsewhere in the health record, including allergy test reports.">
					comment = <"For example, presenting symptoms, examination findings, diagnosis etc.">
				>
				["at0048"] = <
					text = <"Report Comment">
					description = <"Additional narrative about the Adverse Reaction Report, including the reason for non-reporting, if required.">
				>
				["at0049"] = <
					text = <"Future Use">
					description = <"Narrative description of clinician instructions or advice related to future exposure to, or administration of, the Substance/Agent.">
				>
			>
		>
		["de"] = <
			items = <
				["at0000"] = <
					text = <"Nebenwirkung">
					description = <"*A harmful or undesirable, unexpected effect associated with exposure to any substance or agent, including food, plants, animals, venom from animal stings, or a medication at therapeutic or sub-therapeutic doses.(en)">
				>
				["at0001"] = <
					text = <"*Tree(en)">
					description = <"*@ internal @(en)">
				>
				["at0002"] = <
					text = <"*Substance/Agent(en)">
					description = <"*Identification of a substance, agent, or a class of substance, that is considered to be responsible for the Adverse Reaction.(en)">
					comment = <"*Substance/Agent should be coded with a terminology, where possible.(en)">
				>
				["at0004"] = <
					text = <"*Absolute Contraindication?(en)">
					description = <"*Is administration of this Substance/Agent absolutely contraindicated in this individual?(en)">
					comment = <"*A flag indicating that a clinician has identified a propensity for a serious reaction upon further exposure to the Substance/Agent. Record as True if the clinician recommends that deliberate or voluntary exposure to, or administration of, the Substance/Agent should be prevented in future.(en)">
				>
				["at0006"] = <
					text = <"*Overall Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction as a whole, not captured in other fields.(en)">
				>
				["at0009"] = <
					text = <"*Reaction Event(en)">
					description = <"*Details about each Adverse Reaction Event.(en)">
				>
				["at0010"] = <
					text = <"*Specific Substance/Agent(en)">
					description = <"*Specific identification of the actual Substance/Agent considered to be responsible for the Adverse Reaction event.(en)">
					comment = <"*Coding of the specific Substance/Agent with a terminology is preferred, where possible. For example, a medication trade name or identification of a specific food.(en)">
				>
				["at0011"] = <
					text = <"*Manifestation(en)">
					description = <"*Clinical manifestation of the Adverse Reaction expressed as a single word, phrase or brief description, e.g. nausea or rash.(en)">
					comment = <"*Manifestation should be coded with a terminology, where possible. The values entered here may be used to display on an application screen as part a list of adverse reactions, as recommended in the NHS CUI guidelines.(en)">
				>
				["at0012"] = <
					text = <"Beschreibung der Reaktion">
					description = <"*Narrative description of the Adverse Reaction.(en)">
				>
				["at0016"] = <
					text = <"Reaktionsart">
					description = <"*The type of Adverse Reaction as determined by the clinician.(en)">
				>
				["at0018"] = <
					text = <"*Exposure Description(en)">
					description = <"*Description about exposure to the Substance/Agent.(en)">
				>
				["at0019"] = <
					text = <"*Additional Exposure Detail(en)">
					description = <"*Additional detail about exposure/s for this Adverse Reaction event, including structured medication amount/frequency/route information.(en)">
				>
				["at0020"] = <
					text = <"*Earliest Exposure(en)">
					description = <"*Record of the date and/or time of the earliest or initial exposure to the Substance/Agent.(en)">
				>
				["at0021"] = <
					text = <"*Certainty(en)">
					description = <"*Degree of certainty, as assessed by a clinician, that the specific Substance/Agent was the cause of the Adverse Reaction.(en)">
				>
				["at0022"] = <
					text = <"*Suspected(en)">
					description = <"*Possibly the causative agent.(en)">
				>
				["at0023"] = <
					text = <"*Probable(en)">
					description = <"*Likely to be the causative agent, but not confirmed by testing or rechallenge.(en)">
				>
				["at0024"] = <
					text = <"*Confirmed(en)">
					description = <"*Confirmed as the causative agent, by testing or rechallenge.(en)">
				>
				["at0025"] = <
					text = <"Dauer der Exposition">
					description = <"*The amount of time of exposure to the Substance/Agent.(en)">
				>
				["at0027"] = <
					text = <"Datum des Beginns der Reaktion">
					description = <"Das Datum, an dem die Reaktion eintrat.">
				>
				["at0028"] = <
					text = <"Dauer der Reaktion">
					description = <"Die Dauer der Reaktion.">
				>
				["at0029"] = <
					text = <"*Additional Reaction Detail(en)">
					description = <"*Additional detail about the Adverse Reaction, including anatomical location.(en)">
				>
				["at0031"] = <
					text = <"*Multimedia(en)">
					description = <"*Inclusion of any multimedia file to support the recording of the Adverse Reaction event.(en)">
					comment = <"*For example, a photo of a rash or presentation with angioneurotic oedema.(en)">
				>
				["at0032"] = <
					text = <"*Reaction Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction event not captured in other fields.(en)">
				>
				["at0040"] = <
					text = <"*Clinical Management Description(en)">
					description = <"*Narrative description of the clinical management provided.(en)">
				>
				["at0041"] = <
					text = <"*Reporting Details(en)">
					description = <"*Further details required for reporting to regulatory bodies.(en)">
				>
				["at0042"] = <
					text = <"*Tree(en)">
					description = <"*@ internal @(en)">
				>
				["at0044"] = <
					text = <"*Reaction Reported?(en)">
					description = <"*Was the Adverse Reaction reported to a regulatory body?(en)">
				>
				["at0045"] = <
					text = <"*Adverse Reaction Report(en)">
					description = <"*Link to an Adverse Reaction Report sent to a regulatory body.(en)">
				>
				["at0047"] = <
					text = <"*Supporting Clinical Record Information(en)">
					description = <"*Link to further information about the presentation and findings that exist elsewhere in the health record, including allergy test reports.(en)">
					comment = <"*For example, presenting symptoms, examination findings, diagnosis etc.(en)">
				>
				["at0048"] = <
					text = <"*Report Comment(en)">
					description = <"*Additional narrative about the Adverse Reaction Report, including the reason for non-reporting, if required.(en)">
				>
				["at0049"] = <
					text = <"*Future Use(en)">
					description = <"*Narrative description of clinician instructions or advice related to future exposure to, or administration of, the Substance/Agent.(en)">
				>
			>
		>
	>
```

