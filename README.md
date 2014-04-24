Darwin Core Archive Examples
=============

This document tries to cover current or intendend uses of Darwin Core Archives that contain some sort of primary biodiversity data, i.e. primary species occurrence records. It tries not to explain the Darwin Core Archives format as such and assumes the reader knows about the technical details. For format details please see the following sources:

 * GBIF how to guide: http://www.gbif.org/resources/2552
 * Official meta.xml specs: http://rs.tdwg.org/dwc/terms/guides/text/index.htm
 * http://en.wikipedia.org/wiki/Darwin_Core_Archive

Uses cases are divided up by the core class used in the archive, specified as the *rowType* in the meta.xml.

# Occurrence
Classic, simple and flat records using the Occurrence rowType with all available dwc terms (only excluding [MeasurementsAndFacts](http://rs.gbif.org/extension/dwc/measurements_or_facts.xml) and [ResourceRelationship](http://rs.gbif.org/extension/dwc/resource_relation.xml) terms).


# Taxon
## /w Occurrence extension

## /w TypesAndSpecimen extension
http://rs.gbif.org/extension/gbif/1.0/typesandspecimen.xml

## /w Distribution extension
http://rs.gbif.org/extension/gbif/1.0/distribution.xml


# Event


# MaterialSample
##



