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

Part2: 
