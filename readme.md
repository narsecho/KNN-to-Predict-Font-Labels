Predict front labels by KNN and parameters refine. 
Data source: https://archive.ics.uci.edu/ml/machine-learning-databases/00417/fonts.zip
Each "case" describes a digitized image of a specific character (letter or digit) typed in specific font
"FONT"; Each image has size 20 x20 =400 pixels; Each one of these 400 pixels has a "gray level" = integer between 0 and 255
Here in the practice:

Data Preparation:
1. Select 4 fonts as four classes. "bondoni","eras","gabriola","technic" were selected.
2. Drop 9 columns {fontVariant, m_label, orientation, m_top, m_left, originalH, originalW, h, w};Only use 3 columns {font, strength, italic}
3. only use cases with {strength = 0.4 and italic=0}
3. The rows (cases) will be discarded if missing numerical data.


