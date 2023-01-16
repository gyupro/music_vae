# music_vae
This repo will be a private repo soon.

## Generated samples 

[Link](https://drive.google.com/drive/u/0/folders/1NQhCvPxb7QhGgl9laX_HUkImlCuVGL3t)


## Steps applied to generate samples

1. Train model 

install magenta and setup with miniconda (manual installation can cause a problem, faster installation is available with miniconda)

download groovae dataset and create tfrecord files from dataset
```
convert_dir_to_note_sequences --input_dir ../../../../groove/ --output_file notesequences.tfrecord --recursive
```

train music vae with groovae_4bar config file
```
 music_vae_train --config=groovae_4bar --run_dir=. --mode=train --examples_path=notesequences.tfrecord
```

2. Generate samples

Generate samples with command

```
music_vae_generate --config=groovae_4bar --run_dir=. --mode=sample --num_outputs=5 --output_dir=generated
```
- training log

![image](https://user-images.githubusercontent.com/79894531/212575965-cf64e805-2bd3-413e-aaf2-0867c02bda74.png)

## Paper explanation

key word

- hierarchical decoder

### model architecture

![image](https://user-images.githubusercontent.com/79894531/212577791-8259bc08-ca7b-4bee-bc19-0e5921472b70.png)


The music-vae model takes input as note of sequences

The model consists of encoder and decoder, and it uses BidirectionalLstmEncoder to encode input and GrooveLstmDecoder to decode a latent vector

Encdoing Process

![image](https://user-images.githubusercontent.com/79894531/212577403-62d9c9a0-d703-4697-a9e5-484235b7eaf1.png)

### 3.2. Hierarchical Decoder

Decoding Process

Undirectional LSTM for the conductor with a hidden size of (1024, 512)

after producing the sequence of embedding vectors, they are fed into FC layer with tanh (The decoder RNN) 

. . . . (Not yet understood)

#### TODO 

More time needed to understand the logic applied below.

![image](https://user-images.githubusercontent.com/79894531/212578933-6f51ea57-dff5-4a36-8a1e-6a8b85ad62b4.png)



The model finally interprets the output with GrooveConverter as we call post-processing process

loss used to reconstruct output 

|output|loss|
|---|---|
|hit|log loss|
|velocity|mse|
|offset|mse|
