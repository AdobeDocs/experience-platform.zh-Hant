---
title: 傳回專案資料型別
description: 瞭解退貨專案體驗資料模型(XDM)資料型別。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL 傳回專案] 資料型別

[!UICONTROL 傳回專案] 是標準的體驗資料模型(XDM)資料型別，可擷取與購買專案回訪流程相關的重要細節。

![退貨專案資料型別的圖表。](../images/data-types/return-item.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL 傳回狀態] | `returnStatus` | 字串 | 傳回專案的狀態（例如，「擱置中」或「已核准」）。 |
| [!UICONTROL 退貨原因] | `returnReason` | 字串 | 要求專案退貨的原因。 |
| [!UICONTROL 傳回專案條件] | `returnItemCondition` | 字串 | 要求傳回的專案的條件。 |
| [!UICONTROL 傳回解析度] | `returnResolution` | 字串 | 從退貨中預期的所需解決方式或結果（例如，退款或交換）。 |
| [!UICONTROL 要求的退貨數量] | `returnQuantityRequested` | 整數 | 購物者要求退貨的料號數量。 |
| [!UICONTROL 已授權的退貨數量] | `returnQuantityAuthorized` | 整數 | 授權退回的料號數量。 |
| [!UICONTROL 退貨收貨數量] | `returnQuantityReceived` | 整數 | 收到的退回料號數量。 |
| [!UICONTROL 退貨數量已核准] | `returnQuantityApproved` | 整數 | 退貨完全完成且已核准的料號數量。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
