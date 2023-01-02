# WatDiv
## Waterloo SPARQL Diversity Test Suite

WatDiv is a benchmark designed to measure how an RDF data management system performs across a wide spectrum of SPARQL queries with varying structural characteristics and selectivity classes.

WatDiv consists of two components: the data generator and the query (and template) generator.

### Description of the Dataset

The WatDiv data generator allows users to define their own dataset through a dataset description language (see tutorial). This way, users can control

- which entities to include in their dataset,
- how "well-structured" each entity is (for details please refer to a research paper by Duan et al. [1]),
- how different entities are associated,
- the probability that an entity of type X is associated with an entity of type Y, and
- the cardinality of such associations.

Using these features, we designed the WatDiv test dataset (see the associated dataset description model). By executing the data generator with different scale factors, it is possible generate test datasets with different sizes. Table 1 lists the properties of the dataset at scale factor=1.
