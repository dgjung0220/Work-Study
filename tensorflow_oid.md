### Tensorflow Object Detection API

#### 0. Prerequisites
```
export PYTHONPATH=$PYTHONPATH:\home\dg.jung\models\research:\home\dg.jung\models\research\slim
```

#### 1. Code download

처음부터 모든 코드를 다 작성하는 것은 시간,지식적 한계가 있기 때문에 기존 코드를 활용한다. tensorflow에는 tensorflow models라고 하는 별도의 서브 프로젝트가 존재하고 tensorflow를 이용해서 여러가지를 구현해놓은 소스 예제들이 있다.

Tensorflow object detection API contains :
- Pre-trained models
- 주피터 노트북 예제
- handy scripts

```
git clone https:\\github.com\tensorflow\models.git
tar -xvf models.tar.gz
```

#### 2. 기 학습(Pre-trained) 모델 가져오기

Inception V3
```
curl -O http:\\download.tensorflow.org\models\image\imagenet\inception-v3-2016-03-01.tar.gz
tar -xzf inception-v3-2016-03-01.tar.gz
```

SSD - MobileNet
```
curl -O http:\\download.tensorflow.org\models\object_detection\ssd_mobilenet_v1_coco_2017_11_17.tar.gz
tar -xvzf ssd_mobilenet_v1_coco_2017_11_17.tar.gz
```

#### 3. 학습 이미지 수집
[Collecting Image Dataset with bounding box](:note:cf036736-f5fb-4309-8400-89eb0e17b531)

#### 4. TF Record 생성

``\models\research\object_detection\dataset_tools\`` 에 converting code 존재.

압축을 푼 메타데이터와 이미지 파일을 이용하여 tfrecord 파일 형태로 컨버팅해야 한다.
Tfrecord - 이미지 바이너리, 이미지에 대한 정보(이미지 크기, 인식할 물체의 크기, 라벨)

Google OID
```
python object_detection/dataset_tools/create_oid_tf_record.py \
    --input_box_annotations_csv=../../google_oid/train-annotations-bbox.csv \
    --input_image_label_annotations_csv=../../google_oid/train-annotations-human-imagelabels-boxable.csv \
    --input_images_directory=/work/nas/images/ObjectDetection/google_oid/shopping/train_02 \
    --input_label_map=object_detection/data/mscoco_shopping_label_map.pbtxt \
    --output_tf_record_path_prefix=/work/nas/images/ObjectDetection/google_oid/tfrecord/train_02_test/oid_train_02.tfrecord
```

MS COCO
```
python object_detection\dataset_tools\create_coco_tf_record.py \
    --train_image_dir=..\..\cocodataset\train2017 \
    --train_annotations_file=..\..\cocodataset\annotations\instances_train2017.json \
    --val_image_dir=..\..\cocodataset\val2017 \
    --val_annotations_file=..\..\cocodataset\annotations\instances_val2017.json \
    --test_image_dir=..\..\cocodataset\test2017 \
    --testdev_annotations_file=..\..\cocodataset\annotations\image_info_test2017\image_info_test2017.json
```

Oxford Pet
```
python object_detection\dataset_tools\create_pet_tf_record.py \
	--label_map_path=object_detection\data\pet_label_map.pbtxt \
    --data_dir=..\..\Oxford-pet \
    --output_dir=..\..\Oxford-pet\tfrecord
```

#### 5. Training
```
CUDA_VISIBLE_DEVICES=2 python object_detection/legacy/train.py \
        --logtostderr \
        --pipeline_config_path=object_detection/models/model/ssd_mobilenet_v1_coco.config \
        --train_dir=train_dir
```

#### 기타
https:\\towardsdatascience.com\building-a-real-time-object-recognition-app-with-tensorflow-and-opencv-b7a2b4ebdc32