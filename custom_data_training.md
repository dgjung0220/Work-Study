### Custom data training

[[Deep learning] Tensorflow object detection API 사용하기](http://iamyoonkim.tistory.com/13)

#### 1. model config 작성하기  
``models\research\object_detection\samples\configs`` 에 몇 개 모델의 config sample 존재. custom data에 맞게 내용 수정 필요.
  
  
#### 2. .pbtxt 만들기
.pbtxt는 tensorflow 에서 label들을 다루기 위한 format이다.
``models\research\object_detection\data`` 에 sample pbtxt 파일 존재. 형태는 아래와 같다.
```
item {
  name : "m\01g317"
  id : 1
  display_name : "person"
}
```
  
  
#### 3.  .tfrecord 파일 만들기
.tfrecord 파일은 tensorflow에서 training할 때 읽은 대상이다.  즉, (이미지 + 라벨 파일)을 바이너리로 저장한 .tfrecord 파일로 변환해두어야 한다. 변환 코드는 ``models\research\object_detection`` 에 sample로 존재한다.

#### 4. Training
```
$ CUDA_VISIBLE_DEVICES=0 python object_detection/legacy/train.py \
  --logtostderr \
  --pipeline_config_path=${PATH_TO_YOUR_PIPELINE_CONFIG} \
  --train_dir=${PATH_TO_TRAIN_DIR}
```

