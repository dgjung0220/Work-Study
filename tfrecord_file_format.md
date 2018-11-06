### TF Record File Format

[조대협의 블로그 :: 텐서플로우 트레이닝 데이타 포맷인 *.tfrecord 파일 읽고 쓰기](http://bcho.tistory.com/1190?category=555440) 참고

TFRecord에 저장되는 내용들:
- 이미지 높이, 너비 (height, width)
- 파일명 (filename)
- 인코딩 포맷 (format)
- 이미지 바이너리 (encoded)
- bounding box 위치 (xmin, ymin, xmax, ymax



#### Error 1 
``
TypeError: 'jpg' has type <class 'str'>, but expected one of: ((<class 'bytes'>,),)
``
리눅스에서는 string 타입을 그냥 써도 되지만, 윈도우에서는 'str' 타입을 bytes로 변경해주어야 한다. 에러가 난 코드에서 'str' 형태의 string 타입을 쓰고 있다면 이를  b'str' 처럼 앞에 b를 붙어 bytes 타입으로 캐스팅하면 된다.