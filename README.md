# Coding-Raja-Technologies-Internshiimport numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.metrics import precision_score,recall_score,f1_score

fraud_data = pd.read_csv('C:/Users/GOURANG/Desktop/Fraud Detection/Fraud detection.csv')

fraud_data.head()

fraud_data.tail()

fraud_data.info()

fraud_data.isnull().sum()

fraud_data['Class'].value_counts()

fraud_data['Class'].value_counts()

legit = fraud_data[fraud_data.Class == 0]
fraud = fraud_data[fraud_data.Class == 1]

print(legit.shape)
print(fraud.shape)

legit.Amount.describe()

fraud.Amount.describe()

fraud_data.groupby('Class').mean()

legit_sample = legit.sample(n=492)

new_dataset = pd.concat([legit_sample, fraud], axis=0)

new_dataset.head()

new_dataset.tail()

new_dataset['Class'].value_counts()

new_dataset.groupby('Class').mean()

X = new_dataset.drop(columns='Class', axis=1)
Y = new_dataset['Class']

print(X)

print(Y)

X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, stratify=Y, random_state=2)

print(X.shape, X_train.shape, X_test.shape)

model = LogisticRegression()

model.fit(X_train, Y_train)

X_train_prediction = model.predict(X_train)
training_data_accuracy = accuracy_score(X_train_prediction, Y_train)

print('Accuracy on Training data : ', training_data_accuracy)

X_test_prediction = model.predict(X_test)
test_data_accuracy = accuracy_score(X_test_prediction, Y_test)

print('Accuracy score on Test Data : ', test_data_accuracy)

precision_score(Y_test,X_test_prediction)
print('Precision score on Test Data : ', precision_score(Y_test,X_test_prediction))

recall_score(Y_test,X_test_prediction)
print('Recall score on Test Data : ', recall_score(Y_test,X_test_prediction))

f1_score(Y_test,X_test_prediction)
print('F1 score on Test Data : ', f1_score(Y_test,X_test_prediction))
