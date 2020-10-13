# YOLO V5
## Download data set

`!curl -L "https://public.roboflow.com/ds/gpO8CtAgc3?key=bu9xmHqjij" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip`
![](https://i.imgur.com/vX7WoRO.png)

------------
## Make folder 'dataset'
> downloaded files move to folder 'dataset'

------------

## Git cloning
> https://github.com/ultralytics/yolov5.git

------------
## Install packages for yolov5
`cd yolov5`
> pip install -r requirements.txt

------------
## Change path
    from glob import glob
    
    img_list = glob('/content/dataset/export/images/*.jpg')

------------
## Split train/valid data
    from sklearn.model_selection import train_test_split
    
    train_img_list, val_img_list = train_test_split(img_list, test_size=0.2, random_state=2000)

------------

## Save image path as .txt
    with open('/content/dataset/train.txt','w')as f:
    
    	f.write('\n'.join(train_img_list))
    
    with open('/content/dataset/val.txt','w')as f:
    
    	f.write('\n'.join(val_img_list))

------------

## Modify 'yaml'
    import yaml
	
    with open('/content/dataset/data.yaml','r') as f:
      data = yaml.load(f)
    
    data['train'] = '/content/dataset/train.txt'
    data['val'] = '/content/dataset/val.txt'
	
    with open('/content/dataset/data.yaml','w') as f:
      yaml.dump(data,f)


------------

## Training
    python train.py --img 416 --batch 16 --epochs 50 --data /content/dataset/data.yaml --cfg ./models/yolov5s.yaml --weights yolov5s.pt --name gun_yolov5s_results

------------

## Prediction & Inference
    from IPython.display import Image
    import os
    
    val_img_path = val_img_list[1]
    
    #inference
    python detect.py --weights /content/yolov5/runs/exp0_gun_yolov5s_results/weights/best.pt --img 416 --conf 0.5 --source "{val_img_path}"
    
    #save output
    Image(os.path.join('/content/yolov5/inference/output',os.path.basename(val_img_path)))

------------

## Result
![](https://blog.roboflow.ai/content/images/2020/02/detection.gif)
