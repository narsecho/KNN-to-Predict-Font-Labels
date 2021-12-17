Predict front labels by KNN and parameters refine. 
Data source: https://archive.ics.uci.edu/ml/machine-learning-databases/00417/fonts.zip
Each "case" describes a digitized image of a specific character (letter or digit) typed in specific font
"FONT"; Each image has size 20 x20 =400 pixels; Each one of these 400 pixels has a "gray level" = integer between 0 and 255
Here in the practice:

To use google colab run this code, better to create a same path in your google drive, and upload the data files.

Data Preparation:
1. Select 4 fonts as four classes. "bondoni","eras","gabriola","technic" were selected.
2. Drop 9 columns {fontVariant, m_label, orientation, m_top, m_left, originalH, originalW, h, w};Only use 3 columns {font, strength, italic}
3. only use cases with {strength = 0.4 and italic=0}
3. The rows (cases) will be discarded if missing numerical data.

Part1: EDA
1.1 COpute 4 means of each column within the 4 classes, use Kolmogorov-Smirnov KS-test to quantify if there are significant difference.
1.2 Compute correlation matrix CORR of the 400 orignial features X1, ..., X400. Identify and display the 10 highest correlation values and the pixel positions. 
1.3 Standardize the features matrix DATA by centering/rescaling each feature Xj to create a new feature
Yj= (Xj - mj) /sj;
1.4 Generate the "TrueClass" column vector TRUC of dimension N, such that TRUC(n) is the true class of Case # n

Part2: KNN and find best k
2.1 Randomly select 80% and 20% as training and testing data set within each class, and then regroup training and testing set.
2.2 Apply KNN for automatic classificaiton on the reslcaed data into the 4 classes, for k=5,10,15,20,30,40,50. Plot the curve of accuracy vs k 
2.3 Find the best range a<k<b from 2.2 and infill interpolate k to find the best k, compute 90% confidence interval for accuracy of test for best k.
2.4 generate confusion matrix and compare the performances among the 4 classes.
2.5 Generate error list ERR21, Err23 and ERR24, and use 3 casees to explain why they were misclassified by computing the closest neighbours. 

Part3: PCA and KNN
3.1 Compute 400 eigenvalues Lm and 400 eigenvectors Wm; display the graph of Lm vs m
3.2 Compute the PEV(m) by the formula PEV(m) = (L1+L2+...+Lm)/400; display graph PEV(m) Vs m; Compute the smallest integr "r" of PEV(r) >= 90%
3.3 Each case #n will be represented by its first r principal components [ PC1(n) , ..., PCr(n)] These numbers are given by matrix products of the form [line vector]* [column vector] PC1(n) = Sn W1, PC2(n) = SnW2 , ... , PCr(n) = SnWr Case #n will now be described by the row vector Zn = [PC1(n) ....PCr(n)] of its first "r" principal components the row vector Zn has dimension "r" and is given by Zn = Sn * W Denote ZDATA the Nx400 matrix stacking up the N row vectors Z1; Z2; ... ZN Compute the matrix ZDATA by the matrix product ZDATA = SDATAW
3.4 Apply kNN classification with the same k=k* as in 2.4, and with the same TRAIN and TEST sets, but with each case #n described by the "r" new features Zn = [PC1(n) ....PCr(n)]
3.5 Pick color1 color2 color3 color4, one color per class CL1 CL2 CL3 CL4; Represent each Case #n by its first 2 principal components [Z1(n),Z2(n)]
Case #n can be (very approximately) represented by the planar point Vn = [Z1(n), Z2(n)]; Display on the same planar graph the scatter plot of CL2 cases (in color2) and CL4 cases in color4 evaluate visually if these planar projections of CL2 and CL4 look easily separable or not Implement similar displays for CL2, CL3 and CL2,CL1.
3.6 On a new graph display as above the planar projection of CL2 in color2 add the display in color1 of all the misclassifed points listed in the list ERR21; On the same figure add similar displays for the lists ERR23 and ERR24 in color3 and color 4 Interpret visually.
