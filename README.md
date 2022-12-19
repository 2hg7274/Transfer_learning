# Transfer_learning(전이학습)이란?  

데이콘 커뮤니티에 올라온 전이학습 실습 자료에 대한 코드  
사이트: [https://dacon.io/forum/405988?page=1&dtype=recent&fType](https://dacon.io/forum/405988?page=1&dtype=recent&fType)

</br>  

데이터셋: [Kaggle Competition Dogs vs Cats](https://www.kaggle.com/c/dogs-vs-cats) 에서 다운.  


```python
# zip 파일 압축 풀기
import zipfile

original_base_dir = '/Transfer Learning/datasets'
os.mkdir(original_base_dir)
dataset_zip = zipfile.ZipFile('/Transfer Learning/dogs-vs-cats/test1.zip')
dataset_zip.extractall(original_base_dir)
dataset_zip.close()

dataset_zip = zipfile.ZipFile('/Transfer Learning/dogs-vs-cats/train.zip')
dataset_zip.extractall(original_base_dir)
dataset_zip.close()
```  
강아지/고양이 각각 1000개의 훈련, 500개의 검증, 500개의 테스트 세트로 데이터 분할.  
```python
# 폴더 생성
import os, shutil

original_dataset_dir = '/Transfer Learning/datasets/train'
base_dir = '/Transfer Learning/datasets_small'
os.mkdir(base_dir)

train_dir = osp.join(base_dir, 'train')
os.mkdir(train_dir)
val_dir = osp.join(base_dir, 'val')
os.mkdir(val_dir)
test_dir = osp.join(base_dir, 'test')
os.mkdir(test_dir)

train_cats_dir = osp.join(train_dir, 'cats')
os.mkdir(train_cats_dir)
train_dogs_dir = osp.join(train_dir, 'dogs')
os.mkdir(train_dogs_dir)

val_cats_dir = osp.join(val_dir, 'cats')
os.mkdir(val_cats_dir)
val_dogs_dir = osp.join(val_dir, 'dogs')
os.mkdir(val_dogs_dir)

test_cats_dir = osp.join(test_dir, 'cats')
os.mkdir(test_cats_dir)
test_dogs_dir = osp.join(test_dir, 'dogs')
os.mkdir(test_dogs_dir)
```  
```python
# 고양이
fnames = ['cat.{}.jpg'.format(i) for i in range(1000)]
for fname in fnames:
    src = osp.join(original_dataset_dir, fname)
    dst = osp.join(train_cats_dir, fname)
    shutil.copyfile(src, dst)

fnames = ['cat.{}.jpg'.format(i) for i in range(1000, 1500)]
for fname in fnames:
    src = osp.join(original_dataset_dir, fname)
    dst = osp.join(val_cats_dir, fname)
    shutil.copyfile(src, dst)

fnames = ['cat.{}.jpg'.format(i) for i in range(1500, 2000)]
for fname in fnames:
    src = osp.join(original_dataset_dir, fname)
    dst = osp.join(test_cats_dir, fname)
    shutil.copyfile(src, dst)
```  
```python 
# 강아지
fnames = ['dog.{}.jpg'.format(i) for i in range(1000)]
for idx, fname in enumerate(fnames) :
  src = osp.join(original_dataset_dir, f'dog.{idx}.jpg')
  dst = osp.join(train_dogs_dir, fname)
  shutil.copyfile(src, dst)

fnames = ['dog.{}.jpg'.format(i) for i in range(1000, 1500)]
for fname in fnames :
  src = osp.join(original_dataset_dir, fname)
  dst = osp.join(val_dogs_dir, fname)
  shutil.copyfile(src, dst)
  
fnames = ['dog.{}.jpg'.format(i) for i in range(1500, 2000)]
for fname in fnames :
  src = osp.join(original_dataset_dir, fname)
  dst = osp.join(test_dogs_dir, fname)
  shutil.copyfile(src, dst)
```  

코드 수행 후 만들어지는 폴더 형태
```
datasets/
  test1/
  train/
datasets_small/
  test/
    cats/
    dogs/
  train/
    cats/
    dogs/
  val/
    cats/
    dogs/
```  
