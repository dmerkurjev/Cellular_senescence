# To download the data:

# Create environment
conda create -n stroke_rnaseq -c bioconda -c conda-forge \
  sra-tools fastqc multiqc hisat2 samtools trimmomatic subread -y
conda activate stroke_rnaseq

# Folder setup
mkdir -p ~/0_Cellular_senescence/{data,fastq,trimmed,aligned,counts,logs,qc}
cd ~/0_Cellular_senescence/data

wget https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos8/sra-pub-zq-818/SRR011/11255/SRR11255824/SRR11255824.lite.1 # Young -dox SRX7865899

wget https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos8/sra-pub-zq-818/SRR011/11255/SRR11255825/SRR11255825.lite.1 # Young +dox SRX7865900

wget https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos8/sra-pub-zq-818/SRR011/11255/SRR11255826/SRR11255826.lite.1 # Senescent -dox SRX7865901

wget https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos8/sra-pub-zq-818/SRR011/11255/SRR11255827/SRR11255827.lite.1 # Senescent +dox SRX7865902

for r in "${SRR[@]}"; do
  fasterq-dump -e 16 -p -O . "$r"
  gzip -f "${r}.fastq"
done
