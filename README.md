Darwin Core Archive Examples
=============

This document tries to cover current or intendend uses of Darwin Core Archives that contain some sort of primary biodiversity data, i.e. primary species occurrence records. It tries not to explain the Darwin Core Archives format as such and assumes the reader knows about the technical details. For format details please see the following sources:

 * GBIF how to guide: http://www.gbif.org/resources/2552
 * Official meta.xml specs: http://rs.tdwg.org/dwc/terms/guides/text/index.htm
 * http://en.wikipedia.org/wiki/Darwin_Core_Archive

Uses cases are divided up by the core class used in the archive, specified as the *rowType* in the meta.xml.

# Occurrence
Classic, simple and flat records using the Occurrence rowType with all available dwc terms (only excluding [MeasurementsAndFacts](http://rs.gbif.org/extension/dwc/measurements_or_facts.xml) and [ResourceRelationship](http://rs.gbif.org/extension/dwc/resource_relation.xml) terms).

The location, event and taxon identification terms are all included in the core and a single occurrence record must therefore be taxonomically homogenous. It is adequate though to publish a single record for multiple individuals - dwc:individualCount can be used to declare exact numbers or a new term currently under discussion [#142](https://code.google.com/p/darwincore/issues/detail?id=142), [#187](https://code.google.com/p/darwincore/issues/detail?id=187) for a more general abundance/quantity measurement suitable also for organisms like protists, fungi, grasses, etc.

The dwc:basisOfRecord term is used in this scenario to mark specimen, fossil, observation or living organism records. 


# Taxon
Archives using the Taxon class as the core are mostly referred to as *checklists*. They only use the taxonomic terms in the core and use extensions to publish data about specimens, vernacular names, literature, multimedia and more.

### Occurrence extension
In use by Plazi and Pensoft to list the specimens from the *materials cited* section of a taxonomic treatment.

Example Plazi dataset *"Six new species of ants from Egypt"*:
 * DwC-A: http://plazi.cs.umb.edu/GgServer/dwca/D4F853101EB8608A8BD0E5B08F2CB167.zip
 * GBIF dataset page: http://www.gbif.org/dataset/1586aec3-17ca-44c7-ba95-a38c2a467465	

As the taxon terms are already used in the core the Occurrence extension only covers the Location, Event, Identification & Occurrence terms.
In theory the extension could also be used to list observations (again indicated by dwc:basisOfRecrod).

### TypesAndSpecimen extension
Alternatively to an extension based on the Occurrence rowType GBIF/GNA had defined a special, small extension to publish the type material found in taxonomic literature: http://rs.gbif.org/extension/gbif/1.0/typesandspecimen.xml

It is pretty much a subset of Occurrence and was designed before anyone was using the Occurrence rowType as an extension.

### Distribution extension
Another checklist extension was created to publish synthesized species distributions/ranges often found in Faunas and Floras. A distribution record does not listen exact point locations of a species, but instead indicate some larger area like a country or a biogeographic region: http://rs.gbif.org/extension/gbif/1.0/distribution.xml

This extension was designed to also publish absence data indicated by an appropiate dwc:occurrenceStatus.


# Event


# MaterialSample
##




https://code.google.com/p/darwincore/issues/detail?id=187