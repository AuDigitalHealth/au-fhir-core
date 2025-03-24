{%   include search_parameters_intro.md -%}

<br/><br/>*Note:* Support for _id is mandatory for a responder and optional for a requester. Where the expectation for a search parameter differs between actors, the table below will reflect the stronger conformance requirement.

<table class="list">
<tbody>
  <tr>
    <th>Parameter(s)</th>
    <th>Conformance </th>
    <th>Type(s)</th>
    <th>Requirements (when used alone or in combination)</th>
  </tr>
  <tr>
        <td>_id</td>
        <td><b>SHOULD</b></td>
        <td><code>token</code></td>
        <td></td>
  </tr>
  <tr>
        <td>identifier</td>
        <td><b>SHALL</b></td>
        <td><code>token</code></td>
        <td>The requester <b>SHALL</b> provide both the system and code values. The responder <b>SHALL</b> support both.<br/><br/>The requester <b>SHOULD</b> support search using HPIO identifiers as defined in the profile. The responder <b>SHOULD</b> support search using the using HPIO, as defined in the profile.</td>
  </tr>
  <tr>
        <td>organization</td>
        <td><b>MAY</b></td>
        <td><code>reference</code></td>
        <td>The requester <b>SHALL</b> provide at least an id value and <b>MAY</b> provide both the Type and id values. The responder <b>SHALL</b> support both.</td>
  </tr>
  <tr>
        <td>location</td>
        <td><b>MAY</b></td>
        <td><code>reference</code></td>
        <td>The requester <b>SHALL</b> provide at least an id value and <b>MAY</b> provide both the Type and id values. The responder <b>SHALL</b> support both.</td>
  </tr>
  <tr>
        <td>coverageArea</td>
        <td><b>MAY</b></td>
        <td><code>reference</code></td>
        <td>The requester <b>SHALL</b> provide at least an id value and <b>MAY</b> provide both the Type and id values. The responder <b>SHALL</b> support both.</td>
  </tr>
  <tr>
        <td>type</td>
        <td><b>SHOULD</b></td>
        <td><code>token</code></td>
        <td>The requester <b>SHALL</b> provide at least a code value and <b>MAY</b> provide both the system and code values. The responder <b>SHALL</b> support both.</td>
  </tr><tr>
        <td>specialty</td>
        <td><b>SHOULD</b></td>
        <td><code>token</code></td>
        <td>The requester <b>SHALL</b> provide at least a code value and <b>MAY</b> provide both the system and code values. The responder <b>SHALL</b> support both.</td>
  </tr>
  
 </tbody>
</table>

#### Mandatory Search Parameters

The following search parameters and search parameter combinations **SHALL** be supported:

