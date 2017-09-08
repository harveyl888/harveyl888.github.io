---
layout: article
title: "KEGG and neo4j"
excerpt: "Importing the KEGG database into neo4j"
categories: blog
created: 2017-09-08
comments: false
share: false
ads: false
---

The KEGG (Kyoto Encyclopedia of Genes and Genomes) database is a useful reference of biochemical pathways often employed in metabolomics and proteomics studies.  Various tables from the database can be downloaded in flat file format via ftp (ftp://ftp.pathway.jp/kegg) and, although this provides a useful interface to query properties, the real interest in pathways is in their connectivity.  

Two KEGG tables are of interest, namely the *compound* and *rclass* tables.  The *compound* table contains information on the compounds themselves including an id tag (ENTRY), molecular properties and pathways on which they can be found.  When constructing a network the compounds are the nodes.  The *rclass* table contains information on different reaction classes including an id tag (ENTRY), definition of the reaction class, pathways on which it can be found and a series of pairs of compounds which undergo the reaction (substrate and product pairs).  These reactions are the relationships in the network.

It's relatively straightforward to create a neo4j database from these pieces of information.  First the rclass and compound files are read and relevant data are extracted.  Then each of the reactions are populated with properties taken from rclass and compound data.  Finally the database is populated using transactions - a method by which multiple cypher statements can be executed in a single server transaction.

The command used to populate the database is simply:
```
"MERGE (c1:Compound{properties}) MERGE (c2:Compound{properties}) CREATE (c1)-[:REACTION{properties}]->(c2)"
```
where *properties* refer to the properties associated with nodes and relations (in JSON notation).

To run this within a transaction it's:
```python
tx = graph.begin()
for t in triples:
   mergeText = "MERGE (c1:Compound{properties}) MERGE (c2:Compound{properties}) CREATE (c1)-[:REACTION{properties}]->(c2)"
   tx.append(mergeText)
tx.commit()
```
replacing the *properies* with properties of each reaction.


