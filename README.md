# dnagpt
GPT lanuage model for dna sequence

we use gpt2 model to create the dna language model

dna language model trained using gpt2. using human genome data.

Key features of our dangpt models:

1. BPE tokenization instead of k-mers (DNABERT, DNABERT2 also use BPE)
2. GPT model, but not bert(DNABERT, GENA_LM)
3. pre-training on the latest T2T human genome assembly


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




```

from transformers import AutoTokenizer, AutoModel
tokenizer = AutoTokenizer.from_pretrained('dnagpt/human_gpt2-v1')
tokenizer.tokenize("GAGCACATTCGCCTGCGTGCGCACTCACACACACGTTCAAAAAGAGTCCATTCGATTCTGGCAGTAG")
#result: [G','AGCAC','ATTCGCC',....]

model = AutoModel.from_pretrained('dnagpt/human_gpt2-v1')
import torch
dna = "ACGTAGCATCGGATCTATCTATCGACACTTGGTTATCGATCTACGAGCATCTCGTTAGC"
inputs = tokenizer(dna, return_tensors = 'pt')["input_ids"]
hidden_states = model(inputs)[0] # [1, sequence_length, 768]

# embedding with mean pooling
embedding_mean = torch.mean(hidden_states[0], dim=0)
print(embedding_mean.shape) # expect to be 768

# embedding with max pooling
embedding_max = torch.max(hidden_states[0], dim=0)[0]
print(embedding_max.shape) # expect to be 768



