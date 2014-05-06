Darwin Core Archive: Summary of use 
=============

The Darwin Core Archive (DwC-A) standard is the predominant standard for primary biodiversity data exchange within the GBIF network.  As the GBIF community is expanding into new types of data such as occurrences derived from sampling protocols, various proposals for using the DwC-A format have emerged, some including proposals for new core types.

This document aims to 
   1. concisely summarize the proposed formats of DwC-A
   2. provide links to reference datasets for each type
   3. provide links to proposed new cores and extension definitions
   4. provide observations on the key decisions needed

Use cases are provided for each community, categorized by the core class used in the archive, specified as the *rowType* in the *meta.xml*.

This summary is intended for audiences already familiar with the DwC-A format.  For those interested in learning more about the DwC-A format in general, please use the following sources:

 * Darwin Core Terms: http://rs.tdwg.org/dwc/terms/index.htm
 * GBIF how to guide: http://www.gbif.org/resources/2552
 * Official meta.xml specs: http://rs.tdwg.org/dwc/terms/guides/text/index.htm

# Occurrence
Classic, simple and flat records using the Occurrence rowType with all available dwc terms (only excluding [MeasurementOrFact][fact-ext] and [ResourceRelationship][rel-ext] terms).

![occurrence](occurrence.png)

The location, event and taxon identification terms are all included in the core and a single occurrence record must therefore be taxonomically homogeneous. It is adequate though to publish a single record for multiple individuals - dwc:individualCount can be used to declare exact numbers or a set of new terms currently under discussion (see the Event section below) for a more general abundance/quantity measurement suitable also for organisms like protists, fungi, grasses, etc.

The *dwc:basisOfRecord* term is used in this scenario to mark specimen, fossil, observation or living organism records. 


# Taxon
Archives using the Taxon class as the core are mostly referred to as *checklists*. They use only the taxonomic terms in the core and have extensions to publish data about specimens, descriptions, vernacular names, literature, multimedia and other data about taxa.

![taxon](taxon.png)

### Occurrence extension
The Occurrence class is used here as an extension. It is in use by Plazi and Pensoft to list the specimens from the materials cited section of a taxonomic treatment. The Chinese Academy of Sciences is about to publish a large Chinese checklist as part of Species2000 with occurrence data in an extension.

As the taxon terms are already used in the core, the Occurrence extension covers the remaining Location, Event, GeologicalContext, Identification & Occurrence terms. In theory the extension could also be used to list observations (again indicated by dwc:basisOfRecord).

Note that [GBIF recommends the presence][occid] of a unique *dwc:occurrenceID* in order to index the occurrence records in the Occurrence extension, although this is not strictly mandated by the DwC archive specification which only requires an identifier for the core records, not for extensions.

__Example__ *"Six new species of ants from Egypt"* from Plazi:
 * DwC archive: http://plazi.cs.umb.edu/GgServer/dwca/D4F853101EB8608A8BD0E5B08F2CB167.zip
 * GBIF dataset page: http://www.gbif.org/dataset/1586aec3-17ca-44c7-ba95-a38c2a467465  

__Example__ *3i - Cicadellinae Database*:
 * DwC archive: http://ctap.inhs.uiuc.edu/dmitriev/Export/DwCArchive\_Cicadellinae.zip
 * GBIF dataset page: http://www.gbif.org/dataset/26bca1b5-3ef6-4e97-9672-0058c79185fb

### TypesAndSpecimen extension
Alternatively to an extension based on the Occurrence rowType GBIF had previously defined a special, small extension to publish the typification information such as type species and type specimens found in taxonomic literature: http://rs.gbif.org/extension/gbif/1.0/typesandspecimen.xml

It is mostly a subset of Occurrence, but contains a few more typification orientied terms that only make sense in checklists. For example one can use it to publish a type species for a genus. Note that there is no occurrenceID or any other similar identifier in this extension. The extension is indexed into the GBIF [ChecklistBank][clb] and is in use by some checklist datasets, notably the datasets published by the [Species File Group][SFG].

__Example__ *Orthoptera Species File*:
 * DwC archive: http://ipt.speciesfile.org:8080/archive.do?r=orthoptera
 * GBIF dataset page: http://www.gbif.org/dataset/af66d4cf-0fd2-434b-9334-9806a5efa6f7



### Distribution extension
Another checklist extension was created to publish synthesized species ranges often found in Faunas and Floras. A distribution record does not listen exact point locations of a species, but instead indicates some larger area like a country or a biogeographic region where it is expected to exist: http://rs.gbif.org/extension/gbif/1.0/distribution.xml

This extension was designed to also publish absence data indicated by an appropriate *dwc:occurrenceStatus*.


