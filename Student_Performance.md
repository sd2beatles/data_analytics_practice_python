
Data Analysis  of Parental Qualification On 
                        The Performance of Thier Children
=================================================================================

### 1)Introdcution 

[ENG]The data-set,"Student's Performance in Exams' has arisen my question on whether the level of parental's educational 
background should give an impact on their children's achievements in subjects. To answer the question, we will go through 
a series of steps including data manipulation, graphical representation, conclusions based on the results. 

[KOR] "학생의 수학능력 수행"의 데이타 셋은 과연 부모의 학력이 자식들의 학업능력에 어떠한 영향을 미치는 지에 궁금중을 유발시켰습니다. 
      이러한 호기심을 충족시키려, 데이터 조작, 그래프, 결과에 대한 결론을 포함한 일련의 과정들을 수행해 볼 예정입니다. 

[ENG]Visit the website given below to find raw data and full information about it.

[KOR]데이터 소스는 아래의 웹사이트를 방문하시고, 더 많은 정보를 얻도록 하세요. 

Source: [https://www.kaggle.com/spscientist/students-performance-in-exams]


### 2) Data Manipulation 

1. Data Preapreation 

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
plt.style.use('dark_background')
sns.set(style='darkgrid',palette='bright',font_scale=1.5)
df=pd.read_csv("\StudentsPerformance.csv")
df.head()
```
[ENG] The data is stored in the format of pandas for the convenience of data handling. With the use of  DataFrame/Series.head() method, 
      we can get a glimpse of the whole data: showing the first five entries of a input data.

[KOR] 데이터는 데이터 핸들링의 편의성을 의하여 pandas 형식으로 저장을 했습니다. head() 메소드를 통하여 우리는 데이터의 전체적인 측면을 
      볼 수가 있습니다. 이 메소드는 첫 5 개의 행을 반환합니다. 
      
 data1 사진 넣기 
 
 
 2. Checking The Missing Entries
 
 [ENG] To check if there are missing entries emobided in the data-set,  isnull().any() method is employed to detect them. 
       However,  the results return all False and we do not take extra measures to deal with them. 
       
 [KOR] 데이터의 내재된 결측값을 확인하기 위해서, 우리는 isnull().any() 메소드를 이용하여 찾아보았습니다. 이에 대한 결과로 
       모든 필드(field)에서 False값을 반환했기 때문에, 추가저인 조취는 필요해 보이지 않습니다. 
      
      
 3. Filtering Out Irrevalent Information 
 [ENG]What we are interested in is, regardless of ethnicity or race, the influence of parent's education level on that of children. 
      Therefore we should take away the columns named "race/ethnicity". 
 
  
