See [Comparison with other national and international IGs](comparison.html) for a comparison between AU Core profiles and profiles in other implementation guides.

### Usage scenarios

The following are supported usage scenarios for this profile:

- Query for basic information about a healthcare service by name or identifier
- Record or update a record basic information for a healthcare service
- Read information about a healthcare service referenced by another resource

### Profile specific implementation guidance
- See guidance on the construction of an identifier on the relevant Identifier profile page and the section on [Business Identifiers](https://build.fhir.org/ig/hl7au/au-fhir-base/generalguidance.html#business-identifiers) in AU Base.
- A healthcare service's HPIO **SHOULD** be used in `HealthcareService.identifier` if available.
- `HealthcareService.category` provides an efficient way of supporting system interactions, e.g. restricting searches. Implementers need to understand that data categorisation is somewhat subjective. The categorisation applied by the source may not align with a receiver’s expectations. 
- The coverage area that a service is intended for/available to **SHOULD** be defined using one or more instances of the `coverageArea` element, with the address elements of the referenced `Location` populated depending on the type of coverage area to be defined.
