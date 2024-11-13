---
title: 使用AI助理進行XDM欄位探索
description: 請閱讀本檔案，瞭解如何使用AI Assistant進行Experience Data Model (XDM)欄位探索。
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# 使用AI助理的XDM欄位探索

>[!AVAILABILITY]
>
>此功能Alpha中，可能不適用於您的組織。 若要參與Alpha計畫並存取此功能，請聯絡您的Adobe客戶團隊。

您可以使用AI助理來搜尋和探索Experience Data Model (XDM)欄位，然後使用這些欄位在Experience Platform中建立目標對象。

請閱讀下表，瞭解AI Assistant中XDM欄位探索支援的查詢和提示模式。

>[!TIP]
>
>雖然查詢和提示模式在不同使用案例中可能相同，但問題的確切表述將取決於用於給定沙箱的XDM欄位和結構描述。

| 查詢型別 | 查詢/提示模式 | 範例 |
| --- | --- | --- |
| 依資料網域或區域的XDM欄位探索 | 顯示用來表示{DATA_DOMAIN/AREA}的XDM欄位。 | <ul><li>顯示用來代表同意資料的XDM欄位。</li><li>顯示用來代表電子郵件訂閱相關資訊的XDM欄位。</li></ul> |
| 依一般欄位名稱探索的XDM欄位 | <ul><li>顯示與{DATA_DOMAIN/AREA}相關的XDM欄位。</li><li>哪些XDM欄位包含{GENERAL_FIELD_NAME}。</li></ul> | <ul><li>顯示與訂單相關的XDM欄位。</li><li>顯示與互動詳細資料相關的XDM欄位。</li><li>哪個XDM欄位包含訪客ID？</li><li>哪個XDM欄位包含產品類別？</li></ul> |
| 依資料模型譜系探索XDM欄位 | <ul><li>顯示包含{GENERAL_FIELD_NAME}的{FIELD_GROUP/CLASS_NAME}的所有欄位。</li><li>什麼是XDM欄位{GENERAL_FIELD_NAME}的{FIELD_GROUP/CLASS_NAME}？</li></ul> | <ul><li>顯示包含產品資料之欄位群組的所有欄位。</li><li>顯示包含分析資料之欄位群組的所有欄位。</li><li>XDM欄位名字的類別為何？</li><li>XDM欄位電子郵件訂閱的類別是什麼？</li></ul> |
| 提示取得增強型說明以及欄位名稱 | {FIELD_DISCOVERY_QUERY}。 也包含增強型說明。 | <ul><li>顯示用來代表同意資料的XDM欄位。 也包含欄位的增強型說明。</li><li>顯示與互動詳細資料相關的XDM欄位。 也包含欄位的增強型說明。</li></ul> |

{style="table-layout:auto"}