1. **SHALL** support searching using the **[`identifier`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?identifier=[system|][code]`

    Example:
    
      1. GET [base]/HealthcareService?identifier=http://ns.electronichealth.net.au/id/hi/hpio/1.0\|8003621566684455

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the identifier ([how to search by token](http://hl7.org/fhir/R4/search.html#token))

1. **SHALL** support searching using the **[`name`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?name=[string]`

    Example:

    1. GET [base]/HealthcareService?name=Albion%20Hospital%20Radiology%20Service

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the name ([how to search by string](http://hl7.org/fhir/R4/search.html#string))

#### Optional Search Parameters:

The following search parameters and search parameter combinations **SHOULD** be supported:

1. **SHOULD** support searching using the **[`organization`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:
    - **SHOULD** support chained searching of organisation canonical identifier `organization.identifier` (e.g. `organization.identifier=[system|][code]`)
    - **MAY** support chained searching of organisation name `organization.name` (e.g. `organization.name=[string]`)

    `GET [base]/HealthcareService?organization.identifier=[system|][code]`

    `GET [base]/HealthcareService?organization.name=[string]`

    Example:

    1. GET [base]/HealthcareService?organization.identifier=http://ns.electronichealth.net.au/id/hi/hpio/1.0\|8003626566706976
    1. GET [base]/HealthcareService?organization.name=murrabit%20public%20hospital
    
    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified organisation ([how to search by reference](http://hl7.org/fhir/R4/search.html#reference))

1. **SHOULD** support searching using the **[`service-type`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter, in order to search for a HealthcareService based on the type of service(s) it provides or offers.
    - **SHOULD** support *[multipleOr](http://hl7.org/fhir/R4/searchparameter-definitions.html#SearchParameter.multipleOr)* search on `service-type` (e.g.`service-type={system|}[code],{system|}[code],...`)

    `GET [base]/HealthcareService?service-type={system|}[code]{,{system|}[code],...}`

    Example:

    1. GET [base]/HealthcareService?service-type=http://snomed.info/sct\|1223451000168109
    1. GET [base]/HealthcareService?service-type=http://snomed.info/sct\|1223451000168109,http://snomed.info/sct\|1223411000168108

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified healthcare service type(s) ([how to search by token](http://hl7.org/fhir/R4/search.html#token))

1. **SHOULD** support searching using the **[`specialty`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:
    - **SHOULD** support *[multipleOr](http://hl7.org/fhir/R4/searchparameter-definitions.html#SearchParameter.multipleOr)* search on `specialty` (e.g.`specialty={system|}[code],{system|}[code],...`)

    `GET [base]/HealthcareService?specialty={system|}[code]{,{system|}[code],...}`

    Example:

    1. GET [base]/HealthcareService?specialty=http://snomed.info/sct\|394591006
    1. GET [base]/HealthcareService?specialty=http://snomed.info/sct\|394591006,721961006

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified specialty ([how to search by token](http://hl7.org/fhir/R4/search.html#token))

1. **SHOULD** support searching using the **[`location`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:
    - **SHOULD** support searching by location name (e.g. `location.name=[string]`)
    - **SHOULD** support searching by location address parts (e.g. `location.address-state=[string]`, `location.address-city=[string]`, `location.address-postalcode=[string]`)

    `GET [base]/HealthcareService?location.name=[string]`

    `GET [base]/HealthcareService?location.address-state=[string]`

    `GET [base]/HealthcareService?location.address-city=[string]`

    `GET [base]/HealthcareService?location.address-postalcode=[string]`

    Example: 

    1. GET [base]/HealthcareService?location.name=albion%20hospital
    1. GET [base]/HealthcareService?location.address-state=qld
    1. GET [base]/HealthcareService?location.address-city=bayview%20heights
    1. GET [base]/HealthcareService?location.address-postalcode=4868

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified location ([how to search by reference](http://hl7.org/fhir/R4/search.html#reference))

#### Other search candidates (to be removed)

1. **SHOULD / SHALL** support searching using the **[`active`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?active=[code]`
     
     Example: 
    
      1. GET [base]/HealthcareService?active=true

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified active status 


1. **SHOULD / SHALL** support searching using the **[`characteristic`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?characteristic=[system|][code]`

    Example:

    1. GET [base]/HealthcareService?characteristic=wheelchair%20accessibility

1. **SHOULD / SHALL** support searching using the **[`coverage-area`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter to identify healthcare services which operate or provide care in a limited area (the coverage area):
    - **SHOULD** support searching by coverage location address parts (e.g. `coverage-area.address-state=[string]`, `coverage-area.address-city=[string]`, `coverage-area.address-postalcode=[string]`)

    `GET [base]/HealthcareService?coverage-area.address-state=[string]`

    `GET [base]/HealthcareService?coverage-area.address-city=[string]`

    `GET [base]/HealthcareService?coverage-area.address-postalcode=[string]`

    Example: 

    1. GET [base]/HealthcareService?coverage-area.address-state=qld
    1. GET [base]/HealthcareService?coverage-area.address-city=bayview%20heights
    1. GET [base]/HealthcareService?coverage-area.address-postalcode=4868

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified coverage area ([how to search by reference](http://hl7.org/fhir/R4/search.html#reference))

1. **SHOULD / SHALL** support searching using the **[`endpoint`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:
    - **SHOULD** support searching by endpoint connection-type
    - **SHOULD** support searching by endpoint payload-type

    `GET [base]/HealthcareService?endpoint.connection-type=[system]|[code]`
    `GET [base]/HealthcareService?endpoint.payload-type=[system]|[code]`

    Example:

    1. GET [base]/HealthcareService?endpoint.connection-type=http://hl7.org.au/fhir/CodeSystem/smd-interfaces\|http://ns.electronichealth.net.au/smd/intf/SealedMessageDelivery/TLS/2010
    1. GET [base]/HealthcareService?endpoint.payload-type=http://hl7.org.au/fhir/CodeSystem/smd-interfaces\|http://ns.hl7.org.au/hl7v2/profiles/HL7AU-OO-REF-SIMPLIFIED-201706

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified endpoint ([how to search by reference](http://hl7.org/fhir/R4/search.html#reference))

1. **SHOULD / SHALL** support searching using the **[`program`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?program=[system]|[code]`

    Example:

    1. GET [base]/HealthcareService?program=http://snomed.info/sct\|310004004

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified program ([how to search by token](http://hl7.org/fhir/R4/search.html#token))

1. **SHOULD / SHALL** support searching using the **[`service-category`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameter:

    `GET [base]/HealthcareService?service-category=[system]|[code]`

    Example:

    1. GET [base]/HealthcareService?service-category=http://terminology.hl7.org/CodeSystem/service-category\|17

    *Implementation Notes:* Fetches a bundle containing any HealthcareService resources matching the specified category ([how to search by token](http://hl7.org/fhir/R4/search.html#token))

1. **SHOULD / SHALL** support searching using the combination of the **[`service-type`](https://hl7.org/fhir/R4/healthcareservice.html#search)**, **[`coverage-area`](https://hl7.org/fhir/R4/healthcareservice.html#search)** and **[`active`](https://hl7.org/fhir/R4/healthcareservice.html#search)** search parameters:

    `GET [base]/HealthcareService?service-type={system|}[code]{,{system|}[code],...}&coverage-area.address-=[string]&active=[code]`

    Example:

      1. GET [base]/HealthcareService?service-type=http://snomed.info/sc\|310080006&coverage-area.address-postalcode=4868,4867&active=true

    *Implementation Notes:* Fetches a bundle of all HealthcareService resources for the service type, coverage area and active status ([how to search by token](http://hl7.org/fhir/R4/search.html#token) and [how to search by string](http://hl7.org/fhir/R4/search.html#string))
