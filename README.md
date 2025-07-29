# OCR With VLM LM Studio

This repository was created to perform Optical Character Recognition (OCR) using a Visual Language Model (VLM) with LM Studio. The OCR is applied to license plate images from the [Indonesian License Plate Dataset](https://www.kaggle.com/datasets/juanthomaswijaya/indonesian-license-plate-dataset). 

## Features
* OCR inference using a VLM through LM Studio
* Evaluation using Character Error Rate (CER)
* Compatible with custom datasets with paired image and groundtruth files

## Dataset Structure
Each image is accompanied by a corresponding ground-truth `.text` file for evaluation.  
Make sure your dataset is organized as follows:
```
dataset/
├── ground-truth/
│   ├── sample1.txt
│   ├── sample2.txt
│   └── ...
└── images/
    ├── sample1.jpg
    ├── sample2.jpg
    └── ...

```
## Getting Started
Before running the `.ipynb` notebook, make sure to:
1. Install LM Studio by following the guide in the [LM Studio documentation](https://lmstudio.ai/docs/app).
2. Install required Python packages by running:
    ```
    pip install -r requirements.txt
    ```
3. Start the LM Studio server:  
    Make sure the LM Studio application is running, then you can start the server by either:
    * Clicking the "Start Server" button inside the LM Studio app, or
    * Using the terminal command below (requires the app to be open in the background):
        ```
        lms server start
        ```
4. Download the VLM model of your choice from the LM Studio app, then configure the notebook to use it by setting the model name here:
    ```py
    model = lms.llm("google/gemma-3-4b")
    ```
    > You can replace "google/gemma-3-4b" with any other model you’ve downloaded and want to use.

5. Customize the prompt task.  
   The default prompt is designed to extract the license plate number from an image. If you're working with a different dataset or have a different objective, feel free to modify the prompt to suit your needs:
    ```py
    chat.add_user_message(
        "What is the license plate number shown in this image? Respond only with the license plate characters, without any spaces, or punctuation. Do not include the expiration date.",
        images=[image_handle]
    )
    ```
6. Evaluation results will be saved in an Excel file inside the `result/` directory.