# WatDiv


## Waterloo SPARQL Diversity Test Suite

WatDiv is a benchmark designed to measure how an RDF data management system performs across a wide spectrum of SPARQL queries with varying structural characteristics and selectivity classes.

WatDiv consists of two components: the data generator and the query (and template) generator. The data generator generates the RDF dataset of a specified size while the query generator focuses on the generation of test queries that will be used in the study.

### Attribution

When using WatDiv, please cite the following publication:

G. Aluç, O. Hartig, M. T. Özsu, and K. Daudjee. [Diversified stress testing of RDF data management systems](https://doi.org/10.1007/978-3-319-11964-9_13), In _Proc. 13th Int. Semantic Web Conference_, Part I, pages 197–212, 2014.

### Description of WatDiv

The detailed description of WatDiv is [here](Description.md).

<!--
### Description of the Dataset

The WatDiv data generator allows users to define their own dataset through a dataset description language (see tutorial). This way, users can control

* which entities to include in their dataset,
* how "well-structured" each entity is (for details please refer to S. Duan, A. Kementsietsidis, K. Srinivas, and O. Udrea. Apples and oranges: a comparison of RDF benchmarks and real RDF datasets. In *Proc. ACM SIGMOD Int. Conf. on Management of Data*, 2011, pages 145-156.,
* how different entities are associated,
* the probability that an entity of type X is associated with an entity of type Y, and
* the cardinality of such associations.

Using these features,  the WatDiv test dataset is designed (see the associated <a href="watdiv-data-model.txt">dataset description model</a>). By executing the data generator with different scale factors, it is possible to generate test datasets with different sizes. <a href="#table:triples">Table 1</a> lists the properties of the dataset at scale factor=1.

<table border="1" cellpadding="0" cellspacing="0">
	<caption>
         <a name="table:triples"> 
            Table 1. Characteristics of the WatDiv test dataset at scale factor=1.
         </a>
     </caption>
<tbody>
<tr valign="top"><td><i>triples</i></td><td> 105257</td></tr>
<tr valign="top"><td><i>distinct subjects</i></td><td> 5597</td></tr>
<tr valign="top"><td><i>distinct predicates</i></td><td> 85</td></tr>
<tr valign="top"><td><i>distinct objects</i></td><td> 13258</td></tr>
<tr valign="top"><td><i>URIs</i></td><td> 5947</td></tr>
<tr valign="top"><td><i>literals</i></td><td> 14286</td></tr>
<tr valign="top"><td><i>distinct literals</i></td><td> 8018</td></tr>
</tbody>
</table>

An important characteristic that distinguishes the WatDiv test dataset from existing benchmarks is that instances of the same entity do not necessarily have the same set of attributes. <a href="#table:entities">Table 2</a> lists all the different entities used in WatDiv. Take the *Product* entity for instance. *Product instances* may be associated with different *Product Categories* (e.g., Book, Movie, Classical Music Concert, etc.), but depending on which category a product belongs to, it will have a different set of attributes. For example, products that belong to the category "Classical Music Concert" have the attributes *mo:opus*, *mo:movement*, *wsdbm:composer*, *mo:performer* (in addition to the attributes that is common to every product), whereas products that belong to the category "Book" have the attributes *sorg:isbn*, *sorg:bookEdition* and *sorg:numberOfPages*. Furthermore, even within a single product category, not all instances share the same set of attributes. For example, while *sorg:isbn* is a required attribute for a book, *sorg:bookEdition* (Pr=0.6) and *sorg:numberOfPages* (Pr=0.25) are optional attributes, where Pr indicates the probability that an instance will be generated with that attribute. It must be also noted that some attributes are correlated, which means that either all or none of the correlated attributes will be present in an instance (the *pgroup* construct in the WatDiv dataset description language allows the grouping of such correlated attributes). For a complete list of probabilities, please refer to Tables 3 and 4 in Appendix.

 <table border="1" cellpadding="0" cellspacing="0">
    <caption>
         <a name="table:entities"> 
            Table 2. Entities generated according to WatDiv data description model. Entities marked with an asterisk * do not scale.
         </a>
     </caption>
<thead><tr><th align="left">Entity Type</th><th align="left">Instance Count [per scale factor if applicable]</th></tr></thead> 
<tbody>
<tr valign="top"><td>wsdbm:Purchase</td><td> 1500</td></tr>
<tr valign="top"><td>wsdbm:User</td><td> 1000</td></tr>
<tr valign="top"><td>wsdbm:Offer</td><td>900</td></tr>
<tr valign="top"><td>wsdbm:Topic*</td><td> 250</td></tr>
<tr valign="top"><td>wsdbm:Product</td><td> 250</td></tr>
<tr valign="top"><td>sdbm:City*</td><td> 240</td></tr>
<tr valign="top"><td>wsdbm:SubGenre*</td><td> 21</td></tr>
<tr valign="top"><td>wsdbm:Website</td><td> 50</td></tr>
<tr valign="top"><td>wsdbm:Language</td><td> 25</td></tr>
<tr valign="top"><td>wsdbm:Country*</td><td> 25</td></tr>
<tr valign="top"><td>wsdbm:Genre*</td><td> 21</td></tr>
<tr valign="top"><td>wsdbm:ProductCategory*</td><td> 15</td></tr>
<tr valign="top"><td>wsdbm:Retailer</td><td> 12</td></tr>
<tr valign="top"><td>wsdbm:AgeGroup*</td><td> 9</td></tr>
<tr valign="top"><td>wsdbm:Role*</td><td> 3</td></tr>
<tr valign="top"><td>wsdbm:Gender*</td><td> 2</td></tr>
</tbody>
</table>

In short, the WatDiv test dataset is designed such that

* some entities are more structured (meaning that they contain few optional attributes) while the others are less structured;
* entities are associated in complex ways that mimic the real types of distributions on the Web;
* cardinalities of these associations are varied.

### Description of the Tests

WatDiv generates test workloads that are as diverse as possible. WatDiv offers three use cases:

* __Basic Testing:__ These tests consist of queries in four categories, namely, linear queries (**L**), star queries (**S**), snowflake-shaped queries (**F**) and complex queries (**C**) with a total of 20 query templates. These query templates were randomly selected from a pool of queries generated by performing a random walk on the <a href="https://dsg.uwaterloo.ca/watdiv/watdiv-data-model.txt">dataset description model</a> (which can be represented as a graph), while making sure that (i) the selected queries sufficiently represent each category, (ii) the selectivities of the queries within each category vary, and (iii) in some queries selectivity originates from a single (or few) triple patterns while in the others, it originates as a combination of multiple somewhat less selective triple patterns.

* __Extensions to Basic Testing:__ The following use cases have been developed by <a href="http://dbis.informatik.uni-freiburg.de/team/schaetzle/alexander">Alexander Schätzle</a> from <a href="http://www.uni-freiburg.de/">University of Freiburg</a>.
    * __Incremental Linear Testing:__ This use case is designed to test the performance for linear queries with increasing size (number of triple patterns). In contrast to the linear queries in the Basic Testing use case, the queries in this use case have longer patterns. The workload contains 3 types of queries (IL-1, IL-2, IL-3) which are bound by user, retailer or unbound, respectively. Each query starts with 5 triple patterns and we incrementally add triple patterns to the initial query (up to 10 triple patterns).

    * __Mixed Linear Testing:__ This use case is designed to test the performance for linear queries of different size (number of triple patterns). In contrast to the linear queries in the Basic Testing use case, the queries in this use case have longer patterns. The workload contains 2 types of queries (ML-1, ML-2) which are bound by user or retailer, respectively. The query sizes range between 5 and 10 triple patterns for each type. For example, query ML-1-6 is a user bound query with 6 triple patterns.

* __Stress Testing:__ As described in the <a href="https://doi.org/10.1007/978-3-319-11964-9_13">stress testing paper</a>, this use case offers a much more thorough investigation of systems. To generate query templates, follow the installation procedures.

At this point, you may be wondering how these differentiating aspects of WatDiv affect system evaluation, and why they are important at all. The answer is trivial: by relying on a more diverse dataset as such (which is typical for data on the Web), it is possible to generate test queries that focus on much wider aspects of query evaluation, which cannot be easily captured by other benchmarks. Consider the two SPARQL query templates C3 and S7 (cf., basic testing query templates). C3 is a star query that retrieves certain information about users such as the products they like, their friends and some demographics information. For convenience, for each triple pattern in the query template, we also display its selectivity (the reported selectivities are estimations based on the probability distributions specified in the WatDiv dataset description model). Note that while individually triple patterns in C3 are not that selective, this query as a whole, is very selective. Now, consider S7, which (as a whole) is also very selective, but unlike C3, its selectivity is largely due to only a single triple pattern. It turns out that different systems behave very differently for these queries. Systems like RDF-3x [2], which (i) decompose queries into triple patterns, (ii) find a suitable ordering of the join operations and then (iii) execute the joins in that order, perform very well on queries like S7 because the first triple pattern they execute is very selective. On the other hand, they do not do as well on queries like C3 because the decomposed evaluation produces many irrelevant intermediate tuples. In contrast, gStore [3] treats the star-shaped query as a whole and it can pinpoint the relevant vertices in the RDF graph without performing joins; hence, it is much more efficient in executing C3. For a more detailed discussion of our results, please refer to the technical report [4] and the <a http="https://doi.org/10.1007/978-3-319-11964-9_13">stress testing paper</a>.
-->

### Download the Latest Version

Provided that you include a citation to [1], you are free to download and use the WatDiv Data and Query Generator (v0.6) from [source code](https://dsg.uwaterloo.ca/watdiv/watdiv_v06.tar) (md5sum=9eac247dfdec044d7fa0141ea3ad361f). The software is supplied "as is" and all use is at your own risk.

Executable files are also provided. Source code and executable files of all versions and changelog can be found [here](https://dsg.uwaterloo.ca/watdiv/changelog.shtml).

The datasets used in the experiments in [1], as well as a billion triples dataset are also available for download:

* [10M Triples](https://dsg.uwaterloo.ca/watdiv/watdiv.10M.tar.bz2) 58,558,746 bytes
* [100M Triples](https://dsg.uwaterloo.ca/watdiv/watdiv.100M.tar.bz2) 629,608,436 bytes
* [1B Triples](https://dsg.uwaterloo.ca/watdiv/watdiv.1000M.tar.bz2) 6,502,656,740 bytes

You may also download the <a href="https://dsg.uwaterloo.ca/watdiv/stress-workloads.tar.gz">test workloads</a> used in [1].

## Talks

* G. Aluç, O. Hartig, M. T. Özsu, and K. Daudjee. Diversified stress testing of RDF data management systems ([Video](http://videolectures.net/iswc2014_aluc_rdf_data_management/)). Talk at 13th Int. Semantic Web Conference, Trentino, Italy, 2004.

## Publications

1. G. Aluç, O. Hartig, M. T. Özsu, and K. Daudjee. [Diversified stress testing of RDF data management systems](https://doi.org/10.1007/978-3-319-11964-9_13), In _Proc. 13th Int. Semantic Web Conference_, Part I, pages 197–212, 2014.

2. G. Aluç, M. T. Özsu, and K. Daudjee. [Workload matters: Why RDF databases need a new design](https://dl.acm.org/doi/10.14778/2732951.2732957), _Proc. VLDB Endowment_, 7(10):837–840, 2014.

3. L. Gao, L. Golab, M. T. Özsu, G. Aluç. [Stream WatDiv: A Streaming RDF Benchmark](https://dl.acm.org/doi/10.1145/3208352.3208355), In _Proc. International Workshop on Semantic Big Data_, pages 1-6, 2018.

## Artifacts

See the [Description](Description.md) document.

## People

[Güneş Aluç](https://www.linkedin.com/in/gunes-aluc-66588a221/) -- contact for all questions/bug reports galuc-red-@-blue-uwaterloo.ca (without the colors/hypens)

[M. Tamer Özsu](https://cs.uwaterloo.ca/~tozsu/)

[Khuzaima Daudjee](https://cs.uwaterloo.ca/~kdaudjee/)

[Olaf Hartig](http://olafhartig.de)

[Lukasz Golab](http://www.engineering.uwaterloo.ca/~lgolab/)

[Libo Gao](https://www.linkedin.com/in/libo-gao/) 
