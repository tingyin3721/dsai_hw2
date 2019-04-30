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

**Get Training Data and Validation Data**
 - Total data = 50000, 45000 for training, 5000 for validation

**Build Model**
 - Implement with LSTM
 - Hidden Layers = 128
 - Batch Size = 128 / 64 / 256
 - Optimizer : adam
 - Loss Function : categorical_crossentropy
 - Epoch = 100 / 200

**String Matching**
 - When we train our model with the generated datasets, the matching accuracy will gradually increase.
 
**Testing**
 - Generate testing data = 1000
 - Visualize the first 10 data when testing
 - Print out the testing accuracy
 
**Other Discussion**
 - **每個.ipynb檔皆實驗了以下五種不同條件的training**
 - 1.1 實驗使用不同的epoch和batch size訓練 (with batch size = 64, epoch = 100)
 - 1.2 實驗使用不同的epoch和batch size訓練 (with batch size = 256, epoch = 100)
 - 1.3 實驗使用不同的epoch和batch size訓練 (with batch size = 128, epoch = 200)
 - 2. 實驗不同位數的數字 (The digits of input number = 4)
 - 3. 多組數字共同運算 (Add 3 numbers (each number has 3 digits) together)

## 3. Result


## 4. 檔案說明
 - addition_rnn.ipynb : 實現加法器
 - Subtraction_rnn.ipynb : 實現減法器
 - Addition_Subtraction_rnn.ipynb : 加法器混合減法器 (A+B-C or A-B+C)
 - Multiplication_rnn.ipynb : 實現乘法器