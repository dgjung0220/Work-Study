### Object Detection guide.2

##### GPU 사용량 확인
`` nvidia-smi ``
![f2f075fc.png](attachments\f2f075fc.png)
 ``ps aux --sort=-pcpu,-pmem | head -10`` 명령을 통해 사용자 확인. ``kill -9 PID`` 로 프로세스 강제 종료.
 
 ##### Pre-condition
 ```
 protoc_3.5/bin/protoc object_detection/protos/*.proto --python_out=.
 export PYTHONPATH=$PYTHONPATH:/home/goya.choi/models/research:/home/goya.choi/models/research/slim
 ```
 
 ##### Training
 ```
CUDA_VISIBLE_DEVICES=0 python object_detection/train.py --logtostderr --pipeline_config_path=object_detection/models/model/ssd_mobilenet_v1_coco.config --train_dir=train_dir
 ```