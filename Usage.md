## Usage

### Installation

Install the stable version:

```bash
pip install resemble-enhance --upgrade
```

Or try the latest pre-release version:

```bash
pip install resemble-enhance --upgrade --pre
```

### Enhance

```
resemble_enhance in_dir out_dir
```

### Denoise only

```
resemble_enhance in_dir out_dir --denoise_only
```

### Web Demo

We provide a web demo built with Gradio, you can try it out [here](https://huggingface.co/spaces/ResembleAI/resemble-enhance), or also run it locally:

```
python app.py
```

## Train your own model

### Data Preparation

You need to prepare a foreground speech dataset and a background non-speech dataset. In addition, you need to prepare a RIR dataset ([examples](https://github.com/RoyJames/room-impulse-responses)).

```bash
data
├── fg
│   ├── 00001.wav
│   └── ...
├── bg
│   ├── 00001.wav
│   └── ...
└── rir
    ├── 00001.npy
    └── ...
```

### Training

#### Denoiser Warmup

Though the denoiser is trained jointly with the enhancer, it is recommended for a warmup training first.

```bash
python -m resemble_enhance.denoiser.train --yaml config/denoiser.yaml runs/denoiser
```

#### Enhancer

Then, you can train the enhancer in two stages. The first stage is to train the autoencoder and vocoder. And the second stage is to train the latent conditional flow matching (CFM) model.

##### Stage 1

```bash
python -m resemble_enhance.enhancer.train --yaml config/enhancer_stage1.yaml runs/enhancer_stage1
```

##### Stage 2

```bash
python -m resemble_enhance.enhancer.train --yaml config/enhancer_stage2.yaml runs/enhancer_stage2
```

## Blog

Learn more on our [website](https://www.resemble.ai/enhance/)!
