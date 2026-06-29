# Boat Sales Data Exploratory Data Analysis (EDA)

This project provides a comprehensive Exploratory Data Analysis (EDA) of sales transactions, products, customer segments, delivery partners, and channel performance for **boAt**, a leading consumer electronics brand specializing in audio products and accessories.

The goal of this analysis is to identify key drivers of revenue, assess profitability, evaluate delivery performance, analyze returns, and uncover customer purchasing behavior to support data-driven decision-making.

---

## 📁 Project Structure

The project directory consists of the following key files:
- **`EDASales.ipynb`**: The main Jupyter Notebook containing the end-to-end data cleaning, merging, visualization, and EDA.
- **`Sales_Data.csv`** (195 MB): The primary transactional dataset containing details of individual sales orders.
- **`Customer_Details.csv`** (14.3 MB): Profiling data for customers, including demographics and geographic segments.
- **`Product_Details.csv`** (11.4 KB): Information about products, including categories, brand, pricing, and launch metadata.
- **`Delivery_Partner_Data.csv`** (7.5 KB): Data on delivery riders, ratings, vehicles, and experience.
- **`Sales_Channel.csv`** (446 B): Details of online marketplaces, D2C website, and offline retail chains.

---

## 📊 Dataset Schema & Data Dictionary

### 1. `Sales_Data.csv`
Contains the core transaction-level records:
* **`SalesID`**: Unique identifier for each sales record.
* **`OrderDate`**: Date the order was placed.
* **`OrderHour`**: Hour of the day when the order was placed.
* **`CustomerID`**: Reference to the customer details.
* **`ProductID`**: Reference to the product details.
* **`ChannelID`**: Reference to the sales channel.
* **`DeliveryPartnerID`**: Reference to the delivery rider.
* **`Quantity`**: Number of items ordered in the transaction.
* **`GrossMRPValue`**: Total Maximum Retail Price (MRP) value of the transaction.
* **`DiscountPct`**: Applied discount percentage (decimal).
* **`DiscountAmount`**: Value of the discount applied.
* **`SellingPrice`**: Selling price before tax and delivery.
* **`NetSales`**: Final net revenue generated from the sale.
* **`GSTRate` / `GSTAmount`**: GST percentage and the tax value.
* **`COGS`**: Cost of Goods Sold.
* **`ShippingCost`**: Cost to ship the order.
* **`Profit`**: Net profit generated (`NetSales - COGS - ShippingCost`).
* **`PaymentMethod`**: Method used (e.g., COD, UPI, Credit/Debit Card, Wallet).
* **`OrderStatus`**: Current status of order (e.g., Delivered, Cancelled, Returned).
* **`CancellationReason` / `ReturnReason`**: Categorical reasons for cancellations/returns.
* **`DeliveryDays`**: Actual delivery duration in days.
* **`CustomerTier` / `CustomerSegment`**: Extracted details of customer profiling.
* **`CityTier` / `ChannelType`**: Classification of cities and sales channels.
* **`IsFestivalPeriod` / `FestivalName`**: Identifiers for sales occurring during major promotional holidays.
* **`IsWeekend`**: Binary flag indicating if order was placed on Saturday or Sunday.
* **`ProductCategory` / `HeroFlag`**: Secondary product identifiers.

### 2. `Customer_Details.csv`
Contains user-profile details:
* **`CustomerID`**: Unique customer key.
* **`SignupDate`**: Date the customer signed up.
* **`Gender`**: Gender of the customer.
* **`AgeBand`**: Categorical age groups (e.g., `18-24`, `25-34`, `35-44`, `45+`).
* **`Segment`**: Profile classification (e.g., `Young Professional`, `Student`, `Family Buyer`, `Gamer`).
* **`Tier`**: Loyalty ranking (`Tier-1`, `Tier-2`, `Tier-3`).
* **`City` / `State` / `Region`**: Geographic location attributes.
* **`PreferredChannel`**: Customer's most-frequented buying channel.
* **`ActivityWeight`**: Value representing engagement intensity.

### 3. `Product_Details.csv`
Contains catalog specifications:
* **`ProductID`**: Unique product key.
* **`Brand`**: Product brand (predominantly `boAt`).
* **`Category`**: Main product category (e.g., `True Wireless Earbuds`, `Smart Watches`, `Neckbands`).
* **`SubCategory`**: Internal sub-segment (e.g., `Airdopes`).
* **`ProductName`**: User-friendly product name.
* **`HeroFlag`**: Boolean (`1` or `0`) indicating high-profile flagships.
* **`LaunchYear`**: Year the product was introduced.
* **`MRP`**: Maximum Retail Price.
* **`CostPrice`**: Cost to manufacture/procure the item.
* **`PopularityWeight`**: Relative score representing consumer interest.
* **`DemandCluster`**: Operational cluster based on historical demand (`Hero`, `Core`).

