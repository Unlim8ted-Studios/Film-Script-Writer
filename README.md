# Film Script Writer
> This was one of my first projects experimenting with language models.

A small GPT-2 based project for training a model on film scripts and generating new screenplay-style text.

The project includes scripts for collecting screenplay data, converting it into a Hugging Face dataset, fine-tuning DistilGPT-2, and generating text from the finished model.

## How It Works

The basic workflow is:

1. Collect film scripts
2. Convert the scripts into a dataset
3. Fine-tune a GPT-2 model on that dataset
4. Use the trained model to generate screenplay-style text

The project can either use scripts you collect yourself or scrape scripts from IMSDb.

## Files

### `scrape-data.py`

Scrapes available film scripts from IMSDb and saves them as `.txt` files inside a `scripts` folder.

### `data2database.py`

Reads the `.txt` files from the `scripts` folder and converts them into a Hugging Face dataset stored in:

```text
dataset/
```

### `train.py`

Loads the dataset and fine-tunes `distilgpt2` on the screenplay text.

The trained model and tokenizer are saved to:

```text
fine_tuned_gpt2/
```

If CUDA is available, training will automatically use the GPU.

### `generate.py`

Loads the trained model from:

```text
fine_tuned_gpt2/
```

and generates screenplay-style text from a starting prompt.

## Installation

Clone the repository and install the dependencies:

```bash
pip install -r requirements.txt
```

The main dependencies are:

- PyTorch
- Transformers
- Hugging Face Datasets
- BeautifulSoup
- Requests

If you have a compatible GPU, installing the appropriate CUDA-enabled version of PyTorch can make training significantly faster.

## Training Your Own Model

### 1. Gather scripts

You can either run:

```bash
python scrape-data.py
```

or create a folder called:

```text
scripts/
```

and place your own `.txt` screenplay files inside it.

### 2. Build the dataset

Run:

```bash
python data2database.py
```

This combines the screenplay files into a Hugging Face dataset.

### 3. Train

Run:

```bash
python train.py
```

The current training configuration fine-tunes DistilGPT-2 for three epochs and saves the resulting model to:

```text
fine_tuned_gpt2/
```

Training time depends heavily on your hardware and the amount of screenplay data being used.

## Generating a Script

Once a model has been trained, run:

```bash
python generate.py
```

By default, the script starts from a prompt similar to:

```text
FADE IN: INT. COFFEE SHOP - DAY

John and Sarah sit across from each other, sipping their drinks.
```

and continues generating text from there.

You can edit the prompt in `generate.py` to start with any scene or screenplay text you want.

## Dataset

The included `dataset/` directory contains a dataset previously created for the project.

You can replace it by running `data2database.py` on your own collection of screenplay files.

## Notes

This is an experimental project rather than a production screenplay-writing system.

The quality of the generated text depends heavily on:

- the scripts used for training
- the amount of training data
- training time
- model size
- generation settings

The current model is based on DistilGPT-2, so its capabilities are relatively limited compared with modern language models.

## Scraping

`scrape-data.py` was written to collect screenplay text from IMSDb.

Website structure and availability can change over time, so the scraper may require updates if the site changes.

Make sure any data you collect or use is handled in accordance with the source site's terms and applicable copyright rules.
