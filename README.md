# Final Project for EE283: Orthologue finder and NCBI searcher for ENSEMBL ID Gene Lists

This python program is an improvement off of the Final Project submitted for EcoEvo 282, shown here: [EE282 Final Project](https://github.com/pnayak93/ee282/blob/main/Final_Project_Writeup.md)

The EE282 final project consisted of a python script which took gene list outputs from a NGS experiment as input (either in ENSEMBL ID format or Conventional Gene name format) and returned the number of articles written on pubmed for each gene plus a user-inputted search term. For example, if the user input the search term "tendon development" or "ribosomal RNA", this would be searched with each gene in the user input gene list on the Pubmed API. Please see the EE282 writeup for more information.

For the EE283 final project, I decided to take the EE282 final project one step further by finding all orthologous genes in different species for every gene in the gene list, converting the ENSEMBL IDs into conventional gene names, and then performing the search against the Pubmed database via the [Pubmed API](https://www.ncbi.nlm.nih.gov/books/NBK25501/) for each gene and ortholog with the user inputted search terms.

The script has been converted into a command line program, called orthologue-finder-with-database.py, using the argparse python module, and takes 3 arguments as input:   

1) The file name of the excel file containing the input gene list in ENSEMBL ID format. The excel file should be formatted as shown in the following screenshot (Additional examples of output can be seen in the Sample Input Folder on this Github Repository):

![INSERT SCREENSHOT ]()

2) The search term(s) you wish to search with each gene against the Pubmed API/Pubmed Research Database

3) The desired name of your output excel file, e.g. "output-file.xlsx"

Additionally, the program currently requires that you have downloaded the "ensembl_gene_lists" folder (and all files within), as well as the "orthologous_gene_lists" folder (and all files within). After entering the arguments for the program, it will ask for the paths to these folders, and the path to the parent folder containing your input file as well. Once these have all been input, the program should run normally, and output a file similar to the following screenshot (Additional examples of output can be seen in the Sample Output Folder on this Github Repository):

![INSERT SCREENSHOT]()

The reason that these files are needed locally are because the program reads off of the correct orthologous gene list (downloaded off of [Biomart](https://www.ensembl.org/biomart/martview/a2d7e8d51d4d452d497f784ce4a5be89) to find all orthologous for each gene in the user-input gene list, and uses the correct ensembl gene list to translate ENSEMBL IDs into conventional gene names for proper searching against the Pubmed API. In the EE282 final project script, the ENSEMBL ID translation was done via the [ENSEMBL REST API](https://rest.ensembl.org/). This was originally considered for the first iteration for this project, but I found that when you added hundreds or thousands of genes (especially when adding in orthologous genes for multiple species), the API would restrict the sheer number of API calls coming from the program (1x GET request per ENSEMBL ID), drastically slowing down the run time, or crashing the program entirely. The functions for the ENSEMBL API calls are still included within the program, although they are not being used currently, since local files are used instead. If interested, the functions for these calls are the "homolog_finder" and "multi_species_homfinder" functions for finding homologs/orthologous genes for one ENSEMBL ID for one species, and the "ens_id_finder" function for translating ENSEMBL IDs to conventional gene name.  The temporary solution was to create a local data storage/dictionary of sorts in the form of text files. A future improvement would be to only include API calls to the ENSEMBL REST API when the ENSEMBL id was not found in the 

