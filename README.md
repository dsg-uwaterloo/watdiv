# WatDiv


## Waterloo SPARQL Diversity Test Suite

WatDiv is a benchmark designed to measure how an RDF data management system performs across a wide spectrum of SPARQL queries with varying structural characteristics and selectivity classes.

WatDiv consists of two components: the data generator and the query (and template) generator.

### Description of the Dataset

The WatDiv data generator allows users to define their own dataset through a dataset description language (see tutorial). This way, users can control

* which entities to include in their dataset,
* how "well-structured" each entity is (for details please refer to a research paper by Duan et al. [1]),
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
<!---	<thead><tr><th align="left">Column 1</th><th align="right">#</th></tr></thead> -->
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
<thead><tr><th align="left">Entity Type</th><th align="left">Instance Count [per scale factor if applicable]</th></tr></thead> -->
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

## Talks

* G. Aluç, O. Hartig, M. T. Özsu, and K. Daudjee. Diversified stress testing of RDF data management systems ([Video](http://videolectures.net/iswc2014_aluc_rdf_data_management/)). Talk at 13th Int. Semantic Web Conference, Trentino, Italy, 2004.

## Publications

* G. Aluç, O. Hartig, M. T. Özsu, and K. Daudjee. Diversified stress testing of RDF data management systems, In _Proc. 13th Int. Semantic Web Conference_, Part I, pages 197–212, 2014.

* G. Aluç, M. T. Özsu, and K. Daudjee. Workload matters: Why RDF databases need a new design, _Proc. VLDB Endowment_, 7(10):837–840, 2014.

* L. Gao, L. Golab, M. T. Özsu, G. Aluç. Stream WatDiv: A Streaming RDF Benchmark, In _Proc. International Workshop on Semantic Big Data_, pages 1-6, 2018.

## Artifacts

## People

[Güneş Aluç](https://www.linkedin.com/in/gunes-aluc-66588a221/) 

[M. Tamer Özsu](https://cs.uwaterloo.ca/~tozsu/)

[Khuzaima Daudjee](https://cs.uwaterloo.ca/~kdaudjee/)

[Olaf Hartig](http://olafhartig.de)

[Lukasz Golab](http://www.engineering.uwaterloo.ca/~lgolab/)

[Libo Gao](https://www.linkedin.com/in/libo-gao/) 
