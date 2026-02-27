<div align=center>

# Lean State Search
[![arXiv](https://img.shields.io/badge/arXiv-2501.13959-b31b1b?style=flat&logo=arxiv)](https://arxiv.org/abs/2501.13959)
[![Hugging Face](https://img.shields.io/badge/Hugging%20Face-Model-orange?style=flat&logo=huggingface)](https://huggingface.co/ruc-ai4math/LeanStateSearch2025.3)
[![Try Demo](https://img.shields.io/badge/Try%20Demo-Online-orange?style=flat&logo=render)](https://premise-search.com)


</div>

## 🔥 News
* `2025/04/05` Update: Self-host Lean State Search is available!
* `2025/03/07` Update: [LeanSearchClient](https://github.com/leanprover-community/LeanSearchClient) now supports query Lean State Search from within Lean.
* `2025/03/05` Update: Lean State Search is now publicly available!




## 🧩 About

Lean State Search is an innovative search engine powered by a pretrained model, specifically designed to help mathematicians and Lean4 users efficiently search Mathlib theorems using proof states. It is developed by the AI4Math team at Renmin University of China.

This repository contains the frontend and backend code for the application. You can setup your own server for deployment of Lean State Search.

## ⚒️ Installation

You need to fill in the necessary environment variables in the `.env` file. First, copy the `.env.example` to `.env`:

```shell
cp .env.example .env
```

Here is an example project structure:
```
LeanStateSearch
├── .env
├── compose.yaml
├── data
├── protos
├── scripts
├── lean-state-search
├── state-search-be
├── Makefile
└── README.md
```

We recommend using docker for deployment. Run the following command to build the images of frontend and backend:

```shell
make build-images
```

Then run the command to start the service:

```shell
make init-service
```

### Everything after this doesn't work

After starting the basic services, you need to prepare the data yourself. We provide premises extracted from `v4.16.0` of Mathlib as an example. You can use existing tools like [ntp-toolkit](https://github.com/cmu-l3/ntp-toolkit) to extract data. Run the following command to upload data to the postgresql database.

```shell
cd state-search-be
uv run scripts/upload_theorem.py --data-path ../data/premise4.16.0.jsonl --rev v4.16.0
```

Then run the following command to create vector store. It will take some time depending on the hardware of your computer.

```shell
# In state-search-be/
uv run scripts/create_vector_store.py --rev v4.16.0
```

Now your application can work properly in `http://localhost:${FRONTEND_PORT}`.

## 📖 References

### Training from scratch

The code for training the model from scratch and reproducing the experimental results of our paper can be found [here](https://github.com/ruc-ai4math/Premise-Retrieval).

### Call from API

The application can be accessed through API requests. You can refer to [LeanSearchClient](https://github.com/leanprover-community/LeanSearchClient) as an example. The format is as follows:

```
https://localhost:${FRONTEND_PORT}/api/search?query=${Your query}&results=${result number}&rev=${revision}
```

### Contribute to this project

Comming soon.

## 📌 Citation

```bibtex
@misc{tao2025assistingmathematicalformalizationlearningbased,
      title={Assisting Mathematical Formalization with A Learning-based Premise Retriever},
      author={Yicheng Tao and Haotian Liu and Shanwen Wang and Hongteng Xu},
      year={2025},
      eprint={2501.13959},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2501.13959},
}
```
