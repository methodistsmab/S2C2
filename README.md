# S2C2: Single-Cell Cross Communication Explorer
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![R](https://img.shields.io/badge/R-4.3.1+-blue.svg)](https://www.r-project.org/)
[![Python](https://img.shields.io/badge/Python-3.8+-green.svg)](https://www.python.org/)
[![Ollama](https://img.shields.io/badge/Ollama-Local%20LLM-orange.svg)](https://ollama.ai/)
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


## ⚡ Usage

### 1. Load your RDS data
```bash
RScript loadRDS.R 
```

This creates:
- `/temp/celltype.json` - Available cell types
- `/temp/metadata.json` - Dataset metadata
- `/temp/all_celltype.txt` - Cell type list

Choose the `celltype` and `condition` from temp

#### Create Cell Type Files
```bash
# Create sender.txt
echo "Astrocyte" > sender.txt

# Create receiver.txt  
echo "Excitatory neuron" > receiver.txt
```


### 2. Install Dependencies
```bash
# Install R packages
Rscript -e "install.packages(c('Seurat', 'SingleCellExperiment', 'openxlsx', 'presto', 'jsonlite', 'DescTools', 'plyr', 'dplyr', 'homologene', 'ggplot2', 'reshape2', 'stringr'))"

# Install Python packages
pip install -r requirements.txt

# Install Ollama
curl -fsSL https://ollama.ai/install.sh | sh
```

### 3. Start Ollama Service
```bash
ollama serve
```

### 4. Download Example Model
```bash
ollama pull llama3.2
```

### 5. Run Example Analysis
```bash
# Make pipeline executable
chmod +x pipeline-test.sh

# Run with example data
./pipeline.sh \  
  --log-file "./report.log" \
  --rds-file "example.rds" \
  --celltype-colname "Cell.Types" \
  --condition-colname "condition" \
  --condition1 "tumor" \
  --condition2 "NA" \
  --sender-file "./sender.txt" \
  --receiver-file "./receiver.txt" \
  --percent-exp 0.005 \
  --logfc-threshold 0.20 \
  --intermediate-downstream-gene-num 2 \
  --permutation-num 1000 \
  --lambda 0.0 \
  --species "mouse" \
  --assay "RNA" \
  --disease "AD" \
  --results-dir "results" \
  --cell-type "astrocyte-excitatory neuron" \
  --disease-context "AD" \
  --model "llama3.2" \
  --temperature 0.7 \
  --max-tokens 1500 \
  --context-size 131072 \
  --seed 512
```

### Advanced Usage with Custom Parameters

#### Required Parameters
| Parameter | Description | Example |
|-----------|-------------|---------|
| `--log-file` | Analysis log output | `"./report.log"` |
| `--rds-file` | Path to Seurat RDS file | `"./data.rds"` |
| `--celltype-colname` | Cell type column name | `"Cell.Types"` |
| `--condition-colname` | Condition column name | `"condition"` |
| `--condition1` | Primary condition | `"control"` |
| `--condition2` | Secondary condition | `"treatment"` or `"NA"` |
| `--sender-file` | Sender cell type file | `"./sender.txt"` |
| `--receiver-file` | Receiver cell type file | `"./receiver.txt"` |
| `--cell-type` | Communication description | `"microglia-neuron"` |

#### S2C2 Analysis Parameters
| Parameter | Default | Range | Description |
|-----------|---------|-------|-------------|
| `--percent-exp` | 0.005 | 0-1 | Expression percentage threshold |
| `--logfc-threshold` | 0.20 | >0 | Log fold change threshold |
| `--intermediate-downstream-gene-num` | 2 | ≥1 | Downstream gene count |
| `--permutation-num` | 1000 | ≥1 | Permutation test iterations |
| `--lambda` | 0.0 | 0-1 | Lambda parameter |
| `--species` | "mouse" | mouse/human | Species type |
| `--assay` | "RNA" | RNA/integrated | Assay type |
| `--disease` | "AD" | Any | Disease context |
| `--results-dir` | "results" | Any | Output directory |

#### LLM Parameters
| Parameter | Default | Range | Description |
|-----------|---------|-------|-------------|
| `--model` | "llama3.2" | See model list | Ollama model selection |
| `--disease-context` | "Alzheimer's disease" | Any | Disease for LLM analysis |
| `--temperature` | 0.7 | 0-2 | Model creativity |
| `--max-tokens` | 1500 | ≥1 | Maximum generated tokens |
| `--context-size` | 131072 | ≥1024 | Context window size |
| `--seed` | 512 | ≥0 | Random seed for reproducibility |


### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8GB | 16GB+ |
| Storage | 10GB | 50GB+ |
| CPU | 4 cores | 8+ cores |
| GPU | Optional | NVIDIA GPU for faster LLM inference |



## 📚 Citation

If you use S2C2 in your research, please cite:

```bibtex
@article{s2c2_2024,
  title={S2C2: Single-Cell Cross Communication Explorer with AI-Powered Hypothesis Generation},
  author={TBD},
  journal={TBD},
  year={2024},
  doi={TBD}
}
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
