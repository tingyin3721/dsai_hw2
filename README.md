# Addition / Subtraction / Multiplication

## 1. Description
 - Adder (A,B: 3 digits)
 - Subtractor (A-B, A>=B)
 - Combine adder and subtractor (A+B-C or A-B+C)
 - Multiplier (A,B: 3 digits)
 - **Analyze the results under training epoch, training size, different number of digits, more input number**

## 2. Flow
**Data Representation**
 - char vocabulary : "0,1,2,3,4,5,6,7,8,9,+/-,' '"
 - length of the sequence
 - one-hot encoding
 - digital-token decoding

**Data Generation**
 - Generate some question-answer pairs for training and validating.
 - Questions : ['125+496', '23+987', '178+63', '45+12', '86+613']
 - Answer :    ['621', '1010', '241', '57', '699']

**Feature Engineering**
 - Transfer the training sets to one-hot representation.
 - 

**Get Training Data and Validation Data**
 - Total data = 50000, 45000 for training, 5000 for validation

**Build Model**
 - Implement with LSTM
 - Hidden Layers = 128
 - 

**String Matching**


## 3. Result


## 4. 檔案說明