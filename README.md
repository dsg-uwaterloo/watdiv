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

Using these features,  the WatDiv test dataset is designed (see the associated dataset description model). By executing the data generator with different scale factors, it is possible to generate test datasets with different sizes. Table 1 lists the properties of the dataset at scale factor=1.

<table>
     <caption>
         <a name="table:triples"> 
            Table 1. Characteristics of the WatDiv test dataset at scale factor=1.
         </a>
     </caption>
     <tr>
         <th></th>
         <th>scale factor=1</th>
     </tr>
     <tr>
        <td>
            <i>triples</i>
        </td>
        <td>105257</td>
    </tr>
    <tr>
        <td>
            <i>distinct subjects</i>
        </td>
        <td>5597</td>
    </tr>
    <tr>
        <td>
            <i>distinct predicates</i>
        </td>
        <td>85</td>
    </tr>
    <tr>
         <td>
            <i>distinct objects</i>
         </td>
         <td>13258</td>
    </tr>
    <tr>
        <td>
            <i>URIs</i>
        </td>
        <td>5947</td>
    </tr>
    <tr>
        <td>
            <i>literals</i>
        </td>
        <td>14286</td>
    </tr>
    <tr>
        <td>
            <i>distinct literals</i>
        </td>
        <td>8018</td>
    </tr>
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
