# E_commerce_data_analysis-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/96db8743-2739-4ddd-a080-19c5c979fd2d/1cc26a5d5ee1ec047f0b?experience=power-bi

## Problem Statement

This dashboard helps to analyze key business metrics of E_commerce_data including shipping efficiency, product-level performance, sales by region
and customer behavior to support better business decisions across logistics, marketing, and sales strategy.

## KPIs & Visuals
- Total Sales,Total Profit,Avg Order Value,Avg Shipping Cost,Profit %,Avg Delivery days
- Monthly Sales and Profit Trends
- Top 10 products by sales
- % composition of Total Profit by Categories and Total sales by order priority
- Total sales by region

## 📌 Tools Used
- Python for data Cleaning
- mySQL for data storage
- Power BI for reports

### Steps Followed
- Step 1 : Open Jupytor Notebook Read the CSV data file and then removing null values
- Step 2 : Changed the object data types into Int,Float data types based on our requirements
  
        e_df['Sales'] = pd.to_numeric(e_df['Sales'],errors = "coerce").astype("Int32")
        e_df['Aging'] = pd.to_numeric(e_df['Aging'],errors = "coerce").astype("Float32").astype("Int32")
        e_df['Quantity'] = pd.to_numeric(e_df['Quantity'],errors = "coerce").astype("Int32")
        e_df['Profit'] = pd.to_numeric(e_df['Profit'],errors = "coerce").astype("Float32").astype("Int32")
        e_df['Discount'] = pd.to_numeric(e_df['Discount'],errors = "coerce").astype("Float32")
        e_df['Shipping Cost'] = pd.to_numeric(e_df['Shipping Cost'],errors = "coerce").astype("Float32")

        e_df.dtypes
- Step 3 : corrected the wrong region values like 'So3th', '4orth' to 'South', 'North'

        #here i renamed 'So3th', '4orth' to 'South', 'North'
        #e_df.Region.unique()
        e_df['Region'].replace({
           'So3th':'South', 
            '4orth':'North' 
        },inplace=True)
  

- Step 4 : Removed the $ symbol "Sales","Profit","Shipping Cost" these columns for performing the calculations

        e_cols = ["Sales","Profit","Shipping Cost"]
        for col in e_cols:
            e_df[col] = e_df[col].str.replace('$','')
            
- Step 5 : After added the data into the mySQL workbench and then opened powerbi connected to the sql from powerbi
- Step 6 : Created Some measures and added to the dashboard with card visual

           Total Sales = SUM('e_commerce_data e_com_data'[Sales])
           Total Profit = sum('e_commerce_data e_com_data'[Profit])
           Avg Order Value = DIVIDE([Total Sales],DISTINCTCOUNT('e_commerce_data e_com_data'[Order ID]))
           Avg Shipping Cost = AVERAGE('e_commerce_data e_com_data'[Shipping Cost])
           Profit % = DIVIDE([Total Profit],[Total Sales])
           Avg Delivery Days = AVERAGE('e_commerce_data e_com_data'[Aging])

- Step 7 : Added a Gauge visual to the dashboard and set target value as 0.45 (45%)
- Step 8 : Added a Line chart to visualise the monthly Total sales and Total profit
- Step 9 : Created a Bar chart with Top 10 Products by Sales and then added another Bar chart with Total Sales By Region
- Step 10 : Added a Donut chart that shows Total Profit % by Product category
- Step 11 : Added a Pie-chart that shows Total Sales % by Order Priority
- Step 12 : Added a New Slicer with Segment,by this we can filter by Consumer,Corporate & Homeoffice
- Step 13 : Added a Another New Slicer with Ship mode ,we can filter out by ship mode 
  
## Business Insights

### Top 10 Customer Names by sales

      c_names = df.groupby("Customer Name")[['Sales']].sum().sort_values(by="Sales",ascending=False).head(10)
      sns.barplot(y="Customer Name",x="Sales",data=c_names)
      plt.title("Top 10 Customer Names Vs Sales")
      plt.show()

<img width="2021" height="1357" alt="Image" src="https://github.com/user-attachments/assets/0838007d-336d-4e9c-bd2e-bb60aa770567" />


### Region wise Profit by Customer Segment

      df.pivot_table(
          index = "Segment",
          columns = "Region",
          values = "Profit",
          aggfunc = 'sum'
      ).style.background_gradient(cmap="RdYlGn",axis=None)

- The below heatmap shows Region wise customer Profit segment ,so most profitable customers are in the Consumer segment from Central region

<img width="1236" height="210" alt="Image" src="https://github.com/user-attachments/assets/e53360b7-6051-4d0c-80d1-be9ff5785b5b" />  

---

- In power bi Dashboard We can see Top 10 products by Sales and Total sales by region
- All KPI's, Sales and Profit by monthly Trends
- Total Profit By product category and Total sales by Order Priority
- Two slicers by Segment and Shipmode




<img width="1314" height="730" alt="Image" src="https://github.com/user-attachments/assets/36f4a8de-beb5-4ffe-b0e0-317114a4fa41" />


 
