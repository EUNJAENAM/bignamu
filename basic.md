### PRINT/리스트 더하기/
```python
print("a={}, b={}".format(a,b))
# 리스트와 리스트 더하기
myList1 = [1,2,3]
myList2 = [4,5,6]
myList1.extend(myList2)
```

### loc/iloc
```python
#DataFrame에서 부분정보 가져올때는 [열][행]
df["2014년"][2:5]     #2014년 컬럼중 2행~5행까지 정보
#loc / iloc 는 [행,열] 인데 iloc는 숫자로만

df.loc[2:7,['2012년','2014년']]        #부분 불러오기
df.iloc[2:7,3:5]                      #iloc 는 숫자로만

df_any = df1.loc[2035,['행정구역','2019년_총인구수','2020년_총인구수','2021년_총인구수']]
```

### SPLIT/REPLACE/SORT_VALUE
```python
a = 'This is a pen’
temp = a.split(' ')

a = '01-sample.png’
a.replace(‘.png’,‘.jpg’)

df['총계'] = df['총계'].str.replace(',','').astype(int)      #콤마 들어간 숫자 변환
df.sort_values(by='소계', ascending=True, inplace=True)        #소계별로 정렬
a.strip()     #공백제거
```
### 조건값으로 DROP 하기
```python
jogun = df_total[df_total['PerHour'] > 130].index
df_total.drop(jogun, inplace=True)
df_total

a = df[df['구별']=='용산구'].index
df.drop(a, axis='index')

df.drop(index=0)   # 0번 인덱스 삭제
df.drop(index=0, columns='2016년', axis=1)    #0번 인덱스 2016년 컬럼삭제

df.drop(labels=['2012년 이전','2014년','2015년','2016년'], axis=1)
df.drop(labels=[1,2,3], axis=0)
#NaN 제거
df.dropna(subset = [‘열이름’])
#모든 값이 전부 NaN 인 행만 제거
df.dropna(how=’all’)
```
### 조건값으로 정보찾기
```python
df[df['상태'] != '사업개시']    #사업개시란 발전소가 가동중이라는 의미
df[(df['상태'] == '공사진행') & (df['사업개시일'] != 'NaN')]  

df['상호'] =='태양' and df['상호'] =='솔라' and  df['상호'] =='햇빛'
df = df[df['상호'].str.contains('풍력')]
df = df[(df['상호'].str.contains('태양')) | (df['상호'].str.contains('솔라'))].index
```

### COLUMNS NAME
```python
df.columns                               #컬럼명 확인
df.columns = ['구별', '총계']             #컬럼명 새로 지정(변경)
df.rename(columns = {'총계':'소계'},inplace=True)     #rename 사용시
df.drop([0,1], inplace=True)         #불필요 column 삭제 index번호임 (0부터 시작)
```

### 결측치
```python
df.isnull().sum()    #결측치 개수 확인
df.fillna(0,inplace=True)     #결측치 값 특정값으로 채우기
df.fillna(method=’ffill’)      #‘backfill’, ‘bfill’, ‘pad’, ‘ffill’, None
```

### RESET INDEX
```python
df.reset_index(drop=True, inplace=True)       #index reset
CCTV_Seoul.set_index('구별', inplace=True)    #인덱시 변경
```
### 형변환
```python
df.reset_index(drop=True, inplace=True)     #index reset
```
### CONCAT/MERGE
```python
result = pd.concat([df1, df2, df3])     #데이터 연결 (레코드수 증가)
result = pd.concat([df1, df2, df3], keys=['x', 'y', 'z'])   #index 추가
result = pd.concat([df1, df4], axis=1)     #join=outter (기본값), 합집합
result = pd.concat([df1, df4], axis=1, join='inner')    #join=inner, 데이터가 모두 있는 경우

data_result = pd.merge(CCTV_Seoul, pop_Seoul, on='구별')      # 데이터 합치기(Merge)
```

### 상관관계
```python
np.corrcoef(data_result['고령자비율'],data_result['총계'])     #상관관계 분석
```

### 더미변수
```python
col_cols = df.select_dtypes('object').columns.values
df1 = pd.get_dummies(data=df, columns=col_cols)
```

### groupby/sort
```python
train_data[['Destination', 'Transported']].groupby(['Destination'], as_index=False).mean().sort_values(by='Transported')

arrived = train_data[train_data['Transported'] == 1]['Destination']. value_counts()
not_arrived = train_data[train_data['Transported'] == 0]['Destination']. value_counts()
df = pd. DataFrame([arrived, not_arrived])
df. index = ['arrived','not_arrived']
df. plot(kind= 'bar',stacked= False , figsize= (8,4))
plt.title('Destination')
plt. show()
```

### 범주화/시각화
```python
train_data.loc[(train_data['Age'] >= 0) & (train_data['Age'] < 10), 'Age'] = 0
train_data.loc[(train_data['Age'] >= 10) & (train_data['Age'] < 20), 'Age'] = 10
train_data.loc[(train_data['Age'] >= 20) & (train_data['Age'] < 30), 'Age'] = 20
train_data.loc[(train_data['Age'] >= 30) & (train_data['Age'] < 40), 'Age'] = 30
train_data.loc[(train_data['Age'] >= 40) & (train_data['Age'] < 50), 'Age'] = 40
train_data.loc[(train_data['Age'] >= 50) & (train_data['Age'] < 60), 'Age'] = 50
train_data.loc[(train_data['Age'] >= 60) & (train_data['Age'] < 70), 'Age'] = 60
train_data.loc[(train_data['Age'] >= 70) & (train_data['Age'] < 80), 'Age'] = 70

Arrived = train_data[train_data['Transported'] == 1]['Age']. value_counts()
Not_Arrived = train_data[train_data['Transported'] == 0]['Age']. value_counts()
df = pd. DataFrame([Arrived, Not_Arrived])
df. index = ['Arrived','Not_Arrived']
df. plot(kind= 'bar',stacked= False , figsize= (6,4)). legend(loc = 'lower center')
plt.title('Age')
plt. show()
```
