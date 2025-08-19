# EDA

### DataFrame

파일을 DataFrame으로 불러오기

```python
df = pd.read_csv('data.csv')
```

```python
df = pd.read_excel('data.xlsx')
```

컬럼 확인

```python
pd.set_option("display.max_rows", None) # 모든 행 출력
pd.set_option("display.max_columns", None) # 모든 열 출력
  
dtype_df = pd.DataFrame({
	"dtype": df.dtypes,
	"non_null_count": df.notnull().sum(),
	"null_count": df.isnull().sum()
})

dtype_df
```
