# self-regulation-dataset
This repository contains html files from mriqc directory of "https://openneuro.org/datasets/ds004636/versions/1.0.4". 
We developed a webpage that makes cross-comparison between mriqc failed and passed trials's scan visualizations easier.
We create a software pipeline for data visualization and analysis. 

Pipeline of code execution:

1. manually downloaded suggested_exclusions.csv from dataset website

2. download_data.ipynb
    * create mriqc_passed and mriqc_failed directories and txt files using suggested exclusions csv
    * code get_file_html_name function that takes {subject}_{task} input and converts it to the appropriate html name to use as parameter with datalad get method
    * use datalad methods (clone and get) to get all suggested excluded data (both all mriqc failed and all mriqc passed)
        - datalad clone "https://openneuro.org/datasets/ds004636/versions/1.0.4" creates the directory "ds004636" which includes all the metadata
        - datalad get (in code) acquires the specified data information
        
        SIDE NOTES: 
        - I first acquired all the data in another repository. When you do datalad_clone, too many directories are created, that you don't really need. So I transferred all the important BOLD files to this repository manually. 
        - When we clone something from datalad, you can't work with that repository to github because it saves the real data as an embedded link (because the size is too large), and you open ds004636 (dataset) on github because it is an embedded link if previously cloned from a datalad url. 
        - Therefore, whenever I need to acquire more files from datalad, I have another repository (that has the same code with download_data). I run it there, and manually copy the html files downloaded to self-regulation-dataset (our current repository) 

3. After acquiring all the necessary files, wrote the html & javascript in index.html (which is the MRIQC Report Viewer Webpage).
    * Index.html takes in data from mriqc_failed and mriqc_passed text files, creates and populates two dropdown buttons with file names, points to the path of these files once "Go!" is clicked. 

4. Independent of the index.html webpage: Quality_metrics.ipynb contains code for visualization. 

