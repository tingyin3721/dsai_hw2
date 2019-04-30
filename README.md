# Addition / Subtraction / Multiplication

## jupyter link
 - Addition : https://nbviewer.jupyter.org/gist/tingyin3721/aad44ae50a470afc42a2ce7eafbea208
 - Subtraction : https://nbviewer.jupyter.org/gist/tingyin3721/34894154b47aa9c3522e9d0509b5f578
 - Addition_Subtraction_Combine : https://nbviewer.jupyter.org/gist/tingyin3721/241a06e2c2f94db6b754f1ec24df8772
 - Multiplication : https://nbviewer.jupyter.org/gist/tingyin3721/21aa9260df7246e5f4d5aa3cb033278b

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
 - 2.0 實驗不同位數的數字 (The digits of input number = 4)
 - 3.0 多組數字共同運算 (Add 3 numbers (each number has 3 digits) together)

## 3. Result
 - The result for Addition, Subtraction, Combine addition and subtraction
 ![](Result.png)
 - The result for multiplication: Validation Accuracy = Testing Accuracy =  
  
## 4. 討論
 **Addition or Subtraction**
 - Addition 和 Subtraction 的架構皆是使用 LSTM 作 encode，再使用 RepeatVector 將 output 重複4次之後輸入第二個 LSTM 作 decode
 - 從結果可以觀察到 Addition 和 Subtraction 不論使用多少 batch size 和 epoch 訓練，測試精準度都非常高，在 1000 筆的測試資料中都可以達到 99% 以上的精準度；而當輸入數值為四位數字或輸入三個三位數字時，測試精準度也大多在接近 99% 的數值。
 
 **Addition and Subtraction Combine**
 - 混合了加法器和減法器的實現 (Combine)，若使用和 Addition 方法相同架構訓練，精準度最高只到 76%
 - 因此，Combine 的架構略為經過修改，經過 LSTM encode 之後，透過 dense 將資料特徵量變成 (4*hidden_layer數)，再 resize 成 (4, hidden_layer)，輸入 decode 的 LSTM 中(詳細架構可以看 Addition_Subtraction_rnn.ipynb)
 - 經過修改之後的架構，在加法減法混合的資料中，Validation 精準度可以大於 97%，Testing 精準度也可以大於 90%
 - 從 Training Epoch 可以觀察到，加減混合的資料集較為複雜，需要訓練較多次模型才會完全收斂，在實驗中訓練了 200 個 Epoch，相較 Addition 或 Subtraction 的 100 個 Epoch 多了一倍
 
 **Multiplication**
 - Batch size = 128, Epoch = 200
 - 同樣的架構應用在乘法器上效果明顯比較不好，可能因為乘法的運算較複雜，LSTM 擬合的結果較不好，Validation精準度只達 78.99%，Testing精準度只達 0.684

## 5. 檔案說明
 - addition_rnn.ipynb : 實現加法器
 - Subtraction_rnn.ipynb : 實現減法器
 - Addition_Subtraction_rnn.ipynb : 加法器混合減法器 (A+B-C or A-B+C)
 - Multiplication_rnn.ipynb : 實現乘法器