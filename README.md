# Text_To_Image By Flux


Welcome to **FLUX** – a minimal inference code repository designed for image generation and editing using our powerful Flux models. FLUX makes it easy to transform text prompts into stunning images, whether you're experimenting locally or using our hosted API.

![grid](https://github.com/user-attachments/assets/a0443c08-8e12-4afd-a6a4-b00ec5757957)
![Screenshot (98)](https://github.com/user-attachments/assets/1a0bec90-b1d0-4fe1-8a66-f943fa7b7895)



## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
  - [Local Installation](#local-installation)
  - [Installation with TensorRT Support](#installation-with-tensorrt-support)
- [Models](#models)
- [API Usage](#api-usage)
  - [Python Interface](#python-interface)
  - [Command Line Interface](#command-line-interface)
- [Documentation](#documentation)
- [Citation](#citation)
- [License](#license)

## Overview
FLUX offers a suite of models for tasks such as text-to-image synthesis, in/out-painting, and structural conditioning. With support for both local and API-driven workflows, our repository is designed to help you generate and edit images seamlessly.

## Installation

### Local Installation
Clone the repository and install the required packages using the following commands:

```bash
cd $HOME
git clone https://github.com/black-forest-labs/flux
cd $HOME/flux
python3.10 -m venv .venv
source .venv/bin/activate
pip install -e ".[all]"



Installation with TensorRT Support
For enhanced performance using TensorRT, follow these steps to use an NVIDIA PyTorch image:

bash
Copy
Edit
cd $HOME
git clone https://github.com/black-forest-labs/flux

# Import the NVIDIA PyTorch image (replace $oauthtoken with your token)
enroot import 'docker://$oauthtoken@nvcr.io#nvidia/pytorch:25.01-py3'
enroot create -n pti2501 nvidia+pytorch+25.01-py3.sqsh
enroot start --rw -m ${PWD}/flux:/workspace/flux -r pti2501

cd flux
pip install -e ".[tensorrt]" --extra-index-url https://pypi.nvidia.com
Models
FLUX includes an extensive suite of models. Here are some of the available options:

Name	Usage	HuggingFace Repository	License
FLUX.1 [schnell]	Text to Image	Link	apache-2.0
FLUX.1 [dev]	Text to Image	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Fill [dev]	In/Out-painting	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Canny [dev]	Structural Conditioning	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Depth [dev]	Structural Conditioning	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Canny [dev] LoRA	Structural Conditioning	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Depth [dev] LoRA	Structural Conditioning	Link	FLUX.1-dev Non-Commercial License
FLUX.1 Redux [dev]	Image Variation	Link	FLUX.1-dev Non-Commercial License
FLUX.1 [pro]	Text to Image	Available via our API	
FLUX1.1 [pro]	Text to Image	Available via our API	
FLUX1.1 [pro] Ultra/raw	Text to Image	Available via our API	
FLUX.1 Fill [pro]	In/Out-painting	Available via our API	
FLUX.1 Canny [pro]	Structural Conditioning	Available via our API	
FLUX.1 Depth [pro]	Structural Conditioning	Available via our API	
FLUX1.1 Redux [pro]	Image Variation	Available via our API	
FLUX1.1 Redux [pro] Ultra	Image Variation	Available via our API	
Note: The weights of the autoencoder are released under the Apache-2.0 license and are available in the corresponding HuggingFace repositories.

API Usage
Access our models programmatically through our API. First, register at api.bfl.ml to obtain your API key. Then, either set the environment variable:

bash
Copy
Edit
export BFL_API_KEY=<your_key_here>
or pass the API key directly in your calls.

Python Interface
Here's an example of how to generate an image using Python:

python
Copy
Edit
from flux.api import ImageRequest

# Create an API request (non-blocking)
request = ImageRequest("A beautiful beach", name="flux.1.1-pro")
# Alternatively, you can provide the API key directly:
# request = ImageRequest("A beautiful beach", name="flux.1.1-pro", api_key="your_key_here")

# The following will block until the image generation is complete:
image_url = request.url        # Retrieve the URL of the generated image
image_bytes = request.bytes    # Get the raw image bytes
request.save("outputs/api.jpg")  # Save the image locally
image_pil = request.image      # Get a PIL image object
Command Line Interface
Generate images directly from the command line:

bash
Copy
Edit
# Retrieve the URL of the generated image
python -m flux.api --prompt="A beautiful beach" url

# Generate the image and save it locally
python -m flux.api --prompt="A beautiful beach" save outputs/api

# Display the generated image directly
python -m flux.api --prompt="A beautiful beach" image show
