Darwin Core Archive Examples
=============

This document tries to cover current or intendend uses of Darwin Core Archives that contain some sort of primary biodiversity data, i.e. primary species occurrence records. It tries not to explain the Darwin Core Archives format as such and assumes the reader knows about the technical details. For format details please see the following sources:

 * GBIF how to guide: http://www.gbif.org/resources/2552
 * Official meta.xml specs: http://rs.tdwg.org/dwc/terms/guides/text/index.htm
 * http://en.wikipedia.org/wiki/Darwin_Core_Archive

Uses cases are divided up by the core class used in the archive, specified as the *rowType* in the [meta.xml](http://rs.tdwg.org/dwc/terms/guides/text/index.htm).

# Occurrence
Classic, simple and flat records using the Occurrence rowType with all available dwc terms (only excluding [MeasurementsAndFacts](http://rs.gbif.org/extension/dwc/measurements_or_facts.xml) and [ResourceRelationship](http://rs.gbif.org/extension/dwc/resource_relation.xml) terms).

The location, event and taxon identification terms are all included in the core and a single occurrence record must therefore be taxonomically homogenous. It is adequate though to publish a single record for multiple individuals - dwc:individualCount can be used to declare exact numbers or a [new term currently under discussion](#abundance-term) for a more general abundance/quantity measurement suitable also for organisms like protists, fungi, grasses, etc.

The *dwc:basisOfRecord* term is used in this scenario to mark specimen, fossil, observation or living organism records. 


# Taxon
Archives using the Taxon class as the core are mostly referred to as *checklists*. They use only the taxonomic terms in the core and have extensions to publish data about specimens, vernacular names, literature, multimedia and more.

### Occurrence extension
The Occurrence class is used here as an extension. It is in use by Plazi and Pensoft to list the specimens from the *materials cited* section of a taxonomic treatment. As the taxon terms are already used in the core the Occurrence extension covers the remaining Location, Event, GeologicalContext, Identification & Occurrence terms. In theory the extension could also be used to list observations (again indicated by dwc:basisOfRecord).

Note that GBIF requires the presence of a unique *dwc:occurrenceID* although this is not strictly mandated by the dwc archive specification which only requires an identifier for the core records, not for extensions.

Example Plazi dataset *"Six new species of ants from Egypt"*:
 * DwC-A: http://plazi.cs.umb.edu/GgServer/dwca/D4F853101EB8608A8BD0E5B08F2CB167.zip
 * GBIF dataset page: http://www.gbif.org/dataset/1586aec3-17ca-44c7-ba95-a38c2a467465	

### TypesAndSpecimen extension
Alternatively to an extension based on the Occurrence rowType GBIF/GNA had defined a special, small extension to publish the type material found in taxonomic literature: http://rs.gbif.org/extension/gbif/1.0/typesandspecimen.xml

It is pretty much a subset of Occurrence and was designed before anyone was using the Occurrence rowType as an extension. Note that there is no occurrenceID or any other similar identifier in this extension.

### Distribution extension
Another checklist extension was created to publish synthesized species distributions/ranges often found in Faunas and Floras. A distribution record does not listen exact point locations of a species, but instead indicate some larger area like a country or a biogeographic region: http://rs.gbif.org/extension/gbif/1.0/distribution.xml

This extension was designed to also publish absence data indicated by an appropiate *dwc:occurrenceStatus*.


# Event
EU BON and other initiatives are currently planning to use the [dwc:Event core](http://rs.gbif.org/sandbox/core/dwc_event.xml) to be able to publish sample-based data, i.e. species abundance data and measurements about the survey site using the [MeasurementsAndFacts extension](http://rs.gbif.org/extension/dwc/measurements_or_facts.xml) in one archive. The Event core holds data about the where and when, so it covers all terms from Location, GeologicalContext and Event. 

## Occurrence extension
Using the Occurrence rowType as an extension to the Event core (together with some abundance term, see [Occurrence] above) allows to publish species abundance matrices such as Braun Blanquet vegetation plots or long term monitoring data.

As the Event core already covers Location, GeologicalContext and Event terms, the extension data only needs to hold Taxon, Identification and Occurrence terms. In some cases the actual extension data can be very simple and only use the occurrenceID and scientificName terms. Although abundance, individualCount, occurrenceStatus, recordedBy, recordNumber, sex, establishmentMeans and lifeStage should be useful additional terms in many cases.

occurrenceStatus


# MaterialSample
## incl Occurrence core
## Occurrence extension



# Open questions
### Abundance term
What exact new terms are needed to model various ways of measuring species abundance.
Open Darwin Core issues [#142](https://code.google.com/p/darwincore/issues/detail?id=142) & [#187](https://code.google.com/p/darwincore/issues/detail?id=187)

### Are both Event & MaterialSampe core needed ?

### Specimens as Occurrence or MaterialSample ?

### Deprecate TypesAndSpecimen extension ?
