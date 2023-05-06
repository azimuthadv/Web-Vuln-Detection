# Web-Vuln-Detection
Deep Learning - Web Application Vulnerabilities Detection

## Description
This is a detection method that using combine Convolutional Neural Network (CNN) and Long short-term memory (LSTM) to analyze features and relationships in requests from users and predict whether they are vulnerability or not.

## Vulnerabilities Detection 

### Injections

- [x] Cross-Site Scripting
- [x] SQL Injection
- [ ] JSON & XML Injection
- [ ] Path Traversal
- [ ] Command Injection

## Model Architecture 

This is a compact architectural model with two channels. For channel A, I using ```four layer``` include Conv1D - MaxPooling - LSTM - LSTM. And for channel B, I using ```two layer``` LSTM. With extremely large data sets, the model can scale with ```multiple channels``` and ```multiple layers``` to be able to respond to the size of the dataset.

![image](https://user-images.githubusercontent.com/31820707/232204671-2010562e-9f42-4a73-b754-8a8b13141c7d.png)

## Datasets
The training dataset is split 80:20 for training and testing. With 80% of the district training, I use k-fold cross validation with `k=5` to train the model.

![image](https://user-images.githubusercontent.com/31820707/236610797-a69f20d4-0d96-4f05-a9e8-5e6b28552926.png)

| Vuln Type | Sample | Access | 
|---|---|---|
| Cross-site scripting | 13686 | [Public](https://www.kaggle.com/datasets/syedsaqlainhussain/cross-site-scripting-xss-dataset-for-deep-learning) |
| Sql Injection | 30919 | [Public](https://www.kaggle.com/datasets/syedsaqlainhussain/sql-injection-dataset) |
| Generate Dataset | 57060 | Private |

## Data Decoder
The decoder was built with multiple decode layers including `base64` - `URL` - `Unicode` - `utf8` - `clean data` - `...`. 

| Original | Decoded | 
|---|---|
| ```<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></object>``` | ```<objectdata="data:text/html;base64,<script>alert(1)</script>"></object>```|

## Data Processing

From the input, I transform the characters into corresponding integers and do post-padding these numbers into a one-dimensional vector with ```n``` columns.

Data before processing : ```<isindex id=x tabindex=1 onbeforedeactivate=alert(1)></isindex><input autofocus>``` 

Data after processing : ```[20  8 18 15 23 64 19 19 15 14 20  8 18 15 23 64 19 19 15 14 20  8 18 15
 23 64 19 19 15 14 20  8 18 15 23 64 19 19 15 14 20  8 18 15 23 64 19 19
 15 14 20  8 18 15 23 64 19 19 15 14 20  8 18 15 23 64 19 19 15 14 20  8
 18 15 23 64 19 19 15 14 20  8 18 15 23 64 19 19 15 14 20  8 18 15 23 64
 19 19 15 14 20  8 18 15 23 64 19 19 15 14 20  8 18 15 23 64 19 19 15 14
 ... ]```

## Model Summary

Total params: 2,586,017

Trainable params: 2,580,417

Non-trainable params: 5,600

## Model Train

### For public dataset

```
Fold 1
Epoch 1/5
137/137 [==============================] - 22s 110ms/step - loss: 0.1773 - accuracy: 0.9247 - val_loss: 0.1028 - val_accuracy: 0.9642
Epoch 2/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0309 - accuracy: 0.9905 - val_loss: 0.0407 - val_accuracy: 0.9886
Epoch 3/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0207 - accuracy: 0.9945 - val_loss: 0.0326 - val_accuracy: 0.9911
Epoch 4/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0211 - accuracy: 0.9933 - val_loss: 0.0291 - val_accuracy: 0.9938
Epoch 5/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0111 - accuracy: 0.9969 - val_loss: 0.0352 - val_accuracy: 0.9922
Fold 2
Epoch 1/5
137/137 [==============================] - 21s 109ms/step - loss: 0.1845 - accuracy: 0.9254 - val_loss: 0.0384 - val_accuracy: 0.9877
Epoch 2/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0261 - accuracy: 0.9933 - val_loss: 0.0316 - val_accuracy: 0.9911
Epoch 3/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0183 - accuracy: 0.9949 - val_loss: 0.0174 - val_accuracy: 0.9954
Epoch 4/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0119 - accuracy: 0.9969 - val_loss: 0.0211 - val_accuracy: 0.9954
Epoch 5/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0064 - accuracy: 0.9983 - val_loss: 0.0204 - val_accuracy: 0.9952
Fold 3
Epoch 1/5
137/137 [==============================] - 23s 113ms/step - loss: 0.2259 - accuracy: 0.9196 - val_loss: 0.0426 - val_accuracy: 0.9881
Epoch 2/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0315 - accuracy: 0.9921 - val_loss: 0.0260 - val_accuracy: 0.9943
Epoch 3/5
137/137 [==============================] - 14s 105ms/step - loss: 0.0177 - accuracy: 0.9954 - val_loss: 0.0260 - val_accuracy: 0.9913
Epoch 4/5
137/137 [==============================] - 13s 96ms/step - loss: 0.0128 - accuracy: 0.9963 - val_loss: 0.0229 - val_accuracy: 0.9934
Epoch 5/5
137/137 [==============================] - 13s 95ms/step - loss: 0.0110 - accuracy: 0.9969 - val_loss: 0.0198 - val_accuracy: 0.9950
Fold 4
Epoch 1/5
137/137 [==============================] - 22s 108ms/step - loss: 0.1900 - accuracy: 0.9208 - val_loss: 0.0345 - val_accuracy: 0.9895
Epoch 2/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0273 - accuracy: 0.9922 - val_loss: 0.0275 - val_accuracy: 0.9934
Epoch 3/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0175 - accuracy: 0.9951 - val_loss: 0.0263 - val_accuracy: 0.9941
Epoch 4/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0117 - accuracy: 0.9968 - val_loss: 0.0239 - val_accuracy: 0.9950
Epoch 5/5
137/137 [==============================] - 13s 96ms/step - loss: 0.0074 - accuracy: 0.9982 - val_loss: 0.0283 - val_accuracy: 0.9943
Fold 5
Epoch 1/5
137/137 [==============================] - 24s 118ms/step - loss: 0.2132 - accuracy: 0.9240 - val_loss: 0.0349 - val_accuracy: 0.9918
Epoch 2/5
137/137 [==============================] - 13s 98ms/step - loss: 0.0285 - accuracy: 0.9924 - val_loss: 0.0278 - val_accuracy: 0.9920
Epoch 3/5
137/137 [==============================] - 13s 97ms/step - loss: 0.0183 - accuracy: 0.9954 - val_loss: 0.0304 - val_accuracy: 0.9925
Epoch 4/5
137/137 [==============================] - 13s 96ms/step - loss: 0.0109 - accuracy: 0.9974 - val_loss: 0.0239 - val_accuracy: 0.9936
Epoch 5/5
137/137 [==============================] - 13s 96ms/step - loss: 0.0082 - accuracy: 0.9980 - val_loss: 0.0230 - val_accuracy: 0.9941
Training score: 0.5016 +/- 0.4973
Validation score: 0.5098 +/- 0.4844
```

### For private dataset

```
Fold 1
Epoch 1/5
286/286 [==============================] - 36s 102ms/step - loss: 0.1607 - accuracy: 0.9372 - val_loss: 0.0853 - val_accuracy: 0.9713
Epoch 2/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0749 - accuracy: 0.9748 - val_loss: 0.0840 - val_accuracy: 0.9745
Epoch 3/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0542 - accuracy: 0.9812 - val_loss: 0.0642 - val_accuracy: 0.9772
Epoch 4/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0521 - accuracy: 0.9821 - val_loss: 0.0630 - val_accuracy: 0.9800
Epoch 5/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0389 - accuracy: 0.9863 - val_loss: 0.0960 - val_accuracy: 0.9687
Fold 2
Epoch 1/5
286/286 [==============================] - 37s 103ms/step - loss: 0.1531 - accuracy: 0.9414 - val_loss: 0.0605 - val_accuracy: 0.9792
Epoch 2/5
286/286 [==============================] - 27s 95ms/step - loss: 0.0519 - accuracy: 0.9833 - val_loss: 0.0459 - val_accuracy: 0.9855
Epoch 3/5
286/286 [==============================] - 27s 95ms/step - loss: 0.0361 - accuracy: 0.9881 - val_loss: 0.0410 - val_accuracy: 0.9851
Epoch 4/5
286/286 [==============================] - 28s 97ms/step - loss: 0.0275 - accuracy: 0.9905 - val_loss: 0.0487 - val_accuracy: 0.9881
Epoch 5/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0278 - accuracy: 0.9902 - val_loss: 0.0380 - val_accuracy: 0.9872
Fold 3
Epoch 1/5
286/286 [==============================] - 37s 104ms/step - loss: 0.1869 - accuracy: 0.9254 - val_loss: 0.0852 - val_accuracy: 0.9734
Epoch 2/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0581 - accuracy: 0.9820 - val_loss: 0.0533 - val_accuracy: 0.9826
Epoch 3/5
286/286 [==============================] - 29s 103ms/step - loss: 0.0379 - accuracy: 0.9870 - val_loss: 0.0470 - val_accuracy: 0.9844
Epoch 4/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0314 - accuracy: 0.9890 - val_loss: 0.0558 - val_accuracy: 0.9821
Epoch 5/5
286/286 [==============================] - 27s 95ms/step - loss: 0.0249 - accuracy: 0.9908 - val_loss: 0.0530 - val_accuracy: 0.9848
Fold 4
Epoch 1/5
286/286 [==============================] - 40s 112ms/step - loss: 0.1689 - accuracy: 0.9370 - val_loss: 0.0698 - val_accuracy: 0.9747
Epoch 2/5
286/286 [==============================] - 28s 97ms/step - loss: 0.0563 - accuracy: 0.9824 - val_loss: 0.0484 - val_accuracy: 0.9847
Epoch 3/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0385 - accuracy: 0.9876 - val_loss: 0.0514 - val_accuracy: 0.9823
Epoch 4/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0309 - accuracy: 0.9899 - val_loss: 0.0434 - val_accuracy: 0.9855
Epoch 5/5
286/286 [==============================] - 30s 104ms/step - loss: 0.0250 - accuracy: 0.9915 - val_loss: 0.0375 - val_accuracy: 0.9871
Fold 5
Epoch 1/5
286/286 [==============================] - 39s 112ms/step - loss: 0.1774 - accuracy: 0.9286 - val_loss: 0.0882 - val_accuracy: 0.9705
Epoch 2/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0592 - accuracy: 0.9814 - val_loss: 0.0490 - val_accuracy: 0.9827
Epoch 3/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0411 - accuracy: 0.9862 - val_loss: 0.0403 - val_accuracy: 0.9870
Epoch 4/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0333 - accuracy: 0.9884 - val_loss: 0.0389 - val_accuracy: 0.9871
Epoch 5/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0248 - accuracy: 0.9908 - val_loss: 0.0423 - val_accuracy: 0.9873
Training score: 0.5081 +/- 0.4818
Validation score: 0.5182 +/- 0.4651
```

## Model Evaludation

### For public dataset

```
172/172 [==============================] - 5s 30ms/step - loss: 0.0292 - accuracy: 0.9949
172/172 [==============================] - 7s 34ms/step
Accuracy: 99.49%
              precision    recall  f1-score   support

           0       0.99      1.00      0.99      2553
           1       1.00      0.99      1.00      2922

    accuracy                           0.99      5475
   macro avg       0.99      1.00      0.99      5475
weighted avg       0.99      0.99      0.99      5475
```


| Chart Loss | Chart Accuracy  |
|---|---|
| ![image](https://user-images.githubusercontent.com/31820707/236609306-4c7004a2-087e-4b10-8af5-9dc2fc84b049.png) | ![image](https://user-images.githubusercontent.com/31820707/236609319-d026182b-57e0-4b4f-977f-4aee1c72fee8.png) |

### For private dataset

```
357/357 [==============================] - 12s 34ms/step - loss: 0.0406 - accuracy: 0.9887
357/357 [==============================] - 13s 32ms/step
Accuracy: 98.87%
              precision    recall  f1-score   support

           0       0.99      1.00      0.99      6487
           1       0.99      0.98      0.99      4925

    accuracy                           0.99     11412
   macro avg       0.99      0.99      0.99     11412
weighted avg       0.99      0.99      0.99     11412
```

| Chart Loss | Chart Accuracy  |
|---|---|
| ![image](https://user-images.githubusercontent.com/31820707/236611064-4daea2f7-bc0a-43a2-a0fb-7e7deec0a8e4.png) | ![image](https://user-images.githubusercontent.com/31820707/236611074-3778bf4a-06cf-4d49-be47-066edcd1ab28.png) | 

## Model Retrain
Scenario: Model with public dataset re-train with the private dataset

```
Fold 1
Epoch 1/5
286/286 [==============================] - 38s 111ms/step - loss: 0.1264 - accuracy: 0.9587 - val_loss: 0.0795 - val_accuracy: 0.9749
Epoch 2/5
286/286 [==============================] - 28s 97ms/step - loss: 0.0606 - accuracy: 0.9800 - val_loss: 0.0681 - val_accuracy: 0.9797
Epoch 3/5
286/286 [==============================] - 28s 97ms/step - loss: 0.0455 - accuracy: 0.9848 - val_loss: 0.0492 - val_accuracy: 0.9838
Epoch 4/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0332 - accuracy: 0.9889 - val_loss: 0.0444 - val_accuracy: 0.9860
Epoch 5/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0274 - accuracy: 0.9896 - val_loss: 0.0670 - val_accuracy: 0.9785
Fold 2
Epoch 1/5
286/286 [==============================] - 39s 114ms/step - loss: 0.0290 - accuracy: 0.9897 - val_loss: 0.0232 - val_accuracy: 0.9898
Epoch 2/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0235 - accuracy: 0.9910 - val_loss: 0.0238 - val_accuracy: 0.9899
Epoch 3/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0213 - accuracy: 0.9910 - val_loss: 0.0298 - val_accuracy: 0.9881
Epoch 4/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0204 - accuracy: 0.9923 - val_loss: 0.0286 - val_accuracy: 0.9880
Fold 3
Epoch 1/5
286/286 [==============================] - 35s 102ms/step - loss: 0.0206 - accuracy: 0.9914 - val_loss: 0.0179 - val_accuracy: 0.9931
Epoch 2/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0179 - accuracy: 0.9924 - val_loss: 0.0150 - val_accuracy: 0.9938
Epoch 3/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0148 - accuracy: 0.9934 - val_loss: 0.0159 - val_accuracy: 0.9933
Epoch 4/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0129 - accuracy: 0.9939 - val_loss: 0.0169 - val_accuracy: 0.9930
Epoch 5/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0142 - accuracy: 0.9937 - val_loss: 0.0202 - val_accuracy: 0.9926
Fold 4
Epoch 1/5
286/286 [==============================] - 38s 111ms/step - loss: 0.0139 - accuracy: 0.9938 - val_loss: 0.0113 - val_accuracy: 0.9938
Epoch 2/5
286/286 [==============================] - 30s 103ms/step - loss: 0.0126 - accuracy: 0.9937 - val_loss: 0.0123 - val_accuracy: 0.9944
Epoch 3/5
286/286 [==============================] - 30s 104ms/step - loss: 0.0141 - accuracy: 0.9935 - val_loss: 0.0138 - val_accuracy: 0.9939
Epoch 4/5
286/286 [==============================] - 28s 96ms/step - loss: 0.0110 - accuracy: 0.9945 - val_loss: 0.0152 - val_accuracy: 0.9928
Fold 5
Epoch 1/5
286/286 [==============================] - 39s 110ms/step - loss: 0.0146 - accuracy: 0.9931 - val_loss: 0.0119 - val_accuracy: 0.9924
Epoch 2/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0122 - accuracy: 0.9942 - val_loss: 0.0112 - val_accuracy: 0.9947
Epoch 3/5
286/286 [==============================] - 27s 96ms/step - loss: 0.0108 - accuracy: 0.9946 - val_loss: 0.0111 - val_accuracy: 0.9952
Epoch 4/5
286/286 [==============================] - 29s 103ms/step - loss: 0.0106 - accuracy: 0.9947 - val_loss: 0.0160 - val_accuracy: 0.9923
Epoch 5/5
286/286 [==============================] - 30s 105ms/step - loss: 0.0103 - accuracy: 0.9944 - val_loss: 0.0177 - val_accuracy: 0.9912
Training score: 0.5046 +/- 0.4884
Validation score: 0.5092 +/- 0.4797
```

```
357/357 [==============================] - 12s 34ms/step - loss: 0.0365 - accuracy: 0.9883
357/357 [==============================] - 13s 29ms/step
Accuracy: 98.83%
              precision    recall  f1-score   support

           0       0.99      0.99      0.99      6487
           1       0.98      0.99      0.99      4925

    accuracy                           0.99     11412
   macro avg       0.99      0.99      0.99     11412
weighted avg       0.99      0.99      0.99     11412
```

| Chart Loss | Chart Accuracy  |
|---|---|
| ![image](https://user-images.githubusercontent.com/31820707/236615674-63636b0d-f21c-4049-800b-a82233cea925.png) | ![image](https://user-images.githubusercontent.com/31820707/236615684-4d395098-f7d2-4a76-b102-adc11128b9a3.png) | 

## Model Predict

I have developed a simple website so you can check out the model here: https://noobpk.github.io/Web-Vuln-Detection/
