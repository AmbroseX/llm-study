
python=3.10，cu118

## 非Root用户从conda安装

运行

```
conda search cudatoolkit --info
```

找到要下载的cuda版本，把cuda下载到本地

后面安装

```
conda install --use-local 本地cuda包所在路径
```

同样搜索cudnn

```
conda search cudnn --info
```

```
conda install --use-local 本地cuda包所在路径
```

安装torch torchvision torchaudio 和 xformers

```shell
pip install torch==2.1.1 torchvision==0.16.1 torchaudio==2.1.1 xformers==0.0.23 --index-url https://download.pytorch.org/whl/cu118
```

> xformers版本问题：
> 0.0.22对应pytorch 2.0.1
> 
> 0.0.23对应2.1.1
> 
> 0.0.23.post1对应2.1.2

## Vllm安装
查看：[https://github.com/vllm-project/vllm/releases/](https://github.com/vllm-project/vllm/releases/)

根据自己的python版本选择安装
```shell
pip install https://github.com/vllm-project/vllm/releases/download/v${VLLM_VERSION}/vllm-${VLLM_VERSION}+cu118-cp${PYTHON_VERSION}-cp${PYTHON_VERSION}-manylinux1_x86_64.whl
```
命令如下：
```shell
pip install https://github.com/vllm-project/vllm/releases/download/v0.2.7/vllm-0.2.7+cu118-cp310-cp310-manylinux1_x86_64.whl
```
源码安装会缺不少东西

## FastChat安装
[https://github.com/lm-sys/FastChat](https://github.com/lm-sys/FastChat)
### pip安装

```shell
pip3 install "fschat[model_worker,webui]"
pip install einops transformers_stream_generator
```

### 源码安装
修改源代码后可以用这个
首先需要卸载已经安装的fastchat
```shell
pip uninstall fschat
```

```shell
git clone https://github.com/lm-sys/FastChat
cd FastChat
pip install -e ".[model_workder,webui]"
```

