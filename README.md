# S2C2

S2C2 software is a graphical tool for robust prediction of continuous intracellular signal transduction from single-cell or spatial transcriptomics data. 

S2C2 GUI is Java-based, ensuring cross-platform compatibility across Windows, macOS, and Linux, with built-in visualization capabilities. The CLI version is designed for cloud server environments, while the R script provides a fast and efficient option tailored for bioinformaticians working with single-cell and spatial transcriptomics (ST) data in R. These options makes S2C2 a versatile solution for users on various operating systems.

Parallel computing is supported by S2C2, allowing multiple calculations for selected cell type pairs to be executed efficiently. A detailed tutorial, accessible through the provided GitHub link (available upon request), has been created with instructions for installing S2C2 on Windows, macOS, and Linux. System requirements have been outlined, recommending at least 8GB of RAM, with 16GB preferable for handling large-scale single-cell and ST data, as well as a multi-core processor with at least 2.5 GHz per core. For processing multiple cell-cell crosstalk pairs, four or more cores are advised to significantly enhance performance.


# S2C2 software screenshot
![Alt text](https://github.com/methodistsmab/S2C2/blob/main/screenshots/overview.png)

![Alt text](https://github.com/methodistsmab/S2C2/blob/main/screenshots/highlight.png)

# How to use S2C2 GUI software
Decompress the package **S2C2_v1.zip**

Please read the S2C2 user guide to use it.
[S2C2 user guide](https://github.com/methodistsmab/S2C2/blob/main/S2C2-user-guide.pdf)

# How to use CLI version
Decompress the package **CLI_package_v1.zip**

Command Usage:
```
Rscript --max-ppsize=500000 sCCCExplorer_command.R 
         [Output log file]
         [Input ipf file (.rds)]
         [Cell type]
         [Disease condition name]
         [Phenotype 1]
         [Phenotype 2]
         [Cell type list of sender]
         [Cell type list of receiver]
         [Percent express]
         [Logfc threshold]
         [Intermediate downstream gene number]
         [Permutation number]
         [lambda]
         [species - "mouse" or "human"]  
         [assay - "RNA" or "integrated"] 
         [output data folder]

```

Command Example:
```
Rscript --max-ppsize=500000 sCCCExplorer_command.R log_report.dat /your_data_folder/input_ipf.rds cell_type_Jan2524 Diagnosis Control NA sender.txt receiver.txt 0.005 0.20 2 1000 0.0 mouse RNA output_folder

```

# Sample data format

The input data format looks like the figure below. Your data should include the highlight data items.
For the details explanation, you can check the user guide.
![Alt text](https://github.com/methodistsmab/S2C2/blob/main/screenshots/data_format.png)

# Contact and Support

### Principal Investigator
>Wong, Stephen 

>Email: STWong@houstonmethodist.org
>
### Algorithms Support
>Jianting Sheng

>Email: jsheng@houstonmethodist.org

>Ahn, Ju young 

>Email: jahn@houstonmethodist.org

### Software Support
>Zhihao Wan

>Email: zwan@houstonmethodist.org

>Xiaohui Yu

>Email: xyu2@houstonmethodist.org


# Department of System Medicine and Bioengineering 

[DEPARTMENT OF SYSTEMS MEDICINE & BIOENGINEERING ](https://www.houstonmethodist.org/for-health-professionals/department-programs/systems-medicine-bioengineering-smab/)
