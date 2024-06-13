# SQL Advertising Campaign Analysis

## Description

This project explores how digital advertising campaigns perform using a simulated dataset. It uses SQL to analyze campaigns, ad groups, ads, clicks, and impressions. The analysis focuses on understanding campaign budgets, total impressions per campaign, and how ads perform based on metrics like cost-per-click and conversion rates on different platforms. Insights include which devices users click ads on the most and how different campaigns compare in terms of cost and engagement.

## Objectives

- Count the number of campaigns.
- List all ad groups with their campaign name.
- Count the number of ads in each ad group.
- Calculate the total budget for each campaign.
- Calculate the total impressions for each ad.
- Calculate the average cost per click for each ad type.
- List all clicks with ad names and devices.
- Calculate the total cost of clicks for each ad.
- Calculate the total number of clicks for each campaign.
- Calculate the total cost per campaign.
- Identify campaigns with more than 10,000 impressions.
- Identify ads with the highest conversion rate.
- Calculate the total clicks for each device type.
- Calculate the conversion rate for each platform.

## SQL Queries

1. **List all campaigns:**
```sql
   SELECT * FROM campaigns;
```
![Screenshot 2024-06-12 230719](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/ed90353d-6453-483d-a938-f291704692da)

2. **List all ad groups with their campaign name:**
```sql
SELECT ag.adgroup_name, c.campaign_name 
FROM adgroups ag
JOIN campaigns c ON ag.campaign_id = c.campaign_id;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/4775efb6-8e46-42a6-ace8-44d96e411539)

3. **Count the number of ads in each ad group:**
```sql
SELECT adgroup_id, COUNT(*) AS ad_count 
FROM ads 
GROUP BY adgroup_id;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/f9f13868-0747-4552-8de4-0575f28a21ca)

4. **Calculate the total budget for each campaign:**
```sql
SELECT campaign_name, budget 
FROM campaigns;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/a82112a3-c667-443f-896e-3533d8fe64b3)

5. **Calculate the total impressions for each ad:**
```sql
SELECT ad_name, SUM(impressions) AS total_impressions 
FROM ads 
GROUP BY ad_name;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/6b060b65-1113-4f9f-ac06-056d7bed6fa8)

6. **Calculate the average cost per click for each ad type:**
```sql
SELECT ad_type, AVG(cost_per_click) AS avg_cost_per_click 
FROM ads 
GROUP BY ad_type;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/e0b4f3f9-5765-4fb7-b8a4-a84c3fd51651)

7. **List all clicks with ad names and devices:**
```sql
SELECT cl.click_id, a.ad_name, cl.device 
FROM clicks cl
JOIN ads a ON cl.ad_id = a.ad_id;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/1d2fb9e7-b486-42ad-ba8e-4cd8bed973ad)

8. **Calculate the total cost of clicks for each ad:**
```sql
SELECT a.ad_name, SUM(cl.cost) AS total_click_cost 
FROM clicks cl
JOIN ads a ON cl.ad_id = a.ad_id 
GROUP BY a.ad_name;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/a1dc9aed-f6c9-4be4-867d-f683afc93cd8)

9. **Calculate the total number of clicks for each campaign:**
```sql
SELECT c.campaign_name, COUNT(cl.click_id) AS total_clicks 
FROM campaigns c
JOIN adgroups ag ON c.campaign_id = ag.campaign_id
JOIN ads a ON ag.adgroup_id = a.adgroup_id
JOIN clicks cl ON a.ad_id = cl.ad_id
GROUP BY c.campaign_name;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/11ff520b-249d-4f1f-978d-b044b4cae2b1)

10. **Calculate the total cost per campaign:**
```sql
SELECT c.campaign_name, SUM(cl.cost) + SUM(i.cost) AS total_cost 
FROM campaigns c
JOIN adgroups ag ON c.campaign_id = ag.campaign_id
JOIN ads a ON ag.adgroup_id = a.adgroup_id
LEFT JOIN clicks cl ON a.ad_id = cl.ad_id
LEFT JOIN impressions i ON a.ad_id = i.ad_id
GROUP BY c.campaign_name;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/65db7e3a-40a9-4be7-9e2e-40cae5a4a508)

11. **Identify ads with the highest conversion rate:**
```sql
SELECT ad_name, conversion_rate 
FROM ads 
ORDER BY conversion_rate DESC 
LIMIT 5;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/49c7d6c0-24e0-4806-94fd-fd119a6bf533)

12. **Calculate the total clicks for each device type:**
```sql
SELECT device, COUNT(*) AS total_clicks 
FROM clicks 
GROUP BY device;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/7afadf3e-52eb-446e-84fd-356a465d980d)

13. **Calculate the conversion rate for each platform:**
```sql
SELECT c.platform, AVG(a.conversion_rate) AS avg_conversion_rate 
FROM campaigns c
JOIN adgroups ag ON c.campaign_id = ag.campaign_id
JOIN ads a ON ag.adgroup_id = a.adgroup_id
GROUP BY c.platform;
```
![image](https://github.com/sarvaniduggirala/SQL-Advertising-Campaign-Analysis/assets/158331818/bef5cf5f-fe4d-4526-852b-7b2142353afc)

# Conclusion
By employing aggregate functions, joins, and data manipulation techniques, we explored campaign budgets, ad group compositions, and performance metrics such as impressions, clicks, and conversion rates. These SQL operations provided actionable insights into campaign effectiveness, highlighting my proficiency in SQL for data analysis and decision-making in digital marketing contexts.
