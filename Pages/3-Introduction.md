Name Reference: #9629
Title: Introduction
Show on Top Nav Menu: True
Top Nav Menu: Summary
---

The PDex Implementation Guide (IG) identifies three actors and specifies three interactions that occur. Each interaction differs based upon the actors involved and the data payload that **SHALL** be communicated. 

**Actors:**
1. Health Plans
2. Providers
3. Third-Party Applications
  
**Interactions:**
1. Payer to Provider Exchange
2. Member-authorized Health Plan to Health Plan Exchange
3. Member-authorized Health Plan to Third Party Applications 
	
The Blue Button 2.0 initiative (The CMS Blue Button 2.0 API and the CARIN Consumer-Directed Exchange IG) specifies the profiles used to communicate claims information between health plans and their members. The PDex Implementation Guide (IG) is focused on presenting a member's health and claims information as FHIR clinical profiles (based on US Core) that are more easily consumed by Electronic Medical Records (EMR) systems. 
                                                                                                                                                   
Ad-hoc PDex Member History Requests via CDS Hooks provides a mechanism for providers/clinicians to request information from health plans about the medical history for their patient as part of their regular workflow.  The requestor should be aware that the Health Plan may not have a complete medical history of services provided due to delays in billing, patient ability to pay for services, etc.

The same FHIR profiles used to support communication between the health plan and providers will also be used to provide the payload of member health information that will be exchanged between health plans when authorized by a health plan member.

The Patient-everything operation is also included as part of this implementation. This is included to provide Health Plans with the ability to pull or push member-authorized health history via a FHIR bundle that can be exchanged over existing, or future, secure transports between trusted parties.

While the authorization and communication mechanisms may differ between the provider-to-payer exchange and the member-authorized  Payer-to-Payer exchange or member-authorized Payer to Third-Party Application exchange the payload of member history will be the same.  
                                                                                                          
The objective with the above approach is to:

- Minimize the proliferation of FHIR profiles by encouraging the re-use of FHIR profiles that have seen significant development effort invested by stakeholders across health care
- Consolidate the number of operational interfaces that health plans and  EMR systems need to maintain in order to meet regulatory requirements.

