Name Reference: #6412
Title: FHIR Profiles and CDS Hooks Context
Show on Top Nav Menu: False
Top Nav Menu: 
---

The PDex IG makes significant use of established FHIR profiles. These **MAY** be qualified with search parameter definitions and terminology artifacts to describe the content to be shared as part of CDS Hook calls. The output from the CDS Hooks service will use FHIR R4 profiles identified in the US Core and Da Vinci HRex IGs.


The CDS Hooks Appointment-book call provides the Practitioner (UserId), Patient, Encounter identifiers and an appointments object.
Optional fields in the CDS Hooks for PDex context include:
- subscriberId
- access_token

The fields in the context of the CDS Hooks call are used as follows:
- userid: used to identify the provider requesting the information
- patientId: used to identify the patient/subject in the EMR system
- encounterid: used to identify the encounter in the provider's EMR
- memberId: used to describe the unique identifier for a health plan member. This identifier can be found in the Coverage resource as subscriber.id.
- access_token: Used to provide secure access into the Provider's EMR system in order to access the Patient record.

<pre>
{
  "hookInstance": "d1577c69-dfbe-44ad-ba6d-3e05e953b2ea",
  "fhirServer": "http://fhir.example.com",
  "fhirAuthorization" : {
       "access_token" : "some-opaque-fhir-access-token",
       "token_type" : "Bearer",
       "expires_in" : 300,
       "scope" : "patient/Patient.read patient/Observation.read",
       "subject" : "cds-service4"
     },
  "hook": "appointment-book",
  "user": "Practitioner/example",
  "context": {
    "userId": "Practitioner/A12365498",
    "patientId": "EMR1239876",
    "encounterId": "654",
    "appointments": [],
    "memberId": "HP567123489",
  }
}
</pre>

#### SMART-on-FHIR app Parameters

The SMART-on-FHIR app or service initiating the request to the Health Plan's CDS-Hooks service **SHALL** provide a callback URI to enable the CDS Hooks service to notify the SMART-on-FHIR App of the presence of a card.

In the case of an automated call to the Health Plan's CDS Hooks service the card will contain the token(s) needed to access the Health Plan and the card will link to a provider's SMART-on-FHIR app that **SHALL** recognize the Provider and the EMR system the app is connected to.

When a SMART-on-FHIR App is provided as a link in the content returned from the CDS Hooks it **SHALL** receive:

- The URL entrypoint to the Health Plan's FHIR API
- An access token to enable secure access to the Member's health history via the FHIR API
- An access token to enable the app to write data to the Provider's EMR system.

#### SMART-on-FHIR app default search queries

This IG utilizes US Core Profiles whereever practicable. As such this IG supports the search parameters identified in the [US Core IG](https://www.hl7.org/fhir/us/core/). 

The SMART App **SHOULD** provide the capability for a Provider, Organization, Implementer or administrator of a Provider's EMR System to define a set of valid FHIR search queries that can be executed against a Health Plan's FHIR API. This capability enables a Provider or Organization to define the boundaries for the information they are interested in receiving from a Health Plan's FHIR API.

The SMART App **SHALL** import an object from a configuration file containing one or more search queries. The search queries **SHALL** support replaceable parameters that will be exchanged for appropriate values when the query is executed.

The replaceable parameters supported by the SMART App **SHALL** include:

| Replaceable Parameter         | Purpose                                                                  |
|-------------------------------|--------------------------------------------------------------------------|
| [Health_Plan_Member_ID]       | The FHIR ID of the Member from the Patient Resource in the Payers system |
| [Patient_ID]                  | The FHIR ID of the Patient from the Provider's EMR System                |
| [Health_Plan_Practitioner_ID] | The Practitioner ID in the Health Plan's system                          |
| [Practitioner_ID]             | The Practitioner ID in the Provider's EMR System                         |
| [Health_Plan_Organization_ID] | The Organization ID in the Health Plan's system                          |
| [Organization_ID]             | The Organization ID in the Provider's EMR System                         |
| [Health_Plan_Location_ID]     | The Location ID in the Health Plan's system                              |
| [Location_ID]                 | The Location ID in the Provider's EMR system                             |
| [TODAY]                       | Today's Date                                                             |
| [TODAY-NNN]                   | A Calculated Date derived from Today's Date adjusted by a number of Days |

Examples of search queries with replaceable parameters are shown in the table below. Search queries can be created for any resources profiled in the US Core, Da Vinci HRex or Da Vinci PDex IG. A limited sample of these queries are:

| Search Example                                                                   | FHIR Search Query                                                                                                 |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Patient Record                                                                   | Patient?_id=[Health_Plan_Member_ID]                                                                               |
| Encounters for Patient updated since a January 1, 2019 and excluding my Location | Encounter?subject=Patient/[Health_Plan_Member_ID]&_lastUpdated=gt[TODAY-365]&location=ne[Health_Plan_Location_ID] |
| MedicationDispense for Patient created/updated in the last 3 months              | MedicationDispense?subject=Patient/[Health_Plan_Member_ID]&_lastUpdated=gt[TODAY-90]                              |

#### SMART-on-FHIR app for Provider data selection

The SMART App **SHALL** retrieve the CapabilityStatement/Metadata from the Health Plan's FHIR API.
 
The SMART App **SHALL** retrieve the ConformanceStatement/CapabilityStatement/Metadata from the Provider's EMR system. 

The Provider **MAY** select records from the Health Plan's FHIR API to be committed to their EMR system. After selecting the relevant data the provider **MAY** trigger a write of the selected data to their EMR system. Alternatively the Provider's organization **MAY** implement automated selection rules to commit data received to the EMR.

The SMART App **SHALL** use the EMRs Metadata to determine what records **MAY** be written to the EMR system. 

The SMART App **SHALL NOT** convert records from one FHIR version to another.

If the Provider's EMR system supports FHIR R4 the SMART App **SHALL** determine which resources may be written to the Patient's record in the EMR system. It will write these records to the Provider's EMR System. 

The set of records selected by the Provider to commit to the EMR shall be written to the EMR, as per the write rules enforced by the EMR. The remaining selected records that can't be written directly to the EMR shall be written as a DocumentReference per the format selection hierarchy identified in the following section [writing records usingdocumentreference](#writing-records-using-documentreference).

If the Provider's EMR system does not support FHIR R4 the SMART App **SHOULD** create a DocumentReference record and write the selected records to the Provider's EMR System using one of the actions identified in [writing records usingdocumentreference](#writing-records-using-documentreference), below.
    
#### Writing Records Using DocumentReference

The format used to write information to a DocumentReference resource in the Provider's EMR System **SHOULD** be written in order of descending preference identified below:

1. Place the remaining selected records in a FHIR bundle and create a Human Readable PDF of those selected records and write both items to a DocumentReference record for the Patient.
2. Convert the remaining records to an XHTML document and write to a DocumentReference record for the Patient.
3. Convert the remaining records to an ASCII text document and write to a DocumentReference record for the Patient.


