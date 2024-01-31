is the ontology for attributes of gene products in all organisms. Is the result of a collaborative effort to address the need for consistent and species independent descriptions of gene and protein features in distinct biomolecular databanks (e.g. gene involved in protein synthesis vs. translation).
Is the moist developed bio ontology to describe gene and protein features, it Provides 3 controlled terminologies (terms, or categories, + relationships) to describe biological characteristics of genes and proteins (biological processes, molecular functions, cellular components). It has a directed Acyclic graph (DAG) structure (see [[Biological networks]] and [[Network recap]] for more info on DAG). Lower levels indicate generality, upper levels specialization of the represented concept. 
Each concept has these info associated:
- ID: unique and required
- Name: unique and required
- Definition: optional but soon will be required, unique
- Synonyms: optional, multiple
- Reference databases: optional, multiple
- Relationships: "IS_A" or "PART_OF" or the newly added "REGULATES"

## Annotations in GO
When a gene or gene product is annotated to a term it is implicitly annotated also to the parent terms. This is called True path rule.
Evidence (quality) codes exist for each annotation:
- automatically assigned evidence code (IEA) is based on automatic computation and is the lowest quality
- Experimental (EXP): inferred from experiment
- Computational analysis (e.g. ISA aka Inferred from Sequence Alignment)
- Author statement: (e.g. TAS: Traceable Author Statement)
- Curatorial statement: (e.g. IC: Inferred by Curator)
We can expand each category into multiple tags for more specific referencing.
![[ALL_GO_annotations.png]]