Name Reference: #7608
Title: US Core Patient
Show on Top Nav Menu: False
Top Nav Menu: 
---


The  [US Core Patient profile](http://hl7.org/fhir/us/core/StructureDefinition-us-core-patient.html)  **SHALL** be used to express a members demographic information.

The essential fields in the Patient profile are:

| R4 Hierarchical Name           | R4 Name           | Card. | Type            |
|--------------------------------|-------------------|-------|-----------------|
| Patient                        | Patient           | 0..*  |                 |
| Patient.id                     | id                | 0..1  | id              |
| Patient.us-core-race           | us-core-race      | 0..1  | (Complex)       |
| Patient.us-core-ethnicity      | us-core-ethnicity | 0..1  | (Complex)       |
| Patient.us-core-birthsex       | us-core-birthsex  | 0..1  | code            |
| Patient.identifier             | identifier        | 1..*  | Identifier      |
| Patient.identifier.system      | system            | 1..1  | uri             |
| Patient.identifier.value       | value             | 1..1  | string          |
| Patient.name                   | name              | 1..*  | HumanName       |
| Patient.name.family            | family            | 1..1  | string          |
| Patient.name.given             | given             | 1..*  | string          |
| Patient.gender                 | gender            | 1..1  | code            |
| Patient.birthDate              | birthDate         | 0..1  | date            |
| Patient.communication          | communication     | 0..*  | BackboneElement |
| Patient.communication.language | language          | 1..1  | CodeableConcept |

The Member Number will be entered in the ***identifier** field. The code **MB**  **SHALL** be used to identify the member identifier.  See the example below:

<pre>
{
      "use" : "member",
      "type" : {
        "coding" : [
          {
            "system" : "http://hl7.org/fhir/v2/0203",
            "code" : "MB",
            "display" : "Member Number"
          }
        ],
        "text" : "Health Plan Member Number"
      },
      "system" : "http://plan.healthplan.com",
      "value" : "987654321"
    }
</pre>


#### Health Plan Mapping Assistance

A collaboration of Health Plan experts have performed an evaluation of claims information and developed a mapping of  data for Members to the [US Core Patient profile](http://hl7.org/fhir/us/core/StructureDefinition-us-core-patient.html). This is shown below as an assistance  to implementers:

| Line | PayerSource | CMS BB 2.0 Field      | Data Descriptor        | FHIR Profile    | Profile Field               | ValueSet                                                       | Notes                |
|------|-------------|-----------------------|------------------------|-----------------|-----------------------------|----------------------------------------------------------------|----------------------|
| 1.1  | Member      | [BENE_ID](https://bluebutton.cms.gov/resources/variables/bene_id)               | Patientid              | US Core Patient | .identifier.value           |                                                                |                      |
| 2.1  | Member      | [DOB_DT](https://bluebutton.cms.gov/resources/variables/dob_dt)                | Date of birth          | US Core Patient | .birthDate                  |                                                                |                      |
| 3.1  | Member      |  N/A                     | Date of Death          | US Core Patient | .deceased[dateTime]         |                                                                |                      |
| 4.1  | Member      | [BENE_COUNTY_CD](https://bluebutton.cms.gov/resources/variables/bene_county_cd)        | County                 | US Core Patient | .contact.address.district   |                                                                |                      |
| 5.1  | Member      | [BENE_STATE_CD](https://bluebutton.cms.gov/resources/variables/bene_state_cd)         | State                  | US Core Patient | .contact.address.state      |                                                                |                      |
| 6.1  | Member      | [BENE_CNTY_CD](https://bluebutton.cms.gov/resources/variables/bene_cnty_cd)          | Country                | US Core Patient | .contact.address.country    |                                                                |                      |
| 7.1  | Member      | [BENE_RACE_CD](https://bluebutton.cms.gov/resources/variables/bene_race_cd)          | Race code              | US Core Patient | .us-core-race               |                                                                |                      |
| 8.1  | Member      |  N/A                     | Ethnicity              | US Core Patient | .us-core-ethnicity          |                                                                |                      |
| 9.1  | Member      | [GNDR_CD](https://bluebutton.cms.gov/resources/variables/gndr_cd)               | Gender code            | US Core Patient | .gender                     | [Valueset-administrative-gender - FHIR v3.0.1](http://hl7.org/fhir/STU3/valueset-administrative-gender.html)     |                      |
| 10.1 | Member      |  N/A                     | Name                   | US Core Patient | .name                       |                                                                |                      |
| 11.1 | Member      | [BENE_MLG_CNTCT_ZIP_CD](https://bluebutton.cms.gov/resources/variables/bene_mlg_cntct_zip_cd) | Zip code               | US Core Patient | .contact.address.postalCode |                                                                |                      |
| 7.1  | Claim       |  N/A                     | Patient account number | US Core Patient | .identifier.value           |                                                                |                      |
| 8.1  | Claim       |  N/A                     | Medical record number  | US Core Patient | .identifier.value           |                                                                |                      |
| F.1  | R4          |  N/A                     | Birth sex              | US Core Patient | .us-core-birthsex           | [US-Core-R4/ValueSet-birthsex](https://build.fhir.org/ig/HL7/US-Core-R4/ValueSet-birthsex.html)| UNK                  |
| F.2  | R4          |  N/A                     | Telecom                | US Core Patient | .telecom                    |                                                                | Provide If Available |
| F.3  | R4          |  N/A                     | Language               | US Core Patient | .communication              |                                                                | Provide If Available |

Where an entry is provided in the CMS BB2.0 FIELD column  above the definition of the field can be reviewed using the following URL:

https://bluebutton.cms.gov/resources/variables/{CMS_BB2.0_FIELD}/

Where {CMS_BB2.0_FIELD} is replaced with the Field value in lower case. For example:

https://bluebutton.cms.gov/resources/variables/bene_id/
https://bluebutton.cms.gov/resources/variables/dob_dt/

#### Example Patient Resource

An example mapping of a Patient resource is shown here:

<pre>
{
  "resourceType" : "Patient",
  "id" : "example",
  "meta" : {
    "profile" : [
      "http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient"
    ]
  },
  "text" : {
    "status" : "generated",
    "div" : "<div xmlns="http://www.w3.org/1999/xhtml">
			<p>
				<b>Generated Narrative with Details</b>
			</p>
			<p>
				<b>id</b>: example</p>
			<p>
				<b>identifier</b>: Medical Record Number = 1032702 (USUAL)</p>
			<p>
				<b>identifier</b>: Health Plan Member Number = 987654321 (USUAL)</p>
			<p>
				<b>active</b>: true</p>
			<p>
				<b>name</b>: Arthur B. Dent </p>
			<p>
				<b>telecom</b>: ph: 555-555-5555(HOME), amy.shaw@example.com</p>
			<p>
				<b>gender</b>: </p>
			<p>
				<b>birthsex</b>: Male</p>
			<p>
				<b>birthDate</b>: Jan 22, 1953</p>
			<p>
				<b>address</b>: 6518 Meadowridge Rd, Elkridge, MD 21075 US </p>
			<p>
				<b>race</b>: White, American Indian or Alaska Native, Asian, Shoshone, Filipino</p>
			<p>
				<b>ethnicity</b>: Hispanic or Latino, Dominican, Mexican</p>
		</div>"
  },
  "extension" : [
    {
      "url" : "http://hl7.org/fhir/us/core/StructureDefinition/us-core-race",
      "extension" : [
        {
          "url" : "ombCategory",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2106-3",
            "display" : "White"
          }
        },
        {
          "url" : "ombCategory",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "1002-5",
            "display" : "American Indian or Alaska Native"
          }
        },
        {
          "url" : "ombCategory",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2028-9",
            "display" : "Asian"
          }
        },
        {
          "url" : "detailed",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "1586-7",
            "display" : "Shoshone"
          }
        },
        {
          "url" : "detailed",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2036-2",
            "display" : "Filipino"
          }
        },
        {
          "url" : "text",
          "valueString" : "Mixed"
        }
      ]
    },
    {
      "url" : "http://hl7.org/fhir/us/core/StructureDefinition/us-core-ethnicity",
      "extension" : [
        {
          "url" : "ombCategory",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2135-2",
            "display" : "Hispanic or Latino"
          }
        },
        {
          "url" : "detailed",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2184-0",
            "display" : "Dominican"
          }
        },
        {
          "url" : "detailed",
          "valueCoding" : {
            "system" : "urn:oid:2.16.840.1.113883.6.238",
            "code" : "2148-5",
            "display" : "Mexican"
          }
        },
        {
          "url" : "text",
          "valueString" : "Hispanic or Latino"
        }
      ]
    },
    {
      "url" : "http://hl7.org/fhir/us/core/StructureDefinition/us-core-birthsex",
      "valueCode" : "M"
    }
  ],
  "identifier" : [
    {
      "use" : "member",
      "type" : {
        "coding" : [
          {
            "system" : "http://hl7.org/fhir/v2/0203",
            "code" : "MB",
            "display" : "Member Number"
          }
        ],
        "text" : "Health Plan Member Number"
      },
      "system" : "http://plan.healthplan.com",
      "value" : "987654321"
    },
    {
      "use" : "usual",
      "type" : {
        "coding" : [
          {
            "system" : "http://hl7.org/fhir/v2/0203",
            "code" : "MR",
            "display" : "Medical Record Number"
          }
        ],
        "text" : "Medical Record Number"
      },
      "system" : "http://hospital.smarthealthit.org",
      "value" : "1032702"
    }
  ],
  "active" : true,
  "name" : [
    {
      "family" : "Dent",
      "given" : [
        "Arthur",
        "B."
      ]
    }
  ],
  "telecom" : [
    {
      "system" : "phone",
      "value" : "555-555-5555",
      "use" : "home"
    },
    {
      "system" : "email",
      "value" : "arthur.dent@example.com"
    }
  ],
  "gender" : "male",
  "birthDate" : "1953-01-22",
  "address" : [
    {
      "line" : [
        "6518 Meadowridge Rd"
      ],
      "city" : "Elkridge",
      "state" : "MD",
      "postalCode" : "21075",
      "country" : "US"
    }
  ]
}
</pre>

Refer to the US Core Additional examples of the [US Core R4 Implementation Guide](http://hl7.org/fhir/us/core/) for further examples of completed [Patient Profiles ](http://hl7.org/fhir/us/core/StructureDefinition-us-core-patient.html).


