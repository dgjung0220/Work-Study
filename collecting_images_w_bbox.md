### Collecting Image Dataset with bounding box

```
wget -c --limit-rate=5000k <Download URL>
```
아래 사이트에서 다운로드 URL 확인 후, wget 명령어 이용

- [The Oxford-IIIT Pet Dataset](http://www.robots.ox.ac.uk/~vgg/data/pets/)
```
curl -O http://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz
curl -O http://www.robots.ox.ac.uk/~vgg/data/pets/data/a
```
- [Stanford 40 Actions](http://vision.stanford.edu/Datasets/40actions.html)
- [Google Open Images dataset v4](https://storage.googleapis.com/openimages/web/index.html)
  - 신체 관련 : Human body, Human foot, Human leg, Human ear, Human hair, Human head, Human face, Human arm, Human nose, Human hand, Human eye, Human beard, Human mouth
- [MS COCO](http://cocodataset.org/#home)
-------

#### Face recognition
- [face-rec](http://www.face-rec.org/databases/)
  - CAFE - The Child Affective Face Set (아이 얼굴, 감정 인식 이미지)

- [DogCentric Activity Dataset](http://robotics.ait.kyushu-u.ac.jp/yumi/db/first_dog.html)
  - 10 types of dog activity : Ball play, Car, Drink, Feed, Turn head, Pet, Body shake, Sniff, Walk
    
-------

#### Bounding Box & Labeling tool
- [다크 프로그래머 :: DarkLabel1.3 - 이미지/비디오 객체 레이블링 툴 (Image Labeling and Annotation Tool)](http://darkpgmr.tistory.com/16)