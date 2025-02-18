# Step-Audio-tts

文件是Google Colab代码，要在Ububtu的话按照以下步骤

 ## 1.拉取云端仓库
终端执行
```
git clone --recursive https://github.com/stepfun-ai/Step-Audio.git
```

进入项目文件夹
```
cd Step-Audio
```

## 2.检查需要的驱动
```
nvcc --version
```
下面是Colab服务器的代码，别的根目录要改
```
ls /usr/local/cuda-12.5/lib64/libcublasLt*
```

## 3.安装需要的库
```
pip install -q -r requirements.txt
```
```
pip show torch
```
```
pip install torch==2.3.1 torchvision==0.18.1 torchaudio==2.3.1 --index-url https://download.pytorch.org/whl/cu121
```
```
pip install onnxruntime-gpu==1.20.1
```
```
pip show onnxruntime-gpu
```
```
apt install -y sox
```

## 4.登陆Hugging Face
```
huggingface-cli login
```
从Hugging Face下载模型
```
mkdir -p models/stepfun-ai
huggingface-cli download stepfun-ai/Step-Audio-Tokenizer --quiet --local-dir models/stepfun-ai/Step-Audio-Tokenizer
huggingface-cli download stepfun-ai/Step-Audio-TTS-3B --quiet --local-dir models/stepfun-ai/Step-Audio-TTS-3B

```
```
!huggingface-cli download stepfun-ai/Step-Audio-TTS-3B --quiet --local-dir /content/models/stepfun-ai/Step-Audio-TTS-3B
```
