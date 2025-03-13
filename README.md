#Hotel Booking Data Analysis
# 📊 Hotel Booking Data Analysis

## 🏨 Overview
This project analyzes hotel booking data to uncover trends in **cancellations, pricing (ADR), and customer behavior**.  
We compare **City Hotels vs. Resort Hotels** and investigate factors affecting cancellations and revenue.

## 📂 Dataset
- The dataset contains information on hotel reservations, customer details, booking status, and revenue.
- **Key columns:** `hotel`, `is_canceled`, `reservation_status_date`, `adr`, `arrival_date_month`, etc.

## 🔍 Key Insights
✔ **Resort Hotels** have higher prices but lower cancellation rates.  
✔ **Peak months** (July-August) see increased ADR (Average Daily Rate).  
✔ **Cancellations are higher in City Hotels** due to flexible policies.  
✔ Price variations between hotels can impact revenue strategies.  

## This is my python Project code
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')
df=pd.read_csv("C:\\Users\\Aravind kumar\\Downloads\\hotel_booking.csv\\hotel_booking.csv")


```
#1
```python
cancelled_perc=df['is_canceled'].value_counts(normalize=True)
cancelled_perc
plt.figure(figsize=(5,4))
plt.title("Reservation status count")
plt.bar(["Not cancled","Canceled"],df['is_canceled'].value_counts(),edgecolor='k',width=0.7)
plt.show()
plt.savefig("Reservation status count.png", dpi=300, bbox_inches='tight')
```
#2
```python
plt.figure(figsize=(8,4))
ax1=sns.countplot(x='hotel',hue='is_canceled',data=df,palette='Blues')
legend_labels,_=ax1.get_legend_handles_labels()
ax1.legend(bbox_to_anchor=(1,1))
plt.title("Reservation status in different hotels",size=20)
plt.xlabel('hotel')
plt.ylabel('number of reservations')
plt.legend(['not canceled','canceled'])
plt.savefig("reservation2.jpg", dpi=300, bbox_inches='tight')
plt.show()

```
#3
```python
resort_hotel=df[df['hotel']=='Resort Hotel']
resort_hotel['is_canceled'].value_counts(normalize=True)
city_hotel=df[df['hotel']=='City Hotel']
city_hotel['is_canceled'].value_counts(normalize=True)
resort_hotel=resort_hotel.groupby('reservation_status_date')[['adr']].mean()
city_hotel=city_hotel.groupby('reservation_status_date')[['adr']].mean()
plt.figure(figsize=(20,8))
plt.title("Average Daily Rate in City and Resort Hotel",fontsize=30)
plt.plot(resort_hotel.index,resort_hotel['adr'],label='Resort Hotel')
plt.plot(city_hotel.index,city_hotel['adr'],label='City Hotel')
plt.legend(fontsize=20)
plt.savefig("daily.png", dpi=300, bbox_inches='tight')
plt.show()
```
#4
```python
df['month']=df['reservation_status_date'].dt.month
plt.figure(figsize=(16,8))
ax1=sns.countplot(x='month',hue='is_canceled',data=df,palette='bright')
legend_labels,_=ax1.get_legend_handles_labels()
ax1.legend(bbox_to_anchor=(1,1))
plt.title("Reservation status per month",size=20)
plt.xlabel('month')
plt.ylabel('number of reservations')
plt.legend(['not canceled','canceled'])
plt.savefig("month.jpg", dpi=300, bbox_inches='tight')
plt.show()
```
#5
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(12, 6))  # Adjust width and height
sns.barplot(x='month', y='adr', data=df[df['is_canceled'] == 1].groupby('month', as_index=False)['adr'].sum())

plt.title("ADR per Month", fontsize=20)
plt.show()

```
#6
```python
cancelled_data=df[df['is_canceled']==1]
top_10_country=cancelled_data['country'].value_counts()[:10]
plt.figure(figsize=(8,8))
plt.title('Top 10 countries with reservation canceled')
plt.pie(top_10_country,autopct='%.2f',labels=top_10_country.index)
plt.savefig("pie.jpg", dpi=300, bbox_inches='tight')
plt.show()
![image](https://github.com/user-attachments/assets/cb399702-75c7-4c9e-a249-61e6414f6545)


```
#7
```python
cancelled_df_adr=cancelled_data.groupby('reservation_status_date')[['adr']].mean()
cancelled_df_adr.reset_index(inplace=True)
cancelled_df_adr.sort_values('reservation_status_date',inplace=True)
not_cancelled_data=df[df['is_canceled']==0]
not_cancelled_df_adr=not_cancelled_data.groupby('reservation_status_date')[['adr']].mean()
not_cancelled_df_adr.reset_index(inplace=True)
not_cancelled_df_adr.sort_values('reservation_status_date',inplace=True)
plt.figure(figsize=(20,6))
plt.title('Average Daily Rate')
plt.plot(not_cancelled_df_adr['reservation_status_date'],not_cancelled_df_adr['adr'],label='not cancelled')
plt.plot(cancelled_df_adr['reservation_status_date'],cancelled_df_adr['adr'],label='cancelled')
plt.legend()
plt.savefig("average2.jpg", dpi=300, bbox_inches='tight')
plt.show()http://localhost:8888/files/Untitled12.ipynb?_xsrf=2%7Ce2e9a376%7Ca6fd622573c85a9d93361cc35b7f6412%7C1739705102
df=pd.read_csv("C:\\Users\\Aravind kumar\\Downloads\\hotel_booking.csv\\hotel_booking.csv")

```
