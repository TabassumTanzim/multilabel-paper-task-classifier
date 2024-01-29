# MultiLabel-Paper-Task-Classifier
A text classification model built from scatch consisting of data collection, model training and deployement. The model can classify 238 tasks enlisted [here](deployment/task_types_encoded.json)

## Data Collection
Data extraction began by retrieving information from **[papers with code](https://paperswithcode.com/sota)** in two steps. The initial step involved obtaining paper URLs, which led to the formation of [paper_urls](scaper/paper_urls.csv) dataset comprising paper titles and their corresponding links with [paper_url.ipynb](scaper/paper_url.ipynb)

Following this, each URL in the dataset was visited to extract abstracts and the associated tasks from the papers using [url_details.ipynb](scaper/url_details.ipynb), ultimately forming the [primary dataset](scaper/all_data.csv).

In total `26778 paper details` have been scraped.

## Data Pre-processing
At first, there were 2397 different tasks in the dataset. After looking closely, I found that 2139 of them were tasks. So, I removed those tasks, leaving 258 tasks. Then, I got rid of the abstracts without any task, and that left me with 26628 samples.

## Model Training
I fine-tuned a `distilroberta-base` model from HuggingFace Transformers using Fastai and Blurr. You can check out the notebook for the model training [here](notebooks/multilabel_text_classification.ipynb).

## Model Compression and ONNX Inference
The model that underwent training has a memory size of 314+MB. I compressed this model using ONNX quantization and reduced its size to below 83MB.

## Model Deployement
The compressed model is deployed to HuggingFace Spaces Gradio App. The implementation can be found in deployment folder or [here](https://huggingface.co/spaces/Tabas34/paper_classifier)

<img width="1188" alt="image" src="https://github.com/TabassumTanzim/multilabel-paper-task-classifier/assets/75922668/5f5eccb0-fb7c-41e6-8ff6-6bc9df61750b">
