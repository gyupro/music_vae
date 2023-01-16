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

