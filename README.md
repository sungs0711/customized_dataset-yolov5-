# yolov5

# download data set
!curl -L "https://public.roboflow.com/ds/gpO8CtAgc3?key=bu9xmHqjij" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip

# make dir 'dataset'
downloaded files move to folder 'dataset'

# git cloning
https://github.com/ultralytics/yolov5.git

# install packages for yolov5
pip install -r requirements.txt

# change path
from glob import glob

img_list = glob('/content/dataset/export/images/*.jpg')

# split train/valid data
from sklearn.model_selection import train_test_split

train_img_list, val_img_list = train_test_split(img_list, test_size=0.2, random_state=2000)

# save image path as .txt
with open('/content/dataset/train.txt','w')as f:

  f.write('\n'.join(train_img_list))

with open('/content/dataset/val.txt','w')as f:

  f.write('\n'.join(val_img_list))

# 
