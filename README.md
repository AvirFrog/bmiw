# Bioinformatyka Mikroorganizmów i Wirusów



## Instalacja mamby

Żeby zainstalować mambę najprościej (ale sposób ten jest  najgorszy) użyjemy condy



### Zainstalujmy Conde 

<details>
    <summary>Przykładowy kod</summary>


    spoiler
    
    ```bash
    mamba create -n fastqc -y
    ```



## Składanie Genomu Bakterii



Najpierw powinniśmy zainstalować potrzebne nam narzędzia. 

Korzystać będziemy z condy/mamby

Tworzymy środowisko do FastQC i instalujemy FastQC:

```bash
mamba create -n fastqc -y
```

```bash
mamba activate fastqc
```

```bash
mamba install bioconda::fastqc -y
```

Tworzymy środowisko do fastp i instalujemy fastp:

```bash
mamba create -n fastp -y
```

```bash
mamba activate fastp
```

```bash
mamba install bioconda::fastp -y
```

Tworzymy środowisko do spades i instalujemy spades:

```bash
mamba create -n spades -y
```

```bash
mamba activate spades
```

```bash
mamba install bioconda::spades -y
```

Tworzymy środowisko do megahit i instalujemy megahit:

```bash
mamba create -n megahit -y
```

```bash
mamba activate megahit
```

```bash
mamba install bioconda::megahit -y
```

Tworzymy środowisko do quast i instalujemy quast:

```bash
mamba create -n quast -y
```

```bash
mamba activate quast
```

```bash
mamba install bioconda::quast -y
```

