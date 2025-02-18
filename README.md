# Step-Audio-tts

Google Colab，要在Ububtu的话按照以下步骤

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
下面是AutoDL服务器的代码
```
ls /usr/local/cuda-12.5/lib64/libcublasLt*
```

## 3.安装需要的库
pip install -q -r requirements.txt