# Event
The use of Darwin Core for sample-based data was explored in a recent [workshop][dwc-may] and currently, GBIF, as a partner in the EU BON project is [investigating][eubon-proposal] the use of the [dwc:Event core][event-core] to publish sample-based data using a special prototype of the [IPT][ipt] which is available at http://eubon-ipt.gbif.org/. Sample-based data is a type of data available from thousands of environmental, ecological, and natural resource investigations. These can be one-off studies or monitoring programmes. Such data are usually quantitative, calibrated, and follow certain protocols, so that changes and trends of populations can be detected.  This is in contrast to opportunistic observation and collection data, which today form a significant proportion of openly accessible biodiversity data.

![event](event.png)

The (Recording)Event core holds data about the where and when, so it covers all terms from Location, GeologicalContext and Event. 

> *DECISION*: The core event records would use *dwc:eventID* as the primary key to the core records. The *dc:type* should be Event.

To describe the exact kind of survey, dwc:samplingProtocol and dwc:samplingEffort from the Event group can be used.

> *QUESTION*: Is there a need to also have a eventType or overload basisOfRecord for the kind of Event?


Systematic surveys often need to relate sampling events with each other. To do that the generic ResourceRelationship extension could be used, but a distinct new term like *eventSeriesID* or *parentEventID* might be better suited. 

> *QUESTION*: Add a new term *eventSeriesID* or *parentEventID*?


### Occurrence extension
Using an [Occurrence extension][eventocc-ext] to the Event core together with some proposed new terms relating to abundance - specifically *quantity* and *quantityType* - allows for publishing species abundance matrices found in sample-based data such as Braun Blanquet vegetation plots or long term monitoring data. Not that the extension draft uses a new rowType *gbif:EventOccurrence* in order to distinguish it from the full, simple Occurrence. As the extension record does represent a true Occurrence the regular *dwc:Occurrence* rowType seems to be preferrable.

> *DECISION*: Establish new terms *dwc:quantity* and *dwc:quantityType* together with an initial vocabulary for recommended quantityType values. See Darwin Core issues [dwc142] and [dwc187]


> *DECISION*: Use regular *dwc:Occurrence* rowType for occurrence extensions instead of *gbif:EventOccurrence*.

As the Event core already covers Location, GeologicalContext and Event terms, the extension data only needs to hold Taxon, Identification and Occurrence terms. In some cases the actual extension data can be very simple and only use the occurrenceID and scientificName terms. Although abundance, individualCount, occurrenceStatus, recordedBy, recordNumber, sex, establishmentMeans and lifeStage should be useful additional terms in many cases.

Populating *occurrenceStatus* with *absent* allows in principle to also publish absence data as available in many surveys. It needs to be supplied explicitly for every species though so the approach is somewhat limited compared to declaring some taxonomic sampling context for the entire event or dataset.

__Example__ *Rhine Main Observatory Aquatic Invertebrates Biodiversity*:
 * DwC archive: http://eubon-ipt.gbif.org/archive.do?r=rhine-main-observatory-aquatic-invertebrates
 * IPT dataset page: http://eubon-ipt.gbif.org/resource.do?r=rhine-main-observatory-aquatic-invertebrates


### MaterialSample extension
A product of a recording event could also be physical samples, not just observations. Pending the question whether specimens are MaterialSample or Occurrence (see below) an Event core should also support a MaterialSample extension incl quantity terms very similar to the Occurrence extension.

### MeasurementOrFact extension
Having a [measurement extension][fact-ext] linked to a core Event allows to publish measurements about a site like temperature or soil acidity. On the downside one cannot describe measurements about a single specimen or observation as these are living in an extension as well.


# MaterialSample
Darwin Core added a new class term [MaterialSample][dwc:msample] in 2013 which can be used to publish occurrence data in new ways. A key driver for this new term are gene sequence based biodiversity data that are based on some sampling like tissue extractions, water or soil samples. Right now, there are two different proposals existing to use a MaterialSample core in Darwin Core archives mainly differing in the cardinality of a sample and species occurrence.

> *QUESTION*: When should the *Event* core be used instead of the *MaterialSample* core? Is the distinction here again the physical sampling, similar to single observation records (Occurrence) versus specimen (MaterialSample)?

### EnvO
The environment from which a material sample is derived needs to be described. The Environment Ontology [EnvO][envo] provides a controlled vocabulary for the description of environments, providing greater granularity than is currently possible with the Darwin Core *habitat* term. In addition to [habitat][dwc:habitat], EnvO provides three broad classifications for environment - biome, feature, and material. Using EnvO in Darwin Core would allow for standardised searches across environmental descriptions for a broad range of species/samples, including metagenomic samples which use the [MiXS][mixs] standard which already specifies use of EnvO terms.

