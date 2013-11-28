#####Use Case ID: UC-PAS05
#####Use Case Name: Find Candidates

**Level:**                     User Level Goal

**Primary Actors:**            Medical Record Clerk (MRC)

**Stakeholders:**              Medical Record Clerk, Person, Healthcare Provider

**Purpose:**                   The main intent of this use case is to find candidates from person registry.

**Pre Condition:**             MRC must be identified and authenticated.

**Post Condition:**            Appropriate candidate found successfully.

**Frequency of Occurrence:**   High(Per Minute)
__________________________________________________________
**Main Success Scenario: (Find Candidates)**

1. User selects find candidate option.
2. System asks user to enter filtering criteria such as demographic information (including last name, address, gender and approximate birth date).
3. User specifies the values for filtering criteria.
4. System displays the list of person records.

_______________________________________________________________________________
**Alternate Flows** 

**Alt-1:**

1. No person record exist against the filtering criteria

________________________________________________________________________
**Reference Hl7 V3 Interaction Identifiers (Domain: Patient Administration):**

PRPA_ST101305UV02
_______________________________________________________________
**Reference CCHIT Criteria:**

N/A

_______________________________________________________________
**Reference Hl7 RMIM (Domain: Patient Administration):**
[More Details](http://www.hl7.org/implement/standards/product_brief.cfm?product_id=306)

![prpa_rm101306uv query by demographics](https://f.cloud.github.com/assets/5391320/1288047/1b29811c-3004-11e3-9f32-2748989fb2dc.png)
_______________________________________________________________
**Reference FHIR Resource:**
[More Details](http://www.hl7.org/implement/standards/fhir/resourcelist.html)

![person-resource](https://f.cloud.github.com/assets/5391320/1287912/c6008002-3001-11e3-851d-075f380b862c.png)
_______________________________________________________________
**Reference CDA Template:**
[More Details](http://www.hl7.org/Special/committees/structure/index.cfm)

N/A
_______________________________________________________________
**Reference OpenEHR Archetypes (Version 1.4):**
[More Details](http://www.openehr.org/ckm/)

OpenEHR Archetypes (Person)

``` Archetype

archetype (adl_version=1.4)
	openEHR-DEMOGRAPHIC-PERSON.person.v1

concept
	[at0000]	-- Dados da pessoa
language
	original_language = <[ISO_639-1::pt-br]>
	translations = <
		["en"] = <
			language = <[ISO_639-1::en]>
			author = <
				["name"] = <"Sergio Miranda Freire">
				["organisation"] = <"Universidade do Estado do Rio de Janeiro - UERJ">
				["email"] = <"sergio@lampada.uerj.br">
			>
		>
	>
description
	original_author = <
		["name"] = <"Sergio Miranda Freire & Rigoleta Dutra Mediano Dias">
		["organisation"] = <"Universidade do Estado do Rio de Janeiro - UERJ">
		["email"] = <"sergio@lampada.uerj.br">
		["date"] = <"22/05/2009">
	>
	details = <
		["en"] = <
			language = <[ISO_639-1::en]>
			purpose = <"Representation of a person's demographic data.">
			use = <"Used in demographic service to collect a person's data.">
			keywords = <"demographic service", "person's data">
			misuse = <"">
			copyright = <"© openEHR Foundation">
		>
		["pt-br"] = <
			language = <[ISO_639-1::pt-br]>
			purpose = <"Representação dos dados demográficos de uma pessoa.">
			use = <"Usado em serviço demográficos para coletar os dados de uma pessoa.">
			keywords = <"serviço demográfico", "dados de uma pessoa">
			misuse = <"">
			copyright = <"© openEHR Foundation">
		>
	>
	lifecycle_state = <"Authordraft">
	other_contributors = <"Sebastian Garde, Ocean Informatics, Germany (Editor)", "Omer Hotomaroglu, Turkey (Editor)", "Heather Leslie, Ocean Informatics, Australia (Editor)">
	other_details = <
		["references"] = <"ISO/TS 22220:2008(E) - Identification of Subject of Care - Technical Specification - International Organization for Standardization.">
	>

definition
    PERSON[at0000] matches {  -- person demographic data
        details matches {
             allow_archetype ITEM_TREE[at0001] occurrences matches {1..1} matches {
                 include
			        archetype_id/value matches {/(person_details)[a-zA-Z0-9_-]*\.v1/}
             }
        }
        identities matches {
            allow_archetype PARTY_IDENTITY[at0002] occurrences matches {1..1} matches {
                include
                    archetype_id/value matches {/(person_name)[a-zA-Z0-9_-]*\.v1/}
            }
        }
        contacts matches {
            CONTACT[at0003] occurrences matches {1..1} matches {  -- Contacts
                addresses matches {
                    allow_archetype ADDRESS[at0030] occurrences matches {1..1} matches {
                        include
                            archetype_id/value matches {/(address)([a-zA-Z0-9_-]+)*\.v1/}
                            archetype_id/value matches {/(electronic_communication)[a-zA-Z0-9_-]*\.v1/}
                    }
                }
            }
        }
        relationships matches {
 	    PARTY_RELATIONSHIP[at0004] matches {	-- personal relationships
	 	details matches {
		    ITEM_TREE matches {	
			items matches {
		       	    ELEMENT[at0040] matches {	-- type of relationship
			      	value matches { 
				    DV_TEXT matches {*}
				    DV_CODED_TEXT matches {
					defining_code matches {[ac0000]}
				    }		
				}
               		    }
			}
 		    }
		}
            }
        }
    }




ontology
	term_definitions = <
		["pt-br"] = <
			items = <
				["at0000"] = <
					text = <"Dados da pessoa">
					description = <"Dados da pessoa.">
				>
				["at0001"] = <
					text = <"Detalhes">
					description = <"Detalhes demográficos da pessoa.">
				>
				["at0002"] = <
					text = <"Nome">
					description = <"Conjunto de dados que especificam o nome da pessoa.">
				>
				["at0003"] = <
					text = <"Contatos">
					description = <"Contatos da pessoa.">
				>
				["at0004"] = <
					text = <"Relacionamentos">
					description = <"Relacionamentos de uma pessoa, especialmente laços familiares.">
				>
				["at0030"] = <
					text = <"Endereço">
					description = <"Endereços vinculados a um único contato, ou seja, com o mesmo período de validade.">
				>
				["at0040"] = <
					text = <"Grau de parentesco">
					description = <"Define o grau de parentesco entre as pessoas envolvidas.">
				>
			>
		>
		["en"] = <
			items = <
				["at0000"] = <
					text = <"Person">
					description = <"Personal demographic data.">
				>
				["at0001"] = <
					text = <"Demographic details">
					description = <"A person's demographic details.">
				>
				["at0002"] = <
					text = <"Name">
					description = <"A person's name.">
				>
				["at0003"] = <
					text = <"Contacts">
					description = <"A person's contacts.">
				>
				["at0004"] = <
					text = <"Relationships">
					description = <"A person's relationships, especially family ties.">
				>
				["at0030"] = <
					text = <"Addresses">
					description = <"Addresses linked to a single contact, i.e. with the same time validity.">
				>
				["at0040"] = <
					text = <"Relationship type">
					description = <"Defines the type of relationship between related persons.">
				>
			>
		>
	>
	constraint_definitions = <
		["pt-br"] = <
			items = <
				["ac0000"] = <
					text = <"Códigos para tipo de parentesco">
					description = <"códigos válidos para tipo de parentesco.">
				>
			>
		>
		["en"] = <
			items = <
				["ac0000"] = <
					text = <"Codes for type of relationship">
					description = <"Valid codes for type of relationship.">
				>
			>
		>
	>
```