### 4. `Delivery_Partner_Data.csv`
Contains logistics/rider metrics:
* **`DeliveryPartnerID`**: Unique driver reference.
* **`PartnerName`**: Rider name/identifier.
* **`HomeCity` / `Region`**: Operational area details.
* **`VehicleType`**: Delivery vehicle type (e.g., `Bike`, `Electric Bike`, `Scooter`, `Van`).
* **`Rating`**: Average customer rating of the rider.
* **`ExperienceYears`**: Number of years active.

### 5. `Sales_Channel.csv`
Contains distributions channel details:
* **`ChannelID`**: Unique sales channel identifier.
* **`ChannelName`**: Channel brand (e.g., `Amazon India`, `Flipkart`, `boAt Official Website`, `Croma`, `Reliance Digital`).
* **`ChannelType`**: Method description (e.g., `Online Marketplace`, `D2C`, `Offline Retail`).
* **`ChannelScope`**: `Online` vs `Offline`.
* **`RegionScope`**: Scope of service (`National` vs `Multi-city`).
* **`BaseShare`**: Expected baseline revenue split share.

---

## 📈 Analysis Pipeline in `EDASales.ipynb`

The exploratory data analysis follows this systematic workflow:

1. **Import Libraries**: Load core analytics tools (`pandas`, `numpy`, `seaborn`, `matplotlib`).
2. **Data Loading**: Load all five CSV files and check dimensions (`shape`).
3. **Data Integration**: Perform multi-table outer merges mapping transactions back to details on customers, products, channels, and delivery riders.
4. **Data Cleaning & Type Casting**: Convert dates, resolve timezone offsets, clean strings, and check overall data types.
5. **Key Business Metrics Calculation**: Establish baseline benchmarks:
   * Total Revenue
   * Total Profit
   * Total Orders
   * Unique Customers
   * Average Order Value (AOV)
6. **Feature Engineering**: Extract fields such as Year, Month, Month Name, Quarter, and Day Name to support temporal analysis.
7. **Exploratory Visualizations**:
   * **Product Performance**: Top-selling products and category-specific revenue distribution.
   * **Customer Profiling**: Contribution of customer segments and top revenue-generating cities.
   * **Channel Effectiveness**: Bar plots examining Online vs. Offline revenue streams.
   * **Seasonal & Promotional Impacts**: Sales variations during festival versus non-festival periods.
   * **Operational & Logistics Analysis**: Delivery speeds across different vehicle classes and payment methods.
   * **Profitability Dynamics**: Distribution of profit margins across categories and relationship between discount percentages and volumes sold.
   * **Customer Lifetime Value (CLV)**: Segmenting top customers based on cumulative historical spending.

---

## 💡 Key Business Insights

Based on the EDA, several core operational insights were discovered:
1. **Online Dominance**: Online marketplaces (such as Amazon and Flipkart) and the official boAt D2C store generate the vast majority of the company's revenue compared to brick-and-mortar retail stores.
2. **Hero Products Influence**: High-demand/flagship "Hero" products represent a disproportionately high share of overall sales volumes.
3. **Festive Boost**: Promotional periods (such as Diwali, Independence Day, and New Year Sales) generate a major revenue lift compared to standard periods.
4. **Segment Profitability**: Customer tiers and segments show distinct spending behaviors; working professionals and young adults represent the highest Average Order Value (AOV).
5. **Logistics Optimization**: Transit times vary significantly by vehicle type. Traditional delivery vans generally take longer, whereas electric bikes and scooters provide faster deliveries in urban centers.
6. **Return Control**: Return rates remain higher on specific product categories (like smartwatches), suggesting a need to investigate product quality or description accuracy.
7. **Discount Impact**: Heavily discounted products drive massive order volumes but noticeably erode total profit margins.

---

## 🚀 How to Run the Analysis

### 📋 Prerequisites
Ensure you have Python installed, along with the required libraries:
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 🏃 Running the Notebook
1. Clone or navigate to the directory where the files are located.
2. Start the Jupyter notebook environment:
   ```bash
   jupyter notebook
   ```
3. Open `EDASales.ipynb` and run the cells sequentially to reproduce the visualizations and insights.
# BOAT-Sales-Analysis
