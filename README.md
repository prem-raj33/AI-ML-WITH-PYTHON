import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from io import StringIO
data="""index,company,body-style,wheel-base,length,engine-type,num-of-cylinders,horsepower,average-mileage,price
0,alfa-romero,convertible,88.6,168.8,dohc,four,111,21,13495
1,alfa-romero,convertible,88.6,168.8,dohc,four,111,21,16500
2,alfa-romero,hatchback,94.5,171.2,ohcv,six,154,19,16500
3,audi,sedan,99.8,176.6,ohc,four,102,24,13950
4,audi,sedan,99.4,176.6,ohc,five,115,18,17450
5,audi,sedan,99.8,177.3,ohc,five,110,19,15250
6,audi,wagon,105.8,192.7,ohc,five,110,19,18920
9,bmw,sedan,101.2,176.8,ohc,four,101,23,16430
10,bmw,sedan,101.2,176.8,ohc,four,101,23,16925
11,bmw,sedan,101.2,176.8,ohc,six,121,21,20970
13,bmw,sedan,103.5,189,ohc,six,182,16,30760
14,bmw,sedan,103.5,193.8,ohc,six,182,16,41315
15,bmw,sedan,110,197,ohc,six,182,15,36880
16,chevrolet,hatchback,88.4,141.1,l,three,48,47,5151
17,chevrolet,hatchback,94.5,155.9,ohc,four,70,38,6295
18,chevrolet,sedan,94.5,158.8,ohc,four,70,38,6575
19,dodge,hatchback,93.7,157.3,ohc,four,68,31,6377
20,dodge,hatchback,93.7,157.3,ohc,four,68,31,6229
27,honda,wagon,96.5,157.1,ohc,four,76,30,7295
28,honda,sedan,96.5,175.4,ohc,four,101,24,12945
29,honda,sedan,96.5,169.1,ohc,four,100,25,10345
30,isuzu,sedan,94.3,170.7,ohc,four,78,24,6785
31,isuzu,sedan,94.5,155.9,ohc,four,70,38,
32,isuzu,sedan,94.5,155.9,ohc,four,70,38,
33,jaguar,sedan,113,199.6,dohc,six,176,15,32250
34,jaguar,sedan,113,199.6,dohc,six,176,15,35550
35,jaguar,sedan,102,191.7,ohcv,twelve,262,13,36000
36,mazda,hatchback,93.1,159.1,ohc,four,68,30,5195
37,mazda,hatchback,93.1,159.1,ohc,four,68,31,6095
38,mazda,hatchback,93.1,159.1,ohc,four,68,31,6795
39,mazda,hatchback,95.3,169,rotor,two,101,17,11845
43,mazda,sedan,104.9,175,ohc,four,72,31,18344
44,mercedes-benz,sedan,110,190.9,ohc,five,123,22,25552
45,mercedes-benz,wagon,110,190.9,ohc,five,123,22,28248
46,mercedes-benz,sedan,120.9,208.1,ohcv,eight,184,14,40960
47,mercedes-benz,hardtop,112,199.2,ohcv,eight,184,14,45400
49,mitsubishi,hatchback,93.7,157.3,ohc,four,68,37,5389
50,mitsubishi,hatchback,93.7,157.3,ohc,four,68,31,6189
51,mitsubishi,sedan,96.3,172.4,ohc,four,88,25,6989
52,mitsubishi,sedan,96.3,172.4,ohc,four,88,25,8189
53,nissan,sedan,94.5,165.3,ohc,four,55,45,7099
54,nissan,sedan,94.5,165.3,ohc,four,69,31,6649
55,nissan,sedan,94.5,165.3,ohc,four,69,31,6849
56,nissan,wagon,94.5,170.2,ohc,four,69,31,7349
57,nissan,sedan,100.4,184.6,ohcv,six,152,19,13499
61,porsche,hardtop,89.5,168.9,ohcf,six,207,17,34028
62,porsche,convertible,89.5,168.9,ohcf,six,207,17,37028
63,porsche,hatchback,98.4,175.7,dohcv,eight,288,17,
66,toyota,hatchback,95.7,158.7,ohc,four,62,35,5348
67,toyota,hatchback,95.7,158.7,ohc,four,62,31,6338
68,toyota,hatchback,95.7,158.7,ohc,four,62,31,6488
69,toyota,wagon,95.7,169.7,ohc,four,62,31,6918
70,toyota,wagon,95.7,169.7,ohc,four,62,27,7898
71,toyota,wagon,95.7,169.7,ohc,four,62,27,8778
79,toyota,wagon,104.5,187.8,dohc,six,156,19,15750
80,volkswagen,sedan,97.3,171.7,ohc,four,52,37,7775
81,volkswagen,sedan,97.3,171.7,ohc,four,85,27,7975
82,volkswagen,sedan,97.3,171.7,ohc,four,52,37,7995
86,volkswagen,sedan,97.3,171.7,ohc,four,100,26,9995
87,volvo,sedan,104.3,188.8,ohc,four,114,23,12940
88,volvo,wagon,104.3,188.8,ohc,four,114,23,13415"""
df = pd.read_csv(StringIO(data))
df.head()
df['price'] = pd.to_numeric(df['price'], errors='coerce')
missing_rows = df.isnull().sum()
print("Missing Values:\n", missing_rows)
df_clean = df.dropna(subset=['price'])  # Only drop if 'price' is missing
df_clean.reset_index(drop=True, inplace=True)
min_price = df_clean['price'].min()
max_price = df_clean['price'].max()
cars_min_price = df_clean[df_clean['price'] == min_price]
cars_max_price = df_clean[df_clean['price'] == max_price]
print("\n1. Cars with Minimum Price:\n", cars_min_price[['company', 'body-style', 'price']])
print("\n1. Cars with Maximum Price:\n", cars_max_price[['company', 'body-style', 'price']])
body_style_count = df_clean['body-style'].value_counts()
print("\n2. Number of cars with different body-styles:\n", body_style_count)
avg_price_body_style = df_clean.groupby('body-style')['price'].mean().sort_values(ascending=False)
print("\n3. Average price of all body types (descending):\n", avg_price_body_style)
ing
avg_price_company = df_clean.groupby('company')['price'].mean().sort_values(ascending=False)
print("\n4. Average price of all companies (descending):\n", avg_price_company)
sns.set(style="whitegrid")
df_clean['body-style'].value_counts().plot.pie(autopct='%1.1f%%', startangle=90, figsize=(6, 6), title='Body-Style Distribution')
plt.ylabel('')
plt.show()
plt.figure(figsize=(8, 5))
sns.barplot(x=avg_price_body_style.index, y=avg_price_body_style.values, palette='viridis')
plt.title('Average Price by Body-Style')
plt.ylabel('Average Price')
plt.xlabel('Body-Style')
plt.xticks(rotation=45)
plt.show()
plt.figure(figsize=(10, 5))
sns.barplot(x=avg_price_company.index, y=avg_price_company.values, palette='mako')
plt.title('Average Price by Company')
plt.ylabel('Average Price')
plt.xlabel('Company')
plt.xticks(rotation=45)
plt.show()
plt.figure(figsize=(7, 5))
sns.scatterplot(data=df_clean, x='horsepower', y='price', hue='body-style', palette='deep')
plt.title('Horsepower vs Price')
plt.show()
corr_columns = ['wheel-base', 'length', 'horsepower', 'average-mileage', 'price']
corr_matrix = df_clean[corr_columns].corr()
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Heatmap')
plt.show()
plt.figure(figsize=(8, 4))
sns.boxplot(data=df_clean, y='price')
plt.title('Boxplot of Car Prices (Outlier Detection)')
plt.show()
plt.figure(figsize=(8, 4))
sns.boxplot(data=df_clean, y='horsepower')
plt.title('Boxplot of Horsepower (Outlier Detection)')
plt.show()
print("\nMissing Values:\n", missing_rows[missing_rows > 0])
print("\nCleaned Data Overview:\n", df_clean.describe())
