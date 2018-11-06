### Google OID 데이터 분류

#### 1. Import library

```
import numpy as np
import pandas as pd
import glob
import os
import shutil
```
- shutil : 셸 유틸리티. high level file opertations. 파일, 디렉토리의 복사/이동에 사용되는 python 내장 라이브러리.

- glob : [6.2. 파일을 입맛대로(pickle, glob, os.path) - 왕초보를 위한 Python 2.7](https://wikidocs.net/83) 참고.

#### 2. 필요한 카테고리 정의
```
SHOPPING_CATEGORY = ['Eyewear', 'Top', 'Bottom','Shoe', 'Furniture', 'Bag', 
                    'Outerwear', 'Jewelry', 'Dress', 'Watch','Skirt','Package']
OID_CATEGORY = [['Sunglasses', 'Glasses', 'Goggles'], 
                     ['Shirt'], 
                     ['Shorts', 'Trousers', 'Jeans'], 
                     ['Roller skates','High heels','Footwear'],
                     ['Furniture','Loveseat','Closet','Stool', 'Shelf', 'Drawer', 'Bed'],
                     ['Backpack', 'Suitcase', 'Briefcase', 'Handbag'],
                     ['Coat', 'Suit', 'Jacket'],
                     ['Tiara', 'Necklace', 'Earrings'],
                     ['Dress'],['Watch'],['MiniSkirt','Skirt'],
                     ['Glove','Belt','Swimwear','Brassiere','Sock','Tie','Hat','Fedora','Sombrero','Cap']];
```

#### 3. 정의 카테고리별 폴더 생성
```
for i in VISENZE_CATEGORY:
    try:
        if not(os.path.isdir('../data/validation/'+i)):
            os.makedirs(os.path.join('../data/validation/'+i))
    except OSError as e:
        if e.errno != errno.EEXIST:
            print("Failed to create directory!!!")
            raise
```

#### 4. OID class 파일 읽기
```
class_file = '../class-descriptions-boxable.csv'
classList = pd.read_csv(class_file)
```

#### 5. OID annotation 파일 읽기
```
validation_annotations_imagelabels = '../validation-annotations-human-imagelabels-boxable.csv'
validation_label_list = pd.read_csv(validation_annotations_imagelabels)
```

#### 6. 분류
```
for i in range(0, len(validation_label_list)):
    fileName = validation_label_list.iloc[i][0]+'.jpg'
    
    if os.path.exists('../validation/'+fileName):
        category = validation_label_list.iloc[i][2]
        select_index = np.where((classList[0]==category))
        category = classList.iloc[select_index[0][0],1]
        
        print (fileName + ' / ' + category)
        for visenze in range(len(OID_CATEGORY)):
            for oid in range(len(OID_CATEGORY[visenze])):
                if OID_CATEGORY[visenze][oid].lower() in category.lower():
                    shutil.copy('../validation/'+fileName, '../data/validation/'+VISENZE_CATEGORY[visenze])
                    break;
```