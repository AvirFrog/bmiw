# Składanie Genomu

##  Instalacja Condy i Mamby
<details>

<summary>Pobieranie miniforge</summary>

```bash
wget https://github.com/conda-forge/miniforge/releases/download/24.9.2-0/Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
chmod +x Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
./Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
conda config --add channels bioconda
```
  
</details>


## Instalacja niezbędnych programów

Dobrą praktyką (i bezpieczną) jest tworzenie osobnego środowiska do każdego narzędzia, ale nie jest to wymagane.

<details>
<summary> Tworzenie nowego środowiska </summary>

```bash
conda create -n env_name
```
</details>

Instalacja potrzebnych narzędzi:

<details>
<summary>FastQC</summary>
  
```bash
mamba install bioconda:fastqc
```
</details>

<details>
<summary>FastP</summary>
  
```bash
mamba install bioconda:fastp
```
</details>

<details>
<summary>spades</summary>
  
```bash
mamba install bioconda:spades
```
</details>

<details>
<summary>MegaHit</summary>
  
```bash
mamba install bioconda:megahit
```
</details>

<details>
<summary>Quast</summary>
  
```bash
mamba install bioconda:quast
```
</details>

<details>
<summary>MultiQC</summary>
  
```bash
mamba install bioconda:multiqc
```
</details>



