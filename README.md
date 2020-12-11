# Delivery-Time-Prediction

It is very important for food delivery company to get this right, as it has a big impact on consumer experience. Order lateness / underprediction of delivery time is of particular concern as past experiments suggest that underestimating delivery time is roughly twice as costly as overestimating it. Orders that are very early / late are also much worse than those that are only slightly early / late. In this project, I will build a model to predict the estimated time taken for a delivery.

The target of the project is predicting the total seconds value between ‘created_at’ and ‘actual_delivery_time’, which is also known as total delivery duration. In the following, the compelling insights and findings will be presented, and the results and error measurements from each model will be compared and displayed in the model session. Last, I will discuss the quality and reliability of the results. Conclusion and recommendations will be addressed, and I will also present areas that I could’ve improved in and how to predict future results.

## 1.EDA

For this project, I’m provided a historical data contains a subset of deliveries received at DoorDash in early 2015 in a subset of the cities with 197428 records. Several columns from the dataset contain some missing values, after digging out the data, I decided to use different approaches to either fill up or drop the missing values for each column. For total_onshift_dashers, total_busy_dashers, and total_outstanding_orders, i fill up with the average value from the same market and created time, because I assumed that the number of the available dashers working within 10 miles of the store should be similar in the same created hour and region.
- market_id: I drop them
- actual_delivery_time: only 7 records, I drop them
- store_primary_category: I will ignore this column
- order_protocol: I will ignore this column
- total_onshift_dashers: fill up with the average total_onshift_dashers at same market id and created hour.
- total_busy_dashers: fill up with the average total_onshift_dashers at same market id and created hour.
- total_outstanding_orders: fill up with the average total_onshift_dashers at same market id and created hour.

Moreover, there were some values that were anomalous. Some columns contain negative values, which didn’t make sense. I simply make those negative numbers to 0. There are 3 outliers in actual delivery time. They took over 97 hours, so I remove those outliers as well. In addition, I created additional variables such as day of the week of creating time, the hour of creating time, actual delivery time in second to improve model performance. Also, recategorize some of the variables can help to check if a certain group is significant.

First, I looked up the demand distribution, the result as below charts shown. 

![Test Image 1](“P1.png”)



The demands are variety by different markets, day of the week, and created hour. Markets 2 and 4 might be a bigger region which has more demand than other markets. Most of the orders are from the weekend. Demand is getting less from 5 am to 6 pm. The peak time for demand is 2 am. Second, I also examined if the delivery time varies by markets and created time. The result is below shown.

| col 1      | col 2      |
|------------|-------------|
| image 1 | image 2 |

