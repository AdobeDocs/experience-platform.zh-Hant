---
title: 帳戶設定檔深入分析
description: 探索為您的帳戶設定檔深入分析提供支援的SQL，並使用這些查詢產生自訂深入分析，以進一步探索您的客戶及其消費者體驗。
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 帳戶設定檔深入分析

[帳戶設定檔](../../rtcdp/accounts/account-profile-overview.md)用於合併來自各種來源的帳戶資訊，包括多個行銷管道和組織系統。 此統一檢視可全面瞭解客戶帳戶，加強B2B行銷活動。 從資料模型分析衍生的深入解析可讓您的Adobe Real-time Customer Data Platform B2B資料更易於存取、理解，並更能對決策產生影響。

存取提供您深入分析能力的SQL，可以更瞭解您的B2B資料，並產生您自己的高度自訂且可重複使用的深入分析，以進一步探索您的客戶帳戶資訊。 使用現有的Real-Time CDP資料模型SQL作為靈感，根據您獨特的業務需求建立查詢，將原始資料轉換為可採取行動的新見解。

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

下列見解全部都可以用作[帳戶設定檔儀表板](../guides/account-profiles.md)或[自訂儀表板](../standard-dashboards.md)的一部分。 請參閱[自訂總覽](../customize/overview.md)，瞭解如何自訂您的儀表板或[在Widget程式庫和[使用者定義儀表板](../standard-dashboards.md#create-widget)中建立及編輯新Widget](../customize/custom-widgets.md)的說明。

## 已新增的帳戶輪廓 {#account-profiles-added}

此深入分析所回答的問題：

- 在指定期間內新增了多少帳戶設定檔？

+++選取以顯示產生此深入分析的SQL

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## 依產業的新帳戶 {#accounts-by-industry}

此深入分析所回答的問題：

- 帳戶設定檔所屬的前五大產業為何？

+++選取以顯示產生此深入分析的SQL

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## 新帳戶（依型別） {#accounts-by-type}

此深入分析所回答的問題：

- 依帳戶型別區分的帳戶計數是多少？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## 已新增的機會 {#opportunities-added}

此深入分析所回答的問題：

- 在指定期間內新增了多少商機？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## 依個人角色的新機會 {#opportunities-by-person-role}

此深入分析所回答的問題：

- 機會中各種角色的相對大小和計數為何？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## 按收入顯示的新商機 {#opportunities-by-revenue}

此深入分析所回答的問題：

- 依收入排名的20大商機為何（以美元計）？

+++選取以顯示產生此深入分析的SQL

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## 按狀態和階段的新機會 {#opportunities-by-status-and-stage}

此深入分析所回答的問題：

- 有哪些商機，在銷售或行銷漏斗的哪個階段？
- 有哪些已結束的商機？在銷售或行銷漏斗的哪個階段？

+++選取以顯示產生此深入分析的SQL

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## 贏得新商機 {#opportunities-won}

此深入分析所回答的問題：

- 已順利關閉或完成的商機數目為何？

+++選取以顯示產生此深入分析的SQL

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## 贏得的機會（折線圖） {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

此深入分析所回答的問題：

- 在指定期間內，有多少機會已成功關閉或完成（成功）？

+++選取以顯示產生此深入分析的SQL

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## 後續步驟

閱讀本檔案後，您現在瞭解產生帳戶設定檔儀表板深入分析的SQL，以及此分析解決哪些常見問題。 您現在可以編輯並反複處理SQL，以產生您自己的深入分析。

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

您也可以閱讀並瞭解產生[設定檔](./profiles.md)、[對象](./audiences.md)和[目的地](./destinations.md)儀表板之深入分析的SQL。
