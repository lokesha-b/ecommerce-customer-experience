# Olist Ecommerce Initial EDA Summary

## Dataset Shape

| table                |    rows |   columns |
|:---------------------|--------:|----------:|
| customers            |   99441 |         5 |
| orders               |   99441 |         8 |
| order_items          |  112650 |         7 |
| payments             |  103886 |         5 |
| reviews              |   99224 |         7 |
| products             |   32951 |        11 |
| sellers              |    3095 |         4 |
| geolocation          | 1000163 |         5 |
| category_translation |      71 |         2 |


## Key Metrics

- Order coverage: 2016-09-04 to 2018-10-17
- Total orders: 99,441
- Delivered orders: 96,478 (97.0%)
- Unique customers: 96,096
- Repeat customers among delivered orders: 2,801 (3.0%)
- Delivered item revenue: $13,221,498.11
- Average delivered order value: $137.04
- Median delivered order value: $86.57
- Late delivery rate: 8.1%
- Low review rate (score <= 2): 12.8%
- Average review score when on-time/early: 4.29
- Average review score when late: 2.57


## Top Customer States by Revenue

| customer_state   |   orders |    revenue |
|:-----------------|---------:|-----------:|
| SP               |    40501 | 5067633.16 |
| RJ               |    12350 | 1759651.13 |
| MG               |    11354 | 1552481.83 |
| RS               |     5345 |  728897.47 |
| PR               |     4923 |  666063.51 |
| SC               |     3546 |  507012.13 |
| BA               |     3256 |  493584.14 |
| DF               |     2080 |  296498.41 |
| GO               |     1957 |  282836.70 |
| ES               |     1995 |  268643.45 |


## Top Product Categories by Revenue

| primary_category      |   orders |    revenue |
|:----------------------|---------:|-----------:|
| health_beauty         |     8621 | 1234792.71 |
| watches_gifts         |     5455 | 1160214.09 |
| bed_bath_table        |     9240 | 1036092.78 |
| sports_leisure        |     7478 |  952768.94 |
| computers_accessories |     6520 |  892264.23 |
| furniture_decor       |     6208 |  715444.83 |
| housewares            |     5671 |  612859.07 |
| cool_stuff            |     3516 |  607466.01 |
| auto                  |     3804 |  580935.21 |
| garden_tools          |     3411 |  470175.40 |


## Highest Missing Rates in Master Table

| field                         | missing_rate   |
|:------------------------------|:---------------|
| delivery_days                 | 3.0%           |
| order_delivered_customer_date | 3.0%           |
| primary_category              | 2.2%           |
| order_delivered_carrier_date  | 1.8%           |
| item_revenue                  | 0.8%           |
| item_count                    | 0.8%           |
| seller_count                  | 0.8%           |
| freight_value                 | 0.8%           |
| review_score                  | 0.8%           |
| order_approved_at             | 0.2%           |
| payment_types                 | 0.0%           |
| payment_installments          | 0.0%           |


## Generated Visuals

- `outputs/monthly_revenue.png`
- `outputs/top_categories.png`
- `outputs/delivery_days_by_review.png`