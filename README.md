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

## Model Architecture 

This is a compact architectural model with two channels. For channel A, I using ```three layer``` include Conv1D - MaxPooling - LSTM. And for channel B, I using ```two layer``` LSTM. With extremely large data sets, the model can scale with ```multiple channels``` and ```multiple layers``` to be able to respond to the size of the dataset.

![image](https://user-images.githubusercontent.com/31820707/232202832-d5bf67ec-4163-40df-94bb-aad69f905e1b.png)

## Datasets

[XSS Dataset](https://www.kaggle.com/datasets/syedsaqlainhussain/cross-site-scripting-xss-dataset-for-deep-learning)

[SQL Injection Dataset](https://www.kaggle.com/datasets/syedsaqlainhussain/sql-injection-dataset)

## Data Processing

From the input input, I transform the characters into corresponding integers and pad these numbers into a one-dimensional vector with ```n``` columns.

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

```
Epoch 1/5
172/172 [==============================] - 29s 102ms/step - loss: 0.1528 - accuracy: 0.9398 - val_loss: 0.0452 - val_accuracy: 0.9874
Epoch 2/5
172/172 [==============================] - 17s 100ms/step - loss: 0.0297 - accuracy: 0.9917 - val_loss: 0.0383 - val_accuracy: 0.9900
Epoch 3/5
172/172 [==============================] - 16s 96ms/step - loss: 0.0212 - accuracy: 0.9937 - val_loss: 0.0445 - val_accuracy: 0.9883
Epoch 4/5
172/172 [==============================] - 17s 99ms/step - loss: 0.0161 - accuracy: 0.9950 - val_loss: 0.0322 - val_accuracy: 0.9921
Epoch 5/5
172/172 [==============================] - 16s 93ms/step - loss: 0.0132 - accuracy: 0.9964 - val_loss: 0.0310 - val_accuracy: 0.9940
```

## Model Evaludation

```
172/172 [==============================] - 6s 32ms/step - loss: 0.0310 - accuracy: 0.9940
172/172 [==============================] - 6s 25ms/step
Accuracy: 99.40%
              precision    recall  f1-score   support

           0       0.99      1.00      0.99      2553
           1       1.00      0.99      0.99      2922

    accuracy                           0.99      5475
   macro avg       0.99      0.99      0.99      5475
weighted avg       0.99      0.99      0.99      5475
```

| Chart Loss | Chart Accuracy  |
|---|---|
| ![image](https://user-images.githubusercontent.com/31820707/232202923-ee412392-a9ab-407f-b09c-a8ea1737fb41.png) | ![image](https://user-images.githubusercontent.com/31820707/232202935-8e789f88-d0e7-48e6-b511-9a2d1c7d8c0e.png) | 


