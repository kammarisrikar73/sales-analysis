# sales-analysis
creating the first ever to check how can i move forward in this journey
!pip install streamlit
import streamlit as st
import numpy as np
import pandas as pd
st.title("sales analysis")
num=st.number_input("enter the number of transactions",min_value=1)
if st.button("Generate data"):
  product = ["mobile","laptop","earphones","ipad","chargers"] 
  product_column = np.random.choice(product,num) 
  date = pd.date_range(start="2024-01-01",end="2024-01-31") 
  date = np.random.choice(pd.to_datetime(date),num) 
  price_dict = {"mobile":15000, "laptop":40000, "earphones":1000, "ipad":2000, "chargers":500} 
  price = np.array([price_dict[item]for item in product_column]) 
  quantity = np.random.randint(1,10,num) 
  customer_id = np.random.randint(10000,99999,num) 
  df = pd.DataFrame({"Product":product_column, "Date":date, "Price":price, "Quantity":quantity, "Customer_ID":customer_id}) 
  df["Total_purchase"] = df["Price"]*df["Quantity"] 
  print("Total items sale:\n",df["Quantity"].sum()) 
  print("first month income:\n",df["Total_purchase"].sum()) 
  monthly_sales = df.groupby("Date")["Total_purchase"].sum() 
  print(monthly_sales) 
  df.to_csv("sales_analysis",index=False)
