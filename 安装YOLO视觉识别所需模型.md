按照以下顺序来即可

conda create -n yolov11 python=3.10

conda activate yolov11

2.7版本的torch支持50系显卡

pip install torch==2.7.0 torchvision==0.22.0 torchaudio==2.7.0 --index-url https://download.pytorch.org/whl/cu128

pip install ultralytics

pip install websocket-client

pip install paddleocr

仙人指路：不能使用最新版的paddlepaddle

pip install paddlepaddle==3.2.0

其实适配的版本为

torch==2.7.0

paddleocr==3.4.0

paddlepaddle==3.2.0
