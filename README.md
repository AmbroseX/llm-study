# llm-study

[FastChat支持模型](./inference/FastChat支持的模型.md)

[FastChat环境安装](./inference/FastChat环境安装.md)



## 下载hugging face模型和数据集断点下载方法
[查看代码](./scripts/hfd.sh)

推荐官方的 [huggingface-cli](https://huggingface.co/docs/huggingface_hub/guides/download#download-from-the-cli) 命令行工具


其实网络快、稳的话，随便哪种方法都挺好，然而结合国内的网络环境，**断点续传、多线程下载**等特性还是非常有必要的，否则动辄断掉重来很浪费时间。基于这个考虑，对各类方法做个总结和排序：

|方法类别||推荐程度|优点|缺点|
|---|---|---|---|---|
|基于URL|[浏览器网页下载](https://padeoe.com/huggingface-large-models-downloader/#1.-%E6%B5%8F%E8%A7%88%E5%99%A8%E7%BD%91%E9%A1%B5%E4%B8%8B%E8%BD%BD)|⭐⭐⭐|通用性好|手动麻烦/无多线程|
||[多线程下载器](https://padeoe.com/huggingface-large-models-downloader/#2.-%E5%A4%9A%E7%BA%BF%E7%A8%8B%E4%B8%8B%E8%BD%BD%E5%99%A8)|⭐⭐⭐⭐|通用性好|手动麻烦|
|CLI工具|[`git clone`命令](https://padeoe.com/huggingface-large-models-downloader/#3.-Git-clone)|⭐⭐|简单|无断点续传/冗余文件/无多线程|
|专用CLI工具|[`huggingface-cli`+`hf_transfer`](https://padeoe.com/huggingface-large-models-downloader/#4.-huggingface-cli%2Bhf_transfer)|⭐⭐⭐|官方下载工具链，功能最全|无进度条/容错性低|
||[`huggingface-cli`](https://padeoe.com/huggingface-large-models-downloader/#4.1-huggingface-cli)|⭐⭐⭐⭐⭐|官方下载工具|不支持多线程|
|Python方法|[`snapshot_download`](https://padeoe.com/huggingface-large-models-downloader/#5.-snapshot_download)|⭐⭐⭐|官方支持，功能全|脚本复杂/无多线程|
||[`from_pretrained`](https://padeoe.com/huggingface-large-models-downloader/#6.-from_pretrained)|⭐|官方支持，简单|不方便存储，功能不全|
||[`hf_hub_download`](https://padeoe.com/huggingface-large-models-downloader/#6.-hf_hub_download)|⭐|官方支持|不支持全量下载/无多线程|

使用方法：
工具同样支持设置镜像端点的环境变量:
需要给`hfd.sh`添加执行权限
```shell
chmod +x ./hfd.sh
```
```shell
export HF_ENDPOINT="https://hf-mirror.com"
```

基本命令：
```shell
./hfd.sh Qwen/Qwen-1_8B-Chat --tool aria2c -x 4
```
如果没有安装 aria2，则可以默认用 wget：
```shell
./hfd.sh Qwen/Qwen-1_8B-Chat
```

- 下载数据集
```shell
./hfd.sh
```

参考：[https://padeoe.com/huggingface-large-models-downloader/](https://padeoe.com/huggingface-large-models-downloader/)