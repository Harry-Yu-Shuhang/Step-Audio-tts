# Step-Audio-tts

.ipynb文件是Google Colab代码，打开就可以用。要在Ububtu的话按照以下步骤

**注意：Cuda要12.x版本，11.x用不了**

## 1.拉取云端仓库

 创建conda环境
```
conda create -n stepaudio python=3.10
```
激活conda环境
```
conda activate stepaudio
```
如果没安装conda，先安装conda，自行查阅。Python3.10
如果报错，运行以下命令
```
conda init bash  # 如果你用的是 Bash
source ~/.bashrc  # 如果用 Bash
```
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
pip install -r requirements.txt
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
apt update
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
huggingface-cli download stepfun-ai/Step-Audio-Tokenizer --local-dir models/stepfun-ai/Step-Audio-Tokenizer
huggingface-cli download stepfun-ai/Step-Audio-TTS-3B --local-dir models/stepfun-ai/Step-Audio-TTS-3B
```
创建输出结果文件夹
```
mkdir output_audio
```
安装ffmeg(如果没装过)
```
sudo apt install ffmpeg
```

## 5.推理
两种模式
### A.终端运行
两种方法
#### a.tts
```
python tts_inference.py --model-path=models/stepfun-ai/ --synthesis-type=tts --output-path=./output_audio/output_tts.wav
```
#### b.克隆
```
python tts_inference.py --model-path=models/stepfun-ai/ --synthesis-type=clone --output-path=./output_audio/output_clone.wav
```
### B.Python运行
创建 run_tts.py
```
sudo vim run_tts.py
```
按下i进入插入模型，填写以下内容。如果需要修改，自行修改。
```
import os

# 运行 TTS（文本转语音）
os.system("python tts_inference.py --model-path=models/stepfun-ai/ --synthesis-type=tts --output-path=./output_audio/output_tts.wav")

# 运行声音克隆
os.system("python tts_inference.py --model-path=models/stepfun-ai/ --synthesis-type=clone --output-path=./output_audio/output_clone.wav")

print("TTS 生成完毕，文件：output_tts.wav")
print("声音克隆生成完毕，文件：output_clone.wav")
```
按下:wq保存并退出，然后运行
```
python run_tts.py
```
