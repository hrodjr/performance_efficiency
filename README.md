# Performance Efficiency
- Purpose: Provide key performance indicators and create 2-4 actionable suggestions for how the business could improve or be run more efficiently in the following year.
- Goal: Provide recommendations to improve efficiency.
# Project Details
- Libraries
    - pandas
    - numpy
    - matplotlib
    - sklearn
    - scipy
    - seaborn
# Pipeline
My methodology follow is the data pipeline; plan, acquire, prepare, explore, model and deliver.

## Plan
1. Acquire and prepare data challenge csv
2. Analysis based on classification

## Acquire
1. Acquired data challenge provided csv
##### Takeaways
1. Revenue change dtype to timedate
2. Drop order ID
3. Lower case
##### Initial Thoughts
1. Net Revenue by month, sales_rep, escrow_officer
2. Encode property type, order type and change dtype
3. Group by transaction type
4. check for outliers
5. explore and develop hypothesis then test (type of stat test??)

## Prepare
1. dtypes look good.
2. encode and change dtypes. (Encode property type, order type and change dtype)
3. No duplicates
4. did a value count of net sales that are equal to zero. 13 with no sales.
5. drop rows with zero net_revenue.
6. dropped 13 rows with 0 value
7. dropped another 4 rows above 40000 (outliers)
8. Provided downloadable prepared csv

## Explore
1. Explored using Univariate, Bivariate and Multivariant exploration
2. Further exploration and prediction done on <a href="https://public.tableau.com/views/PerformanceEfficiency/Net_RevenuebyType?:language=en-US&:display_count=n&:origin=viz_share_link">Tableau</a>.
##### Takeaways
1. identified possible outliers:
    - net_revenue
    - residential
    - title
    - resale
2. outliers/data too close to remove

### Hypothesis Testing
Chi2

1. Are title orders dependent on resales? Null Rejected
2. Are title orders dependent on residential sales? Null Rejected

Two Sample T-Test
1. null: There is no difference in net_revenue for residential and commercial property types. Null Rejected
2. null: There is no difference in net_revenue for title and title & escrow order types. Null Rejected
3. null: There is no difference in net_revenue for resale and refinance orders. Null Rejected

##### Key Takeaways
1. 334, 355, 357 make up less than four percent of orders
    - Unknowns: location of these three locations
        - Question: Does location affect sales?
2. Residential orders make 4.5% of sales.
    - Drop residential orders
        - Question: Will dropping residential orders decrease sales?
    -Unknown: cost difference in marketing residential orders over cost of orders.
3. Order type 'Title' makes up 2.9% of orders.
    - Drop title orders and only provide both.
        - Question: Will dropping title orders decrease sales?
    - Unknown: cost difference in marketing title orders over cost of orders.
4. Resale makes up 78% of orders
    - Refinance makes up 22%
    - Keep: focus refinance in different areas
        - Question: In what cost center does refinance do better? - Does location make a difference in refinance orders?
5. Drop outliers
6. Sales reps (15 with less than 100 orders)
        - Question: Are they in bad locations?
    - sales rep by location
7. Escrow Officer (18 with less than 100 orders)
        - location? escrow officer to laction
    - Unkown: Excrow Officer duties, full/part time employees, self-employed    
    
## Model
1. Classification Mchine Learning (WORKING)

### Takeaways

# Data Dictionary
| **Value**      | **Description**                                                                                                               | **dtype**  |
|----------------|-------------------------------------------------------------------------------------------------------------------------------|------------|
| revenue_month  | Calendar month the revenue was received. This is usually when the order closes. The median time to close an order is 30 days. | datetime64 |
| sales_rep      | ID for the sales representative that sourced the order. An ID of zero represents a null value in the data                     | int64      |
| escrow_officer | ID for the associate responsible for processing the order. An ID of zero represents a null value in the data.                 | int64      |
| cost_center    | ID for the branch that processed the order. The branches are located throughout the state and in a variety of metro areas.    | int64      |
| net_revenue    | The revenue metric we track for performance.                                                                                  | float64    |
| residential    | "1 indicates a residential property, where 0 represents a commercial property."                                               | int64      |
| title          | "1 indicates title only order, where 0 indicates a title & escrow order."                                                     | int64      |
| resale         | "1 indicates a resale order, where 0 indicates a refinance order."                                                            | int64      |
