Name Reference: #8293
Title: US Core Location
Show on Top Nav Menu: False
Top Nav Menu: 
---

The  [US Core Location profile](http://hl7.org/fhir/us/core/StructureDefinition-us-core-location.html)  **SHALL** be used to record location/facility-specific information.

The essential fields to be provided in the US Core Location resource are:

| R4 Hierarchical Name          | R4 Name              | Card. | Type                                    |
|-------------------------------|----------------------|-------|-----------------------------------------|
| Location                      | Location             | 0..*  |                                         |
| Location.id                   | id                   | 0..1  | id                                      |
| Location.status               | status               | 0..1  | code                                    |
| Location.name                 | name                 | 1..1  | string                                  |
| Location.telecom              | telecom              | 0..*  | ContactPoint                            |
| Location.address              | address              | 0..1  | Address                                 |
| Location.address.line         | line                 | 0..*  | string                                  |
| Location.address.city         | city                 | 0..1  | string                                  |
| Location.address.state        | state                | 0..1  | string                                  |
| Location.address.postalCode   | postalCode           | 0..1  | string                                  |
| Location.managingOrganization | managingOrganization | 0..1  | Reference(US Core Organization Profile) |

#### Health Plan Mapping Assistance

A collaboration of Health Plan experts have performed an evaluation of claims information and developed a mapping of data for Members to the [US Core Location profile](http://hl7.org/fhir/us/core/StructureDefinition-us-core-location.html). This is shown below as an assistance  to implementers:

| Line | PayerSourceRecord | CMS BB 2.0 Field | Data Descriptor               | FHIR Profile     | Profile Field     | ValueSet                                                         | Notes |
|------|-------------------|------------------|-------------------------------|------------------|-------------------|------------------------------------------------------------------|-------|
| 15.1 | Claim             |  N/A                | Claim bill facility type code | US Core Location | .type             | http://build.fhir.org/v3/ServiceDeliveryLocationRoleType/vs.html |       |
| 5.1  | Claim-Provider    |  N/A                | Claim site of service NPI     | US Core Location | .identifier.value |                                                                  |       |
| 16.1 | Claim-Provider    |  N/A                | Claim service location NPI    | US Core Location | .identifier.value |                                                                  |       |
| 7.1  | Claim-Pharmacy    | N/A                 | Pharmacy service type code    | US Core Location | .type             |                                                                  |       |

Where an entry is provided in the CMS BB2.0 FIELD column the definition of the field can be reviewed using the following URL:

https://bluebutton.cms.gov/resources/variables/{CMS_BB2.0_FIELD}/

Where {CMS_BB2.0_FIELD} is replaced with the Field value in lower case. For example:

https://bluebutton.cms.gov/resources/variables/bene_id/
https://bluebutton.cms.gov/resources/variables/dob_dt/

#### Example Location Resource

An example mapping of a Location resource is shown here:

<pre>
{
  "resourceType" : "Location",
  "id" : "hl7east",
  "meta" : {
    "profile" : [
      "http://hl7.org/fhir/us/core/StructureDefinition/us-core-location"
    ]
  },
  "text" : {
    "status" : "generated",
    "div" : "<div xmlns=\"http://www.w3.org/1999/xhtml\"><p><b>Generated Narrative with Details</b></p><p><b>id</b>: hl7east</p><p><b>meta</b>: </p><p><b>identifier</b>: 29</p><p><b>status</b>: active</p><p><b>name</b>: Health Level Seven International - Amherst</p><p><b>description</b>: HL7 Headquarters - East</p><p><b>telecom</b>: ph: (+1) 734-677-7777</p><p><b>address</b>: 3300 Washtenaw Avenue, Suite 227 Amherst MA 01002 USA </p><h3>Positions</h3><table class=\"grid\"><tr><td>-</td><td><b>Longitude</b></td><td><b>Latitude</b></td></tr><tr><td>*</td><td>-72.519854</td><td>42.373222</td></tr></table><p><b>managingOrganization</b>: Health Level Seven International</p></div>"
  },
  "identifier" : [
    {
      "system" : "http://www.acme.org/location",
      "value" : "29"
    }
  ],
  "status" : "active",
  "name" : "Health Level Seven International - Amherst",
  "description" : "HL7 Headquarters - East",
  "telecom" : [
    {
      "system" : "phone",
      "value" : "(+1) 734-677-7777"
    }
  ],
  "address" : {
    "line" : [
      "3300 Washtenaw Avenue, Suite 227"
    ],
    "city" : "Amherst",
    "state" : "MA",
    "postalCode" : "01002",
    "country" : "USA"
  },
  "position" : {
    "longitude" : -72.519854,
    "latitude" : 42.373222
  },
  "managingOrganization" : {
    "display" : "Health Level Seven International"
  }
}
</pre>

Refer to the US Core Additional examples of the [US Core R4 Implementation Guide](http://hl7.org/fhir/us/core/) for further examples of completed [US Core Location Profiles ](http://hl7.org/fhir/us/core/StructureDefinition-us-core-location.html).





