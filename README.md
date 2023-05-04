# Project: Bird Species Classifier
This project aims to classify two bird species 'Psilopogon nuchalis' and 'Pycnonotus sinensis' accurately, with which is based on the images I provided. Due to low level devices, the file posted on GitHub can only demonstrated a dataset size of 311. However, this project is designed to contain considerable images and therefore database and cluster method are applied to tackle with situations of large sample size.

This a photo of 'Psilopogon nuchalis', provided from myself.(also known as Taiwan barbet)
![image](6B1A0315.JPG)
This a photo of 'Pycnonotus sinensis', provided from myself.
![image](6B1A2900.JPG)

## Instruction
Since the image dataset is under maintenance, it is not available to enclose it with this project on GitHub. However, if interested, readers are encouraged to download the .ipynb file I provided with and utilize it with your own dataset. 

Moreover, if the readers want to give my model a try, there is a sample code if you download 'model_v2.h5' and try it with python code:
```py
   import cv2
   import tensorflow as tf
   import numpy as np
   
   model = tf.keras.models.load_model('model_v1.h5')
   
   def img_read(path):
    img = cv2.imread(path)
    img = cv2.resize(img,(256,256))
    img = np.expand_dims(img,axis=0)
    img = img/255.
    return img


   def predict_img(path,model):
    img = img_read(path)
    predict = model_Kmeans.predict(img)
    predicted_class =np.argmax(predict,axis=1)

    if(predicted_class[0] == 1):
        print("This is Pycnonotus sinensis!")
    else:
        print("This is Psilopogon nuchalis!")
   
   image = read_img(path_you_provide)
   predict_img
```
This is an attempt using 'model_v2.h5' and a image of Pycnonotus sinensis from myself (not used in training):
![image](20228079.jpeg)
```py
   model_Kmeans =  tf.keras.models.load_model('model_v2.h5')
   predict_img('/Users/wuguanxun/Desktop/20228079.jpeg',model_Kmeans)
```
The result is 
```py
   >>> 1/1 [==============================] - 0s 9ms/step
   >>> This is Pycnonotus sinensis!
```
## Database
We expect to introduce two databases into this project. MongoDB is implemented owing to its outstanding extendability and we store images and labels here. MySQL is planned to be used to collect metadata from images thereselves; however, I did not put it in use since the image data itself is the core I want to process.

## Method
Since I expect to afford large image data when conditions are available, label propagation with K-Means is used to pick samples that are more representative. After selecting quality samples, we input our images data (256x256x3) into CNN.

## Performance
The performances on two dataset(the reduced dataset and the entire dataset) are almost identically perfect. However, it is worth noticing that CNN with the reduced dataset use less epoch to accomplish the task whereas the entire dataset use more epoches and more time per epoch. When we enlarge the dataset, the difference will become more significant.

The performance of models of full dataset and reduced dataset is shown as below, respectively:
![image](model1.png)
![image](model2.png)
