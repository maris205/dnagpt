# dnagpt
GPT lanuage model for dna sequence

we use gpt2 model to create the dna language model

Origin data is in https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_009914755.1/

it's the full human genome data

download data use ncbi data set tools: 

curl -o datasets 'https://ftp.ncbi.nlm.nih.gov/pub/datasets/command-line/LATEST/linux-amd64/datasets' 

chmod +x datasets 

./datasets download genome accession GCF_000001405.40 --filename genomes/human_genome_dataset.zip 

then move the gene data to human2.fra


then run:
1 process_data.ipynb
2 sample_data.ipynb
3 train_bpe.ipynb
4 train_gpt_formal.ipynb
to train the gpt2 version of dna language model

