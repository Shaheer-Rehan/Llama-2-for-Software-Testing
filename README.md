# Llama-2-for-Software-Testing
This project focuses on test case generation from focal methods in Java by finetuning the Llama-2-7b-chat-hf model. 

## Selection of LLM & Dataset
The Llama-2-7b-chat-hf model for NousResearch was selected as the base model. This is the same model as the official Llama-2-7b from Meta, but it has been republished by NousResearch on the Hugging Face platform and is openly accessible. The model is available at https://huggingface.co/NousResearch/Llama-2-7b-chat-hf

The publicly available methods2test repository from Microsoft was selected to train the model. This repository is available at https://github.com/microsoft/methods2test

The dataset selected for this task contains focal methods in Java as the inputs and their respective unit tests as the outputs.

### Link to the Dataset Files
For the experiment, the level of focal context selected is FM_FC which includes important information of the focal class name along with the focal method. The FM_FC folder from the raw corpus is used for the project, and the training data is treated as the parent dataset during the finetuning process. The folder containing the raw data with the specified context level from the Microsoft repository is available at this link: https://github.com/microsoft/methods2test/tree/main/corpus/raw/fm_fc 

## Choice of Hardware
The A100 GPU from Google Colab was used for the entirety of this project, and the settings specified in the code notebook will not work unless the A100 GPU is used due to memory overheads.

## Experiment Methodology
A subset of 25000 records is used from the dataset due to the constraints of time and computational resources.

The dataset is then tokenized, and the resulting records are filtered based on the number of tokens to ensure a high-quality dataset. Next, QLoRA quantization is performed so that the finetuning process can be computed on consumer-scale hardware.

Finally, the Llama-2-7b model is trained for 12 epochs to ensure it can be sufficiently trained and repurposed for software test case generation.

## Validation
The model, after finetuning, is used for inference to examine how it performs for unseen focal methods in Java. The model’s response is then compared with baseline test cases available for the focal methods.
