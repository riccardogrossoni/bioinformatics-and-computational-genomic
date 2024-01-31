We now have a huge amount of datasets available, which are in continuous growth. We need a way to "make sense" of massive data sets. Bio terminologies and ontologies have an important role for this problem. There are several being developed and used to:
- Define, describe and identify information
- Favor information management and analysis with:
	- Integration of sparse and heterogeneous info
	- Identification and grouping of similar bio sequences
	- Statistical analysis and data mining of controlled annotations to:
		- Highlight most relevant biological features
		- Help unveiling knowledge from data
- Support translational research (to quickly bring in the clinical practice new biomolecular knowledge)
## Bio-terminologies
We define bio-terminologies as the collections of terms which are precise and comprehensible that univocally define and identify different concepts. They are useful for knowledge sharing and analysis, are defined and maintained by experts and can be applied to various fields such as:
- Biochemical and metabolic pathways (KEGG)
- Protein families and domains (Pfam)
- Genetic diseases (OMIM)
- Biological processes, molecular functions and cellular components (Gene Ontology)
They are also very useful for enhancing gene lists with bioinformation.
## Semantic networks
Logical structures used to represent knowledge
- **nodes**: represent concepts
- **arches**: represent relationships between concepts (and the knowledge)
It's also a reasoning tool that can be used to infer new knowledge
There are 2 main connections:
![[Connections_semantic_networks.png]]
We can use the transitive propriety to infer new knowledge:
![[semantic_networks_inferred_knowledge.png]]
## Bio ontologies
Ontology development is fragmented, there are several communities creating and maintaining different ontologies with different models and it's Difficult to relate different annotation repositories to each other. For this reasons open ontology development and data annotation tools are being developed by the NCBO (national center of biomedical ontology). The **NCBO** founded **OBO**, which is a platform to aggregate and "translate" the different ontologies. 
To be part of OBO an ontology must:
- be open and accessible to everyone without constrain and the origin must be recognized. Subsequent modifications must be distributed under different names and identifiers.
- Expressed in a common and shared syntax (OBO syntax, its extension, or in OWL (Web Ontology Language)): in order to ease use of the same tools and shared implementation of software applications.
- Clearly specified and with a well defined content: each ontology must be orthogonal to the other OBO ontologies.
- Not overlapping other OBO ontologies: partial overlapping can be allowed in order to enable combination of ontology terms to form new terms.
- Able to include textual definitions of all terms: since several biomedical terms can be ambiguous, the concepts they represent must be precisely defined with their meaning within the specific ontology domain they refer (which must be also specified).
- Finally it must be well documented.
There are various recognized OBO ontologies now:
- **SO**: sequence ontology, focuses on features and proprieties of nucleic acid sequences
- **ChEBI**: Chemical Entities of Biological Interest is the Ontology of “small molecular entities" which are products of nature or synthetic products used to intervene in the processes of living organisms.
- **GO**: see [[Gene Ontology]] 

## Annotations
An annotation is the association between a gene (or gene product) to a biomedical or biomolecular concept. Each gene is associated with multiple concepts (has more features). Each concept category is assigned to many genes (many genes (gene products) have same features). These annotations can be human curated or predicted automatically by machines (with or without human supervision).
Ontological annotations must be assigned by associating genes (or gene products) with the most specific terms describing their features.


