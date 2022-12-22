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

```

### distplot
```python
sns.distplot(df_total['ET'])

```

### boxplot
```python
sns.boxplot(x=df_total['level1_pnu'], y=df_total['ET'])

```

### pairplot
```python
sns.pairplot(df_total)

```

### heatmap
```python
import matplotlib.pyplot as plt
sns.heatmap(df_total.corr(), annot = True)
plt.show()

```
