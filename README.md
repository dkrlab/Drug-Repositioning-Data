# Heter-LP

Codes are written by C# in visual studio 2015.

Data are provided as below: 

Our suggested heterogeneous network for drug repositioning is consists of three sub-networks, drugs, diseases, and targets and their relations.So, six separate matrices are required: (1) drug similarities, (2) disease similarities, (3) targets similarities, (4) drug-disease relations, (5) disease-target relations and (6) drug-disease relations. The data used for each one is explained in the following sections. 

(1) Drug similarities

We used three different similarities for drugs: Chemical substructures similarities, Side effect similarities, Anatomical Therapeutic Chemical (ATC) code similarities.

•	In this study, one of the similarity criteria between the two drugs is the similarity of their two-dimensional chemical structure. A basic premise in drug sciences is that drugs with the same chemical structure have similar therapeutic functions . To investigate this similarity, we have used a fingerprint descriptor of PubChem. In this descriptor, a binary prescriptive drug (zero means no existence/ one means existence). In the descriptor, 888 different drugs and 881 chemical infrastructures have been presented. So in fact, we have a binary matrix with 888 rows and 881 columns. This matrix is accessible via  . On the PubChem website, these 881 chemical infrastructures are described completely. To calculate the chemical similarity between each pair of drugs based on this matrix, we used the Jaccard similarity measure implemented in the “PROXY” package  provided in R.

•	By investigating information on the adverse effects of drugs, researchers have discovered new relationships among drugs that have not been detectable by examining chemical structures and therapeutic effects. In the research carried out by combining chemical structures and side effects, the accuracy of predictions has increased dramatically and some relations is predicted that have not been made by examining chemical structures alone. In virtually all of the studies that have been used to determine the side effects of drugs in drug-drug-related research, SIDER has been introduced as a major source. SIDER is an online database that maintains relations between the side effects of drugs and adapts this information through the text-mining methods. The file downloaded from this site is a fingerprint matrix (similar to that described in the similarity of the chemical infrastructure) which has 888 drugs (rows) and 1385 different side effects (columns). We obtained this matrix with the help of the "PROXY" package in R as a matrix of similarity between the 888 drugs.

•	Researchers in the pharmaceutical sciences have classified drugs to organize them. This classification is based on the mechanism of action, metabolism, chemical structures, and so on. In this regard, different types of classifications for different purposes are provided. One of the most important of these classifications is ATC. ATC is a clinical classification system developed and supported by the WHO . This classification is used as a research resource on how drugs should be prescribed to enhance the quality of drug using. This system has a hierarchical structure with five different levels . 
There are various data sources that provide ATC codes for drugs, including the most important and most widely used DrugBank  and KEGG . We received the latest available version (on September 2016) from the KEGG website. These data were rearranged in the form of a fingerprint matrix by "reshape2" package  in R and finally computed the similarity matrix with the help of the "PROXY" package in R.

(2) Disease similarities

We used four different similarities for diseases: Phenotype semantic similarities of OMIM , Disease genes similarities, similarity based on ICD-10  classification, semantic similarity based on DO .

•	OMIM is a human disease information database. MimMiner   categorizes human phenotypes in this database by using text mining methods . These phenotypic similarities are accessible through the MimMiner website. These similarities are presented in the form of a matrix, in which the factors presented in the rows and columns are all human-type diseases, with 4784 rows and 4784 columns. Each entry of it represents the semantic similarity between the two diseases, which is calculated based on the frequency of MeSH  repeats in each pair of diseases in the OMIM medical literatures. In other words, each row or column of this matrix is a semantic similarity profile for a disease.

•	DisGeNET  is one of the largest and most comprehensive information resources on human genetic diseases. It also provides a suite of bioinformatics tools to facilitate analysis of these data. The database has provided more than 500,000 links between more than 17,000 genes and more than 20,000 human and animal diseases. DisGeNET's emphasis is on data integration, standardization and accurate tracking of information. In addition to integrating data from various information sources, the database is very helpful in providing the required information in various formats, so that, with the help of graph display tools like Cytoscape, relations between disease and genes could be presented as bipartite graphs. Also, the information available in DisGeNET is expanded and completed using semantic web technologies and it is linked to various sources are currently available in the LOD Cloud. We have received a list of diseases that have common genes by running an SPARQL Query (on December 2016) on the DisGeNet website. Then by using of "reshape2" and "PROXY" packages converted them to fingerprint matrix and Jaccard's similarity matrix. This similarity matrix contains the similarity of 3321 diseases and various genetic damages.

