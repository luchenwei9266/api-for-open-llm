## docker build

```shell
docker build -t llm-api:pytorch .
```

## docker run

### 主要参数

+ `model_name`: 模型名称，如 `chatglm`、`phoenix`、`moss`等

+ `model_path`: 开源大模型的文件所在路径

+ `device`: 是否使用 `GPU`，可选值为 `cuda` 和 `cpu`，默认值为 `cuda`

+ `lora_model_path`（可选项）: `lora` 模型文件所在路径

+ `embedding_name`（可选项）: 嵌入模型的文件所在路径

+ `quantize`（可选项）: `chatglm` 模型的量化等级，可选项为 16、8、4

+ `load_in_8bit`（可选项）: 使用模型 `8bit` 量化

+ `load_in_4bit`（可选项）: 使用模型 `4bit` 量化

+ `stream_interval`（可选项）: 单词流式输出的 `token` 数量


### ChatGLM

```shell
docker run -it -d --gpus all --ipc=host --net=host -p 80:80 --name=chatglm \
    --ulimit memlock=-1 --ulimit stack=67108864 \
    -v `pwd`:/workspace \
    llm-api:pytorch \
    python api/app.py \
    --port 80 \
    --allow-credentials \
    --model_name chatglm \
    --model_path THUDM/chatglm-6b \
    --device cuda \
    --embedding_name GanymedeNil/text2vec-large-chinese
```

### MOSS

```shell
docker run -it -d --gpus all --ipc=host --net=host -p 80:80 --name=moss \
    --ulimit memlock=-1 --ulimit stack=67108864 \
    -v `pwd`:/workspace \
    llm-api:pytorch \
    python api/app.py \
    --port 80 \
    --allow-credentials \
    --model_name moss \
    --model_path fnlp/moss-moon-003-sft-int4 \
    --device cuda \
    --embedding_name GanymedeNil/text2vec-large-chinese
```

### Phoenix

```shell
docker run -it -d --gpus all --ipc=host --net=host -p 80:80 --name=phoenix \
    --ulimit memlock=-1 --ulimit stack=67108864 \
    -v `pwd`:/workspace \
    llm-api:pytorch \
    python api/app.py \
    --port 80 \
    --allow-credentials \
    --model_name phoenix \
    --model_path FreedomIntelligence/phoenix-inst-chat-7b \
    --device cuda \
    --embedding_name GanymedeNil/text2vec-large-chinese
```

### Guanaco

```shell
docker run -it -d --gpus all --ipc=host --net=host -p 80:80 --name=guanaco \
    --ulimit memlock=-1 --ulimit stack=67108864 \
    -v `pwd`:/workspace \
    llm-api:pytorch \
    python api/app.py \
    --port 80 \
    --allow-credentials \
    --model_name guanaco \
    --model_path timdettmers/guanaco-33b-merged \
    --device cuda \
    --load_in_4bit \
    --embedding_name GanymedeNil/text2vec-large-chinese
```