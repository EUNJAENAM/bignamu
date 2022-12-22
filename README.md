### PLOT
```python
import matplotlib.pyplot as plt
plt.rc('font',family='NanumBarunGothic')    #한글폰트 설정
plt.figure()
data_result['총계'].sort_values().plot(kind='barh', grid=True, figsize=(8,8))
plt.show()

df[‘aa’].value_counts().plot(kind=“bar”)
```

### SCATTER
```python
import matplotlib.pyplot as plt

plt.scatter(data_result['인구수'], data_result['총계'], s=50)
plt.xlabel('인구수')
plt.ylabel('CCTV')
plt.grid()
plt.show()

df_total.plot.scatter(x='A_DISTANCE', y='ET', c='DarkBlue')

```

### 선형회귀 SCATTER Chart
```python
# numpy에서 선형회귀를 구할수 있는 함수, 기울기와 절편 y=wx+b
fp1 = np.polyfit(data_result['인구수'], data_result['소계'], 1)

f1 = np.poly1d(fp1)
fx = np.linspace(100000, 700000, 100)
plt.figure(figsize=(10,10))
plt.scatter(data_result['인구수'], data_result['소계'], s=50)
plt.plot(fx, f1(fx), ls='dashed', lw=3, color='g')
plt.xlabel('인구수')
plt.ylabel('CCTV')
plt.grid()
plt.show()

```

## SEABORN
### Countplot
```python
import seaborn as sns
sns.countplot(data=df_total, x=’aaa’)

![image](https://user-images.githubusercontent.com/91514129/209146251-139ce0d2-d8c9-49e8-aaa1-ea081cbe363c.png)

```

### distplot
```python
sns.distplot(df_total['ET'])
![image](https://user-images.githubusercontent.com/91514129/209146416-d9aad2c4-d4a9-4aea-83db-44a21accd41d.png)

```

### boxplot
```python
sns.boxplot(x=df_total['level1_pnu'], y=df_total['ET'])
![image](https://user-images.githubusercontent.com/91514129/209146440-697a4812-f358-4d48-9c08-6c5c3a871259.png)

```

### pairplot
```python
sns.pairplot(df_total)
![image](https://user-images.githubusercontent.com/91514129/209146458-51c7bf14-b2d8-40d6-b7da-ec872d8a8d42.png)

```

### heatmap
```python
import matplotlib.pyplot as plt
sns.heatmap(df_total.corr(), annot = True)
plt.show()

![image](https://user-images.githubusercontent.com/91514129/209146479-c6c2208d-e528-4b90-836b-5b8cf96e27fc.png)

```
