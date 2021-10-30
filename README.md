https://aws.amazon.com/

로그인

EC2 인스턴스 시작

key 다운로드

putty 설정(key 위치, ip 등)

putty 실행

'ubuntu' 계정으로 들어감(w 권한이 있는 계정)



`home/ubuntu` 경로에서 시작! (ubuntu(계정명) 디렉터리)



---

### Setting

> 박스 안에 있는 코드를 putty 창(리눅스 커맨드 창)에 순서대로 입력하면 됨



가상환경 목록 보기

```
conda info --envs
```



가상환경 clone

```
conda create -n [env-name] --clone [src-env-name]
```



가상환경 삭제 방법(optional)

​	가상환경 만들다가 뭐 문제 생기면, 이 방법으로 지웠다가 다시 생성

```
conda remove --name yolov5 --all
```



```
mkdir dataset
cd dataset
```

현재위치 home/ubuntu/dataset/



yaml 카피

```
cd ..
cp ./yolov5/data/coco128.yaml ./dataset/data.yaml
cd dataset
```

현재위치 home/ubuntu/dataset/



coco dataset (image & annotation) download

```
wget images.cocodataset.org/zips/train2017.zip
wget images.cocodataset.org/zips/val2017.zip
wget images.cocodataset.org/zips/test2017.zip
wget images.cocodataset.org/annotations/annotations_trainval2017.zip
wget images.cocodataset.org/annotations/stuff_annotations_trainval2017.zip
wget images.cocodataset.org/annotations/panoptic_annotations_trainval2017.zip
```



```
mkdir images
mkdir labels
cd images
mkdir train
mkdir val
cd ..
cd labels
mkdir train
mkdir val
mkdir test
cd ..
```

현재위치 home/ubuntu/dataset



```
unzip train2017.zip -d ./images
unzip val2017.zip -d ./images
unzip test2017.zip -d ./images
unzip annotations_trainval2017.zip
```



디렉터리명 변경

```
cd images
mv train2017 train
mv val2017 val
mv test2017 test
cd ..
```

현재위치 home/ubuntu/dataset



coco annotation 파일을 yolo annotation 형식으로 변환하는 코드 다운로드

```
wget https://github.com/RTalha/COCOTOYOLO-Annotations/raw/main/cocotoyolo.jar
```

cocotoyolo.jar를 실행 -> "json file(annotations) path" "image path" "class" "save path"

```
java -jar cocotoyolo.jar "annotations/instances_train2017.json" "images/train/" "bottle, laptop" "labels/train"
```

```
java -jar cocotoyolo.jar "annotations/instances_val2017.json" "images/val/" "bottle, laptop" "labels/val"
```

<ubuntu>

yolov5

dataset

​	└ data.yaml

​	└ cocotoyolo.jar

​	└ images

​			└ train : .jpg

​			└ val : .jpg

​			└ test .jpg

​	└ labels

​			└ train : .txt

​			└ val : .txt

​			└ test : NaN



--- 일단 여기까지 세팅... 나머지는 이어서

