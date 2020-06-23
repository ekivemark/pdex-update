Name Reference: #5574
Title: Implementation Hierarchy and Priorities
Show on Top Nav Menu: False
Top Nav Menu: 

---
The PDex Implementation Guide (IG) will utilize existing HL7 FHIR Profiles in the following order of descending priority:

1. HL7 FHIR US Core STU3 v3.1.0 (based on FHIR R4 - [http://hl7.org/fhir/us/core/](http://hl7.org/fhir/us/core/) ) 
2. Da Vinci HRex IG profiles (based on FHIR R4 - [http://build.fhir.org/ig/HL7/davinci-ehrx/](http://build.fhir.org/ig/HL7/davinci-ehrx/) )

This Implementation Guide recognizes that Electronic Medical Record systems used by providers may have existing FHIR APIs that are based on versions of FHIR prior to FHIR R4 with DSTU2 (Argonaut) being the most popular implementation.

Amongst Health Plans there has been limited adoption of FHIR specifications and FHIR APIs. Therefore, for profiles and APIs identified in this IG the FHIR R4 version **SHALL** be used.


