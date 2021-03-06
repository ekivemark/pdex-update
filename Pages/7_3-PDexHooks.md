Name Reference: #9484
Title: PDex Hooks
Show on Top Nav Menu: False | True
Top Nav Menu: 
---

Sharing of Member health information via PDex **SHALL** use the CDS Hooks specification. Connection to health plan systems **SHALL** be supported via the following hook:

- appointment-book

The overall flow of the SMART-on-FHIR and CDS-Hooks interaction is summarized in the diagram below:

<table>
	<tr>
		<td>
			<img  width="100%" height="auto"  src="PDexHooks.png">
		</td>
	</tr>	
</table>

It is possible that this hook will change over the course of the review/approval process, including changes to the names of the hooks, their context parameters or other information. Future versions of this implementation guide will be updated to align with such changes. Additional hooks may also be added.

This IG defines an extension to the appointment-book hook. The additional optional context fields are:

- MemberId (optional): The number that identifies the unique person in the health plan system

NOTE: Even pre-existing hooks are not yet locked down as normative and similar changes are possible, though perhaps less likely.

A sample of the CDS Hook for appointment-book is included below:

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
    "userId" : "Practitioner/A12365498",
    "patientId" : "EMR1239876",
    "encounterId" : "654",
    "appointments" : [],
		}
		"extension" : {
        "memberId" : "HP567123489", 
				"coverage" :  "Coverage/{{id}}
		}
  }
</pre>

If a Health Plan does not provide a Member Id on a coverage card the extension can reference a Coverage resource that contains the Subscriber Id and plan details and the beneficiary information (ie. the member demographic information).

Any identifiers associated with the coverage for the patient (which may include patient demographics) **SHOULD** be obtained from the FHIR Coverage record for the patient, or **MAY** be entered manually by the provider via the SMART-on-FHIR App.
