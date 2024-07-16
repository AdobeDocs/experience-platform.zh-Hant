---
title: 傳回專案資料型別
description: 瞭解退貨專案體驗資料模型(XDM)資料型別。
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# [!UICONTROL 傳回專案]資料型別

[!UICONTROL 退貨專案]是標準的體驗資料模型(XDM)資料型別，會擷取與購買專案的退貨程式相關的重要細節。

![傳回專案資料型別的圖表。](../images/data-types/return-item.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL 傳回狀態] | `returnStatus` | 字串 | 傳回專案的狀態（例如，「擱置中」或「已核准」）。 |
| [!UICONTROL 退貨原因] | `returnReason` | 字串 | 要求專案退貨的原因。 |
| [!UICONTROL 傳回專案條件] | `returnItemCondition` | 字串 | 要求傳回的專案的條件。 |
| [!UICONTROL 傳回解析度] | `returnResolution` | 字串 | 從退貨中預期的所需解決方式或結果（例如，退款或交換）。 |
| [!UICONTROL 要求的退貨數量] | `returnQuantityRequested` | 整數 | 購物者要求退貨的料號數量。 |
| [!UICONTROL 已授權退貨數量] | `returnQuantityAuthorized` | 整數 | 授權退回的料號數量。 |
| [!UICONTROL 收到的退貨數量] | `returnQuantityReceived` | 整數 | 收到的退回料號數量。 |
| [!UICONTROL 已核准的退貨數量] | `returnQuantityApproved` | 整數 | 退貨完全完成且已核准的料號數量。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
