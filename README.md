# Employee Attrition
این پروژه برای تحلیل ریزش کارکنان طراحی شده و از الگوریتم های یادگیری ماشین استفاده می کند
-اول از همه دیتاست رو از کگل دانلود کردم و بعد خودم اطلاعات نامربوط رو خیلی لازم نمیشود رو حذف کردم 
و زمانی که دیتاست رو خوندم متوجه شدم یه سری از دریف ها NaN هست.با این دستور کد اون بخش ها رو حذف کردم

# خوندن فایل
df = pd.read_csv("Employee-Attrition.csv")  د

#  حذف ستون‌هایی که کامل خالی هستن
df = df.dropna(axis=1, how='all')
# حذف ردیف‌هایی که حداقل یک مقدار خالی دارن
df_cleaned = df.dropna()

#  ذخیره فایل تمیزشده
df_cleaned.to_csv("cleaned_file.csv", index=False)

print("✅ فایل تمیزسازی شد و ذخیره شد.")



-و بعد دوبار دیتا چک کردم و حروف ها رو تبدیل به عدد کردم .


#تبدیل حروف به عدد
le=LabelEncoder()

for col in df:
    if df [col].dtype=='object':
        if len (df[col].unique()) <=9:
            print(col)
            le.fit(df[col])
            df[col]=le.transform(df[col])



-حالت های مختلف رو چک کردم و اونای که تعداد زیادی داشتن و کاربردی نداشتن رو حذف کردم
#حذف دیتا اضافی
df.drop(['TotalWorkingYears','YearsAtCompany','YearsSinceLastPromotion'],axis=1,inplace=True)


-رابطه ترک شغل و با کار زیاد رو چک کردم 
            f,ax = plt.subplots(figsize=(5,5))
sns.countplot(x="OverTime",hue="Attrition",data=df)


-ترک شغل رو از ستون ها خارج کردم که خروجی من به حساب بیاد
#جدا کردن x,y
x=df.drop('Attrition',axis=1)
y=df['Attrition']

-خروجی و ورودی تست و تمرین رو جدا کردم
#جدا کردن test,train
x_train, x_tast, y_train, y_test =train_test_split(x,y, test_size=0.2)

-با الگوریتم random forst چک کردم درصد قابل قبولی نداد
model_rf = RandomForestClassifier(n_estimators=100,random_state=42)
model_rf.fit(x_train,y_train)

-با الگوریتم logistic regression چک کردم درصد قابل قبولی نداد
model_lr = LogisticRegression(random_state=42 ,max_iter=100 )
model_lr.fit(x_train,y_train)

-با الگوریتم light gbm چک کردم درصد قابل قبولی داد

-و حالا با دیپ لرنینگ چک کردم
