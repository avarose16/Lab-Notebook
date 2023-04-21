# Lab-Notebook
Lab notebook for GEN711

4/14 Class Notes

git clone (link)
pulls repository features into the VS code workspace 

github.com/jthmiller/gen711-811-example

fork example repository 

fork:
add a copy of a repo to your account

git version:
tells you what version of git is installed

4/21 CLASS NOTES

cut adapt:
removes primer sequences 

conda activate genomics: 
gives access to the fastq program

touch testfile.txt:
makes an empty text file

git add (filename):
adds a file to git from ron


COMMANDS

cp /tmp/gen711_project_data/fastp-single.sh ~/fastp-single.sh

chmod +x ~/fastp-single.sh

head fastp.sh

./fastp-single.sh 150 /tmp/gen711_project_data/FMT/fastqs trimmed_fastqs

conda activate qiime2-2022.8

qiime tools import \
   --type "SampleData[PairedEndSequencesWithQuality]"  \
   --input-format CasavaOneEightSingleLanePerSampleDirFmt \
   --input-path /home/users/amr1175/trimmed_fastqs \
   --output-path /home/users/amr1175/trimmed_fastqs / trimmed_stuff \

   qiime cutadapt trim-paired \
    --i-demultiplexed-sequences /home/users/amr1175/trimmed_fastqs/trimmed_stuff \
    --p-cores 4 \
    --p-front-f TACGTATGGTGCA \
    --p-discard-untrimmed \
    --p-match-adapter-wildcards \
    --verbose \
    --o-trimmed-sequences /home/users/amr1175/trimmed_fastqs / cutadapt-sequences.qza

qiime demux summarize \
--i-data /home/users/amr1175/trimmed_fastqs/cutadapt-sequences.qza \
--o-visualization  /home/users/amr1175/trimmed_fastqs / outputfiles.qzv 

qiime dada2 denoise-paired \
    --i-demultiplexed-seqs qiime_out/${run}_demux_cutadapt.qza  \
    --p-trunc-len-f ${trunclenf} \
    --p-trunc-len-r ${trunclenr} \
    --p-trim-left-f 0 \
    --p-trim-left-r 0 \
    --p-n-threads 4 \
    --o-denoising-stats /home/users/amr1175/trimmed_fastqs /denoising-stats.qza \
    --o-table /home/users/am1175/trimmed_fastqs /feature_table.qza \
    --o-representative-sequences /home/users/amr1175/trimmed_fastqs /rep-seqs.qza

qiime metadata tabulate \
    --m-input-file /home/users/amr1175/trimmed_fastqs /denoising-stats.qza \
    --o-visualization /home/users/amr1175/trimmed_fastqs /denoising-stats.qzv

qiime feature-table tabulate-seqs \
        --i-data /home/users/amr1175/trimmed_fastqs /rep-seqs.qza \
        --o-visualization /home/users/amr1175/trimmed_fastqs /rep-seqs.qzv 
