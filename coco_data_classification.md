### COCO dataset 데이터 분류

#### 상위 카테고리
['accessory' 'animal' 'appliance' 'electronic' 'food' 'furniture' 'indoor' 'kitchen' 'outdoor' 'person' 'sports' 'vehicle']

#### 하위 카테고리
['airplane' 'apple' 'backpack' 'banana' 'baseball bat' 'baseball glove' 'bear' 'bed' 'bench' 'bicycle' 'bird' 'boat' 'book' 'bottle' 'bowl' 'broccoli' 'bus' 'cake' 'car' 'carrot' 'cat' 'cell phone' 'chair' 'clock' 'couch' 'cow' 'cup' 'dining table' 'dog' 'donut' 'elephant' 'fire hydrant' 'fork' 'frisbee' 'giraffe' 'hair drier' 'handbag' 'horse' 'hot dog' 'keyboard' 'kite' 'knife' 'laptop' 'microwave' 'motorcycle' 'mouse' 'orange' 'oven' 'parking meter' 'person' 'pizza' 'potted plant' 'refrigerator' 'remote' 'sandwich' 'scissors' 'sheep' 'sink' 'skateboard' 'skis' 'snowboard' 'spoon' 'sports ball' 'stop sign' 'suitcase' 'surfboard' 'teddy bear' 'tennis racket' 'tie' 'toaster' 'toilet' 'toothbrush' 'traffic light' 'train' 'truck' 'tv' 'umbrella' 'vase' 'wine glass' 'zebra']

```python
import numpy as np
import json

instance_file = '../annotations/annotations_val2017/instances_val2017.json'

json_data = open(instance_file).read()
result = json.loads(json_data)

# key 목록
print(result.keys())

# 
category_list = result['categories']
super_cat = []
for i in category_list:
    # print(i['supercategory'])
    super_cat.append(i['supercategory'])
    
print(np.unique(super_cat))

# name category
name_cat = []
for i in category_list:
    # print(i['name'])
    name_cat.append(i['name'])
    
print(np.unique(name_cat))
```

