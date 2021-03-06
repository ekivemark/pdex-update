The IG will continue to be tested at connectathons and will continue to utilize commonly adopted standards (e.g. US Core profiles) that have been tested by other groups (e.g. Argonaut). USCDI concepts are encapsulated in US-Core Profiles on FHIR Resources. The Vocabulary, Value Sets and codings used in this IG are based on US-Core Profiles. Regardless of the way in which payers store their administrative and clinical information they will need to map it appropriately to these profiles. 

In addition, we are creating a supplemental guide to provide more examples of how to populate the resources that are being exchanged based on the nature of the source information (e.g. lab results via V2 transactions, CDA, or claims).

# Intellectual Property

This HL7 specification contains and references intellectual property owned by third parties ("Third Party IP").  Implementers and testers of this specification **SHALL** abide by the license requirements for each terminology content artifact utilized within a functioning implementation. Terminology licenses **SHALL** be obtained from the Third Party IP owner for each code system and/or other specified artifact used.  It is the sole responsibility of each organization deploying or testing this specification to ensure their implementations comply with licensing requirements of each Third Party IP.

# Conventions

This implementation guide (IG) uses specific terminology to flag statements that have relevance for the evaluation of conformance with the guide:

**SHALL** indicates requirements that must be met to be conformant with the specification.

**SHOULD** indicates behaviors that are strongly recommended (and which may result in interoperability issues or sub-optimal behavior if not adhered to) but which do not, for this version of the specification, affect the determination of specification conformance.

**MAY** describes optional behaviors that are free to consider but where there is no recommendation for, or against, adoption.

It is important to differentiate in the Implementation Guide between identifiers used by the Provider/EMR and those used by the Payer/Health Plan to identify the patient/subject/member.

For the purposes of this IG we will use the following terms:

* **patient** or **subject** id will be used to express the identifier used by the provider to identify a patient/subject.

* **member** id will be used to express the identifier used by the payer/health plan to identify an individual member. Health Plans may historically have referred to these individual members as:
* Member
* Subscriber 
* Beneficiary
* Dependent
* Group Member
* Plan Member
* Covered Party
* Subject of Care


