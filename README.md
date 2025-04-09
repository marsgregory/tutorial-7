# **Student-Led-Tutorial: Genome Annotation Using Prokka**
### **Task**: Annotate a Bacterial Genome and Submit to a Public Repository
### **Date**: April 17th

---

## **Objective**
Students will:
1. Use **Prokka** to annotate a bacterial genome.
2. Visualize the annotated genome in a genome browser.
3. Validate the annotations and prepare the genome for submission to a public database.
4. Discuss the significance of genome annotation for research and the community.

---

## **Software and Manuals**
1. **Prokka**: Rapid prokaryotic genome annotation.  
   - [Prokka GitHub](https://github.com/tseemann/prokka)  
   - [Prokka Documentation](https://github.com/tseemann/prokka#usage)  
2. **Artemis**: Genome browser for manual curation.  
   - [Artemis Download](https://www.sanger.ac.uk/tool/artemis/)  
3. **tbl2asn**: For GenBank submission formatting.  
   - [tbl2asn Documentation](https://www.ncbi.nlm.nih.gov/genbank/tbl2asn2/)  
4. **KEGG Mapper**: Pathway visualization.  
   - [KEGG Mapper](https://www.genome.jp/kegg/mapper.html)  

---

## **Dataset**
### **Genome**:  
A draft genome of a bacterial species relevant to agriculture, healthcare, or the environment. For this tutorial:  
- **Example**: A rhizobial bacterial genome involved in nitrogen fixation.  
- **Source**: Download a draft genome from **NCBI GenBank** or **JGI Genome Portal**.  
- **Example dataset**:  
  - NCBI Assembly: [*Bradyrhizobium japonicum* USDA 110 genome](https://www.ncbi.nlm.nih.gov/assembly/GCF_000011365.1/).  

---

## **Step-by-Step Tutorial**
### Fork and clone repository(?)
### **Step 1: Install Prokka**
The HPC server has Prokka pre-installed.
   ```bash
   module load prokka/1.14.5
   ```
### **Step 2: Download the Genome**
1. Download the genome FASTA file from NCBI or JGI.
``` bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/011/365/GCF_000011365.1_ASM1136v1/GCF_000011365.1_ASM1136v1_genomic.fna.gz
```
2. Decompress the genome file
``` bash
gunzip GCF_000011365.1_ASM1136v1_genomic.fna.gz
```
2. Rename genome file for simplicity
``` bash
mv GCF_000011365.1_ASM1136v1_genomic.fna genome.fasta
```
### **Step 3: Annotate the Genome Using Prokka**
1. Run Prokka to annotate the genome:
``` bash
prokka --outdir prokka_output --prefix bradyrhizobium --genus Bradyrhizobium --species japonicum genome.fasta
```
- --outdir: Directory for output files.
- --prefix: Prefix for output filenames.
- --genus and --species: Specify the organism's name.
2. Push key output files in prokka_output/:
```
cd prokka_output
```
```
git add bradyrhizobium.faa
git commit -m "KEGG file"
git push origin main
```
```
git add bradyrhizobium.gbk
git commit -m "IGV file"
git push origin main
```
### **Step 4: Visualization Using Artemis**
1. Install Artemis (or any other genome browser). The IGV viewer is a good online alternative (https://igv.org/app/)
``` bash
wget https://sanger-pathogens.github.io/Artemis/Artemis/
tar zxf artemis-unix-release-18.0.0.tar.gz
```
2. To run Artemis:
``` bash
artemis/art prokka_output/bradyrhizobium.gff
```
- Explore coding regions, functional annotations, and structural features.
### **Step 5: Validate Annotations**
1. Check for functional annotations:
- Identify key genes, such as those involved in nitrogen fixation (e.g., nif genes).
- Use KEGG Mapper to map annotated genes to metabolic pathways:
- Upload bradyrhizobium.faa to KEGG Blast Koala (https://www.kegg.jp/blastkoala/).
- Enter blastkopala generated KO numbers into the KEGG MAPPER- RECONSTRUCT (https://www.genome.jp/kegg/mapper/reconstruct.html)

### **Step 6: Results Discussion**