•	ICD-10 is the tenth edition of the International Statistical Classification of Diseases and Health Problems (ICDs), presented by the World Health Organization (WHO). This classification includes illness codes, signs and symptoms, abnormal findings, social conditions, and external causes of injury or illness. Of course, in some countries, according to the needs of that community, there have been changes, but most countries prefer to use its global accepted version. The purpose of the ICD is to provide the ability to record, analyze, interpret and compare disease data in different countries or regions at different times. In fact, the ICD can be used to rename and characterize illnesses from words to an alphabetical and numerical code, thus facilitating storage, retrieval and analysis. 
KEGG website has provided 1508 diseases at three levels (A to C) based on ICD-10 classification (on September 2016). Using the C-level division, we transform the relationships between diseases into the form of a fingerprint matrix, and then we calculated the similarity matrix (Jaccard's similarity) (by using of "reshape2" and "PROXY" in R). The similarity matrix of this section shows the relationship between 1366 diseases.

•	DO  is a standard ontology for human diseases that has developed their phenotypic characteristics in order to provide consistent, reusable and sustainable descriptions of human disease conditions. In this ontology, a semantic combination of diseases has been developed based on OMIM, ICD, MeSH and SNOMED concepts. Various tools and methods have been proposed to calculate the semantic similarity between different factors. Of these, we chose the DOSE  package to calculate the semantic similarity between diseases and genes and proteins based on DO.

(3) Targets similarities

We used four different similarities for protein targets: semantic similarities based on GO , semantic similarities based on HPO , semantic similarities based on DO, similarities based on KEGG classification.

•	GO is an ontology that aims to define the concepts and classes used to describe the function of genes and proteins and the relationships between these concepts. In this ontology, based on the genetic functions, each concepts belongs to one of these categories: Molecular function, Cellular component, Biological process.
To estimate the functional similarities between the two proteins, we used the semantic similarity between the GO concepts, computed by GOSemSim package provided in R . Finally, a similarity matrix was obtained for 1550 protein targets.

•	HPO aims to provide a standard vocabulary for phenotypic disorders caused by human diseases. Each term in the HPO describes a phenotypic disorder. There are tools for calculating the similarity between drug targets based on this ontology. In this regard, we used the HPOSim package in R . In this package, there are six different methods for calculating the similarity that we used Resnik method. Finally, we get a similarity matrix for 979 protein targets.

•	It is possible to calculate the similarity between protein targets (based on the diseases that are associated with these proteins and their related genes) with the help of the DOSE package (presented in diseases similarity section). Finally, we obtain a similarity matrix contains 1092 protein targets.

•	KEGG provides general groups of proteins in separate files and defines subgroups for each group. we categorize the proteins according to the subgroups of the second level (the more detailed level) and with the help of "reshape2" and "PROXY" packages in R computed the similarity between 1132 proteins.

(4) Drug-disease relations

We used two data sources, TTD  and KEGG, for the relationship between drugs and disease.

•	TTD  is a database for providing information about well-known and ongoing drug targets. In this database, the nucleic acid targets, the diseases, the relevant biological pathways and the drugs related to each of these targets and diseases are also examined. In this database there are links to databases containing the functional information of the targets, their sequences, the three-dimensional structure, ligand binding properties, enzymes and drugs structure, clinical development status, and so on.
We received drug relations and their therapeutic effects based on the latest version of TTD (5.1.01). After a brief preprocessing to remove unnecessary data from this file (such as subtypes of treatment or specific TTD’s identifiers), we obtained a list of medications and therapeutic effects. Then we transformed this list to matrix form using the "reshape2" package in R.

•	Based on various sources of information, KEGG has collected a variety of diseases in a file (the sources used for each disease are individually identified in this file). For each disease, an identifier, the name of the disease, an explanation of the disease, the group and subtypes of the disease, its related pathways, the related genes involved in the disease, and the drugs associated with that disease are presented in this flat file. We put the name of the disease, together with all the drugs related to them, into a list, and then we turned it into matrix using the "reshape2" package in R.

(5) Disease-target relations

We used two data sources, KEGG and DiGeNet, for the relationship between disease and target.

•	The KEGG database in a flat file provides diseases along with their related genes and related genetic products. We downloaded this file on September 2016 and turned it into matrix form with the help of mentioned R packages.

•	We received the list of diseases, genes, and related genetic products from DisGeNet  by running a SPARQL Query (on December 2016. Then it was turned into matrix form with the help of R.

(6) Drug-target relations

One of the main issues in the design and production of drugs is the interactions between drugs and targets. Drugs that have common target proteins usually have the same therapeutic function. It is often assumed that drugs that interact with the same targets can be used to treat similar diseases . We used two data sources, KEGG and DrugBank, for the relationship between drugs and targets.

•	KEGG is an important source for supplying information about drugs and their targets. In this database, there is a flat file of drugs classified based on their targets. Target proteins are presented at five levels (from general to partial); at levels of one to four groups and subgroups of protein, and at the fifth level, the target protein has been identified. We turn it into a matrix form based on the most detailed level (which exactly specifies a particular protein) with the help of R packages.

•	DrugBank is one of the most important databases on the drugs and target proteins. In addition to availability of search option based on drug and target, there are downloadable files of drugs, targets and their relation in DrugBank website. We received drug-target relation list in December 2016 and turned it into matrix form with the help of R packages.
