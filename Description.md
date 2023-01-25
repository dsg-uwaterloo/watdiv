# WatDiv


## Benchmark Details

### Description of the Dataset

The WatDiv data generator allows users to define their own dataset through a dataset description language (see tutorial). This way, users can control

* which entities to include in their dataset,
* how "well-structured" each entity is (for details please refer to a research paper by Dunn et all [<a href="#ref:Dunn">1],
* how different entities are associated,
* the probability that an entity of type X is associated with an entity of type Y, and
* the cardinality of such associations.

Using these features,  the WatDiv test dataset is designed (see the associated [dataset description model](watdiv-data-model.txt)). By executing the data generator with different scale factors, it is possible to generate test datasets with different sizes. <a href="#table:triples">Table 1</a> lists the properties of the dataset at scale factor=1.

<table border="1" cellpadding="0" cellspacing="0">
    <caption>
         <a name="table:triples"> 
            Table 1. Characteristics of the WatDiv test dataset at scale factor=1.
         </a>
     </caption>
<!---   <thead><tr><th align="left">Column 1</th><th align="right">#</th></tr></thead> -->
<tbody>
<tr valign="top"><td><i>triples</i></td><td> 105257</td></tr>
<tr valign="top"><td><i>distinct subjects</i></td><td> 5597</td></tr>
<tr valign="top"><td><i>distinct predicates</i></td><td> 85</td></tr>
<tr valign="top"><td><i>distinct objects</i></td><td> 13258</td></tr>
<tr valign="top"><td><i>URIs</i></td><td> 5947</td></tr>
<tr valign="top"><td><i>literals</i></td><td> 14286</td></tr>
<tr valign="top"><td><i>distinct literals</i></td><td> 8018</td></tr>
</tbody>
<!---<tfoot><tr valign="top"><td align="right">Sum:</td><td align="right">1,234,569</td></tr>
</tfoot>-->
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
<!---<tfoot><tr valign="top"><td align="right">Sum:</td><td align="right">1,234,569</td></tr>
</tfoot>-->
</table>

In short, the WatDiv test dataset is designed such that

* some entities are more structured (meaning that they contain few optional attributes) while the others are less structured;
* entities are associated in complex ways that mimic the real types of distributions on the Web;
* cardinalities of these associations are varied.

### Description of the Tests

WatDiv generates test workloads that are as diverse as possible. WatDiv offers three use cases:

* __Basic Testing:__ These tests consist of queries in four categories, namely, linear queries (**L**), star queries (**S**), snowflake-shaped queries (**F**) and complex queries (**C**) with a total of 20 query templates. These query templates were randomly selected from a pool of queries generated by performing a random walk on the [dataset description model](https://dsg.uwaterloo.ca/watdiv/watdiv-data-model.txt) (which can be represented as a graph), while making sure that (i) the selected queries sufficiently represent each category, (ii) the selectivities of the queries within each category vary, and (iii) in some queries selectivity originates from a single (or few) triple patterns while in the others, it originates as a combination of multiple somewhat less selective triple patterns.

* __Extensions to Basic Testing:__ The following use cases have been developed by [Alexander Schätzle](http://dbis.informatik.uni-freiburg.de/team/schaetzle/alexander) from [University of Freiburg](http://www.uni-freiburg.de).
    * __Incremental Linear Testing:__ This use case is designed to test the performance for linear queries with increasing size (number of triple patterns). In contrast to the linear queries in the Basic Testing use case, the queries in this use case have longer patterns. The workload contains 3 types of queries (IL-1, IL-2, IL-3) which are bound by user, retailer or unbound, respectively. Each query starts with 5 triple patterns and we incrementally add triple patterns to the initial query (up to 10 triple patterns).

    * __Mixed Linear Testing:__ This use case is designed to test the performance for linear queries of different size (number of triple patterns). In contrast to the linear queries in the Basic Testing use case, the queries in this use case have longer patterns. The workload contains 2 types of queries (ML-1, ML-2) which are bound by user or retailer, respectively. The query sizes range between 5 and 10 triple patterns for each type. For example, query ML-1-6 is a user bound query with 6 triple patterns.

* __Stress Testing:__ As described in the [stress testing paper](https://doi.org/10.1007/978-3-319-11964-9_13), this use case offers a much more thorough investigation of systems. To generate query templates, follow the installation procedures.

At this point, you may be wondering how these differentiating aspects of WatDiv affect system evaluation, and why they are important at all. The answer is trivial: by relying on a more diverse dataset as such (which is typical for data on the Web), it is possible to generate test queries that focus on much wider aspects of query evaluation, which cannot be easily captured by other benchmarks. Consider the two SPARQL query templates C3 and S7 (cf., basic testing query templates). C3 is a star query that retrieves certain information about users such as the products they like, their friends and some demographics information. For convenience, for each triple pattern in the query template, we also display its selectivity (the reported selectivities are estimations based on the probability distributions specified in the WatDiv dataset description model). Note that while individually triple patterns in C3 are not that selective, this query as a whole, is very selective. Now, consider S7, which (as a whole) is also very selective, but unlike C3, its selectivity is largely due to only a single triple pattern. It turns out that different systems behave very differently for these queries. Systems like RDF-3x [<a href="#ref:Neumann">2], which (i) decompose queries into triple patterns, (ii) find a suitable ordering of the join operations and then (iii) execute the joins in that order, perform very well on queries like S7 because the first triple pattern they execute is very selective. On the other hand, they do not do as well on queries like C3 because the decomposed evaluation produces many irrelevant intermediate tuples. In contrast, gStore [<a href="#ref:Zou">3] treats the star-shaped query as a whole and it can pinpoint the relevant vertices in the RDF graph without performing joins; hence, it is much more efficient in executing C3. For a more detailed discussion of our results, please refer to the technical report [<a href="#ref:Aluc">4] and the [stress testing paper](https://doi.org/10.1007/978-3-319-11964-9_13).

### Installing WatDiv Data, Query and Query Template Generator

Compiling WatDiv (in C++) is straightforward -- the only dependencies are the [Boost libraries](http://www.boost.org/) and the Unix words file (i.e., make sure you have a [wordlist package](http://packages.ubuntu.com/trusty/wordlist) installed under /usr/share/dict/). Once you have installed Boost, simply execute the following commands on UNIX:

```
tar xvf watdiv_v05.tar
cd watdiv
setenv BOOST_HOME <BOOST-INSTALLATION-DIRECTORY>
export BOOST_HOME=<BOOST-INSTALLATION-DIRECTORY> (in bash)
make
cd bin/Release
```

The last step above is important. To run the data generator, issue the following command:
```
./watdiv -d <model-file> <scale-factor>
```

You will find a model file in the model sub-directory where WatDiv was installed. Using a scale factor of 1 will generate approximately 100K triples. For a more detailed description of the dataset that will be generated, please refer to <a href="#table:triples">Table 1</a>. This will print the generated RDF triples on the standard output while producing a file named `saved.txt` in the same directory. The following steps depend on this file, therefore, keep it safe.

To run the query generator, issue the following command:
```
./watdiv -q <model-file> <query-file> <query-count> <recurrence-factor>
```
Use the same model file in the model sub-directory where WatDiv was installed. You will find the [basic testing query templates](https://dsg.uwaterloo.ca/watdiv/basic-testing.shtml) in the testsuite sub-directory where WatDiv was installed.

To generate more query templates for stress testing (cf., [stress testing paper](https://cs.uwaterloo.ca/~galuc/watdiv/paper/)), use the _query template generator_.
```
./watdiv -s <model-file> <dataset-file> <max-query-size> <query-count>
```
In the latest version, you may specify (i) the number of bound patterns in the query (default=1) as well as (ii) whether join vertices can be constants or not (default=false). To use these features, execute watdiv with the following signature instead.
```
./watdiv -s <model-file> <dataset-file> <max-query-size> <query-count> <constant-per-query-count> <constant-join-vertex-allowed?>
```

### References

[<a name="ref:Duan">1] S. Duan, A. Kementsietsidis, K. Srinivas, and O. Udrea. Apples and oranges: a comparison of RDF benchmarks and real RDF datasets. In *Proc. ACM SIGMOD Int. Conf. on Management of Data*, 2011, pages 145-156.

[<a name="ref:Neumann">2] T. Neumann and G. Weikum. The RDF-3X engine for scalable management of RDF data. VLDB J., 19(1): 91-113, 2010.

[<a name="ref:Zou">3] L. Zou, J. Mo, D. Zhao, L. Chen, and M. T. Özsu. gStore: Answering SPARQL queries via subgraph matching. Proc. VLDB Endow., 4(1): 482-493, 2011.

[<a name="ref:Aluc">4] G. Aluç, M. T. Özsu, K. Daudjee, and O. Hartig. <a href="https://cs.uwaterloo.ca/~galuc/chameleon-db/">chameleon-db: a workload-aware robust RDF data management system</a>. Technical Report CS-2013-10, University of Waterloo, 2013.