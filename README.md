# Customer Orders and Returns Analysis

## Table of Contents
- [Background and Overview](#background-and-overview)
- [Data Dictionary](#data-dictionary)
- [Executive Summary](#executive-summary)
- [Insight Deep Dive](#insight-deep-dive)
  - [Overall Metrics](#overall-metrics)
  - [Return Rates and Purchase Behavior](#return-rates-and-purchase-behavior)
  - [Returns by Age Group and Gender](#returns-by-age-group-and-gender)
  - [Returns by Product Group and Gender](#returns-by-product-group-and-gender)
  - [Returns by Product Group and Age Groups](#returns-by-product-group-and-age-groups)
  - [Logistic Regression Analysis](#logistic-regression-analysis)
  - [SHAP Values Interpretation](#shap-values-interpretation)
- [Recommendations](#recommendations)
- [Limitations and Further Studies](#limitations-and-further-studies)

## Background and Overview

Understanding how customer behave is critical for enhancing satisfaction, optimizing operations, and increasing revenues. The objective is to identify trends and actionable insights that can reduce return rates, enhance customer retention, and ultimately contribute to improved profitability

## Data Dictionary

| **Column Name**        | **Description**                                            |
|------------------------|------------------------------------------------------------|
| `user_id`              | Unique identifier for each customer                        |
| `age`                  | Age of the customer                                        |
| `gender`               | Gender of the customer (e.g., Male, Female)                |
| `city`                 | City where the customer resides                            |
| `traffic_source`       | Source through which the customer arrived (e.g., Ads, Organic Search) |
| `order_id`             | Unique identifier for each order                           |
| `status`               | Status of the order (e.g., Delivered, Returned)            |
| `product_id`           | Unique identifier for each product                         |
| `product_category`     | Category of the product (e.g., Accessories, Activewear)    |
| `product_name`         | Name of the product                                        |
| `product_retail_price` | Retail price of the product                                |
| `cost`                 | Cost incurred for the product                              |
| `sale_price`           | Sale price at which the product was sold                   |
| `returned_at`          | Timestamp when the product was returned                    |
| `event_type`           | Type of event associated with the order                    |
| `dc_name`              | Distribution center handling the order                     |
| `d_lat`                | Latitude of the distribution center                        |
| `d_long`               | Longitude of the distribution center                       |
| `u_lat`                | Latitude of the user location                              |
| `u_long`               | Longitude of the user location                             |
| `dc2c_distance`        | Distance between distribution center and customer          |
| `created_at`           | Timestamp when the order was created                       |
| `shipped_at`           | Timestamp when the order was shipped                       |
| `delivered_at`         | Timestamp when the order was delivered                     |
| `prep_time`            | Time taken to prepare the order for shipment               |
| `delivery_time`        | Time taken to deliver the order to the customer             |
| `total_time`           | Total time from order creation to delivery                 |
| `num_of_item`          | Number of items in the order                                |

## Executive Summary

This analysis reveals that out of 2,612 unique customers, there were 3,113 total orders resulting in 6,008 returns. This high return rate, approximately 15%, indicates a significant revenue loss estimated at 28% due to returned items. Additionally, the repeat purchase rate stands at around 16%, suggesting opportunities to enhance customer retention. The data also highlights specific demographics and product categories with higher return rates, providing targeted areas for improvement.

## Insight Deep Dive

### Overall Metrics

- **Number of Unique Customers:** 2,612
- **Total Orders:** 3,113
- **Total Returns:** 6,008
- **Total Revenue:** \$649,661.10
- **Total Items Sold:** 40,732

These metrics provide a foundational understanding of the customer base and transactional volume. Notably, the number of returns exceeds the number of orders, indicating that multiple items per order are being returned.

### Return Rates and Purchase Behavior

- **Return Rate:** 15.04%
- **Repeat Purchase Rate:** 15.84%
- **Revenue Loss from Returns:** 28.13%
- **Percentage of Sales Reversed:** 14.58%
- **Percentage of Repeat Returners:** 1.17%

A return rate of approximately 15% is significant and contributes to a substantial revenue loss of over a quarter of total sales. The repeat purchase rate suggests that while some customers are returning, a smaller fraction are making multiple purchases, potentially indicating issues with customer satisfaction or product quality.

### Returns by Age Group and Gender

| **Age Group** | **Female Returns** | **Male Returns** |
|---------------|--------------------|------------------|
| <18           | 312                | 270              |
| 18-24         | 414                | 409              |
| 25-34         | 528                | 448              |
| 35-44         | 601                | 456              |
| 45-54         | 481                | 365              |
| 55-64         | 543                | 590              |
| 65+           | 289                | 322              |

**Insights:**
- The highest number of returns occurs in the 35-44 age group, particularly among females.
- Males in the 55-64 age group have the highest returns compared to other male age groups.
- Younger age groups (<18 and 18-24) show substantial return activity, indicating potential issues with product suitability or expectations.

### Returns by Product Group and Gender

| **Product Group**                   | **Female Returns** | **Male Returns** |
|-------------------------------------|--------------------|------------------|
| Accessories                         | 137                | 215              |
| Active                              | 129                | 152              |
| Blazers and Jackets                 | 112                | 0                |
| Clothing Sets                       | 9                  | 0                |
| Dresses                             | 253                | 0                |
| Fashion Hoodies and Sweatshirts     | 224                | 267              |
| Intimates                           | 436                | 0                |
| Jeans                               | 214                | 192              |
| Jumpsuits and Rompers               | 27                 | 0                |
| Leggings                            | 97                 | 0                |
| Maternity                           | 117                | 0                |
| Outwear and Coats                   | 108                | 251              |
| Pants                               | 0                  | 241              |
| Pants and Capris                    | 121                | 0                |
| Plus                                | 188                | 0                |
| Shorts                              | 106                | 185              |
| Skirts                              | 73                 | 0                |
| Sleep and Longes                    | 147                | 216              |
| Socks                               | 0                  | 199              |
| Socks and Hosiery                   | 127                | 0                |
| Suits                               | 29                 | 0                |
| Suits and Sport Coats               | 0                  | 143              |
| Sweaters                            | 177                | 204              |
| Swim                                | 184                | 204              |
| Tops and Tees                       | 153                | 183              |
| Underwear                           | 0                  | 208              |

**Insights:**
- **Intimates** have the highest number of returns among female product categories, indicating possible sizing or quality issues.
- **Accessories** and **Fashion Hoodies and Sweatshirts** are popular return categories for both genders.
- Certain categories like **Blazers and Jackets**, **Clothing Sets**, and **Dresses** have zero returns for males, suggesting these products are primarily purchased by females.
- **Pants**, **Socks**, and **Underwear** are significant return categories for males, potentially highlighting fit or style preferences.

### Returns by Product Group and Age Groups

#### Accessories
- Highest returns in 18-24 and 55-64 age groups.

#### Active
- Consistent returns across all age groups, with a peak in <18 and 55-64.

#### Blazers and Jackets
- Returns concentrated in 35-44 age group.

#### Clothing Sets
- Minimal returns, primarily in 25-34 and 65+.

#### Dresses
- Significant returns in 35-44 and 45-54 age groups.

#### Fashion Hoodies and Sweatshirts
- High returns across 25-34, 35-44, and 55-64 age groups.

#### Intimates
- Major returns in 35-44 age group.

#### Jeans
- Returns spread across all age groups, peaking in 18-24 and 35-44.

#### Jumpsuits and Rompers
- Low returns, distributed among younger and older age groups.

#### Leggings
- Returns mainly in 25-34 and 35-44 age groups.

#### Maternity
- Returns primarily in 35-44 and 55-64 age groups.

#### Outwear and Coats
- Highest returns in 25-34 age group.

#### Pants
- Consistent returns across 18-24, 25-34, and 55-64.

#### Pants and Capris
- Returns notable in 55-64 age group.

#### Plus
- Returns distributed across various age groups, with peaks in 25-34 and 35-44.

#### Shorts
- Highest returns in 25-34 and 55-64 age groups.

#### Skirts
- Limited returns, mainly in younger age groups.

#### Sleep and Longes
- High returns in 25-34 and 55-64 age groups.

#### Socks and Hosiery
- Returns spread across 35-44 and 55-64 age groups.

#### Suits and Sport Coats
- Returns notable in 25-34 and 65+ age groups.

#### Sweaters
- High returns in 25-34 and 65+ age groups.

#### Swim
- Significant returns in 25-34 and 55-64 age groups.

#### Tops and Tees
- Returns spread across 25-34 and 55-64 age groups.

#### Underwear
- Returns primarily in 45-54 and 55-64 age groups.

**Insights:**
- Certain product categories show age-specific return patterns, suggesting differing preferences or sizing issues.
- Middle-aged groups (25-44) exhibit higher return rates across multiple product categories, indicating potential areas for targeted improvements.

### Logistic Regression Analysis

```plaintext
Optimization terminated successfully.
         Current function value: 0.586855
         Iterations: 5
                           Logit Regression Results                           
===============================================================================
Dep. Variable:          status_binary   No. Observations:                21,947
Model:                          Logit   Df Residuals:                    21,937
Method:                           MLE   Df Model:                             9
Date:                Sat, 05 Oct 2024   Pseudo R-squ.:                0.001676
Time:                        15:27:20   Log-Likelihood:                -12,880.
converged:                       True   LL-Null:                       -12,901.
Covariance Type:            nonrobust   LLR p-value:                 1.940e-06
=======================================================================================
                       coef    std err          z      P>|z|      [0.025      0.975]
----------------------------------------------------------------------------------------
const               -0.6339      0.070     -8.996      0.000      -0.772      -0.496
delivery_time        -3.876e-06   7.27e-06     -0.533      0.594   -1.81e-05    1.04e-05
age                   -0.0028      0.001     -3.169      0.002      -0.005      -0.001
gender                -0.0305      0.031     -0.984      0.325      -0.091       0.030
city                 -3.774e-06    4.3e-05     -0.088      0.930    -8.8e-05    8.04e-05
product_category      -0.0048      0.002     -2.412      0.016      -0.009      -0.001
product_retail_price   0.0013      0.001      0.891      0.373      -0.002       0.004
num_of_item           -0.0422      0.015     -2.890      0.004      -0.071      -0.014
revenue               -0.0017      0.003     -0.641      0.522      -0.007       0.004
dc2c_distance        -4.569e-05   1.33e-05     -3.445      0.001   -7.17e-05   -1.97e-05