Currently under review is a proposal that the value of the Darwin Core *habitat* term be selected from the EnvO habitat class and that three new terms (environmental material, environmental feature, and biome) be added to Darwin Core and their values drawn from the equivalent EnvO classes.

### sampleType
In order to distinguish the kind of sample, e.g. DNA extract, tissue, whole organism, lot, environmental sample, basisOfRecord could be used if the vocabulary is extended. However that might lead to a very overloaded and confusing vocabulary. It might be better to create a dedicated vocabulary for a new materialSampleType term.

> *QUESTION*: Create a new term *materialSampleType* to express the kind of sample?


### "Specimen" core

![sample](sample1.png)

As an outcome of the GSC16 BCO Hackathon in Oxford John Wiezcoreck created a [MaterialSample core][msample-core] that contains all terms a simple [Occurrence core][occ-core] also provides, but using the rowType *dwc:MaterialSample* with the *dwc:materialSampleID* identifier instead of *dwc:occurrenceID*.

It is proposed to use this rowType for all specimens, fossils and living organisms to make them distinct from pure observations which should still be using the *dwc:Occurrence* core. It can then also be used to publish data from the Global Genome Biodiversity Network (see [TDWG 2013 report][tdwg2013] where the main use case relates to DNA/tissue extraction and ability to follow a  chain of sampling/extracting.

An important requirement for (DNA) sampling is that one can follow back the chain of sampling/extracting. For this the generic ResourceRelationship extension could be used again if there is a shared, globally understood vocabulary. Alternatively a new term such as *parentMaterialSampleID* could build up such a link. The problem is very much the same as for relating events with the proposed *eventSeriesID*.

> *QUESTION*: Create a new term *parentMaterialSampleID*?

As the core contains the Taxon and Identification terms it can only be used to describe samples that contain (or a derived from?) a single taxon. This prevents it's use for environmental samples.

### Occurrence extension

![sample](sample2.png)

Based on the needs for environmental sampling and their subsequent metagenomic DNA sequencing the MaterialSample core could be restricted to just the sampling event covering terms from Location, Event, GeologicalContext and MaterialSample. Taxon abundance data would be stored in an *dwc:Occurrence* extension that covers the remaining Taxon, Identification and Occurrence terms. This setup is very much the same as for sample-based data using the *dwc:Event* core, but using the *dwc:MaterialSample* rowType and a different *dwc:materialSampleID* identifier.

For metagenomic results every cell of an [OTU abundance table][otu-table] would become an occurrence extension record with the abundance given using the quantity terms under discussion. A standard format for OTU tables is the [biom format][biom].

> *QUESTION*: Should a *MaterialSample* core be restricted to Location, Event, GeologicalContext and MaterialSample or contain all simple occurrence terms?

> *QUESTION*: Should the recommended rowType for a simple specimen record be *MaterialSample* or *Occurrence*?



[occ-core]:	http://rs.gbif.org/core/dwc_occurrence.xml
[event-core]:	http://rs.gbif.org/sandbox/core/dwc_event.xml
[msample-core]:	http://rs.gbif.org/sandbox/core/dwc_material_sample.xml
[fact-ext]:	http://rs.gbif.org/extension/dwc/measurements_or_facts.xml
[rel-ext]:	http://rs.gbif.org/extension/dwc/resource_relation.xml
[eventocc-ext]:	http://rs.gbif.org/sandbox/extension/event_occurrence.xml

[dwc:msample]:	http://rs.tdwg.org/dwc/terms/index.htm#MaterialSample
[dwc:habitat]: http://rs.tdwg.org/dwc/terms/index.htm#habitat

[dwc-may]:	http://www.standardsingenomics.org/index.php/sigen/article/view/sigs.4898640/1067
[eubon-proposal]:	GBIF-IPT-for-sample-data.docx
[tdwg2013]:	TDWG2013GGBNWGReport

[ipt]:	http://www.gbif.org/ipt
[clb]:	http://www.gbif.org/species
[occid]:	http://gbif.blogspot.dk/2014/04/ipt-v21.html
[SFG]:	http://www.gbif.org/publisher/47a779a6-a230-4edd-b787-19c3d2c80ab5
[envo]:	http://environmentontology.org/
[mixs]:	http://www.nature.com/nbt/journal/v29/n5/full/nbt.1823.html
[otu-table]:	http://www.wernerlab.org/teaching/qiime/overview/c
[biom]:	http://biom-format.org/documentation/biom_format.html

[dwc142]: https://code.google.com/p/darwincore/issues/detail?id=142
[dwc187]: https://code.google.com/p/darwincore/issues/detail?id=187
