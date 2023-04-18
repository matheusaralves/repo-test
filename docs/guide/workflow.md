[< Home](/)

# Workflow

As seen in the abstract, the application **automates** the manual process that was executed daily, which was the execution of the following query:
```sql
CREATE OR REPLACE TABLE `meli-bi-data.SBOX_PFOFFDE.fraud-moving-sellers-op`
AS (
select cus_cust_id_sel as seller, sit_site_id as site, "off" as config_id, industry_id as industry, flow_type as flow, industry_id_new as new_industry, "salesforce_pedidos_flex" as table_name from `meli-bi-data.SBOX_PF_OFF.salesforce_pedidos_flex`
union all
select cus_cust_id_sel as seller, sit_site_id as site, "off" as config_id, industry_id as industry, flow_type as flow, industry_id_new as new_industry, "CX_ListadoSel_ConReclamo_trusted_paraFlex" as table_name from `meli-bi-data.SBOX_PF_OFF.CX_ListadoSel_ConReclamo_trusted_paraFlex`
union all
select cus_cust_id_sel as seller, sit_site_id as site, "off" as config_id, industry_id as industry, flow_type as flow, industry_id_new as new_industry, "movimiento_industrias" as table_name from `meli-bi-data.SBOX_PF_OFF.movimiento_industrias`
union all
select cus_cust_id_sel as seller, sit_site_id as site, "off" as config_id, industry_id as industry, flow_type as flow, industry_id_new as new_industry, "List_sellers_trusted_api_cow_OP" as table_name from `meli-bi-data.SBOX_PF_OFF.List_sellers_trusted_api_cow_OP`
```

For effective automation, proceed with the following workflow:

First, all **Sellers** that need to be moved from **BigQuery** are selected and filtered, so that any field that has a null value is removed.

Therefore, a first filtering is performed so that only Sellers with industry equal to **DEFAULT** are used and those with different ones are removed.

After this filtering, the **prediction** is defined that will be used later in **[Naomi](https://naomi.adminml.com/tree)**. This prediction will be responsible for concatenating different information in a single field.

Now comes the time to communicate with the **[fraud-risk](https://web.furycloud.io/fraud-risk-config/summary)** application, in which sellers will only be present at this endpoint if they have a different default industry.

For every **50 sellers** searched, there is a **5-second pause** in order not to overload the endpoint. This is done through a **“sleep”**.

In **Naomi**, the aforementioned prediction will concatenate flow, site, config and new industry with a “_” between each of these fields.

Still in **Naomi**, when accessing this prediction, he separates it into different “portions” of **10 sellers**, with the aim of doing a pagination.

This is done in the following way: for each prediction, it goes through the list of all sellers that need to be moved and identifies whether that seller refers to that prediction. If positive, the seller is added to a list that will later go through the pagination process mentioned above.

This pagination of **10 out of 10** sellers is also done so that the service is not overloaded.

With that, a **PUT** is done by the application every 10 selected sellers and for each **PUT** , there is a **5-second sleep**.

After this step, there is a new **fraud-risk filter**, to filter out who still has the industry in **DEFAULT**. At that moment, **2 different lists** are made, one related to the data that came from **Naomi** and another that went through the filter.

One list deals with sellers that have been moved and those that are still in default.

Thus, the data about sellers that have been moved is then stored in the **database**, feeding its respective tables.

After insertion in the database, an **E-MAIL** is sent informing the changes that have occurred.
