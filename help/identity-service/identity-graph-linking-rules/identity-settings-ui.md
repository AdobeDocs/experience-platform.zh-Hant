---
title: 身分設定UI
description: 瞭解如何使用身分設定使用者介面。
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 605aa5ed2db2bfd7f787f2dff9fa00cee2afbce6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 身分設定UI

>[!AVAILABILITY]
>
>此功能尚未推出；身分圖表連結規則的Beta版計畫預計於7月在開發沙箱上開始。 如需參與率條件的詳細資訊，請聯絡您的Adobe客戶團隊。

身分設定是Adobe Experience Platform Identity Service UI中的功能，可用來指定唯一的名稱空間及設定名稱空間優先順序。

請閱讀本指南，瞭解如何使用身分設定工具。

## 先決條件

開始使用身分設定前，請先閱讀下列檔案：

* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [名稱空間優先順序](./namespace-priority.md)
* [圖表模擬](./graph-simulation.md)

## 設定您的身分設定

若要存取身分設定，請導覽至Adobe Experience Platform UI中的Identity Service工作區，然後選取 **[!UICONTROL 設定]**.

![已選取身分設定按鈕。](../images/rules/identity-ui.png)

身分設定頁面隨即顯示，系統會向您顯示一則確認訊息，提醒您先在開發沙箱中測試及驗證身分設定，然後再在生產沙箱中完成設定。

![身分設定頁面。](../images/rules/identity-settings.png)

身分設定頁面分為兩個區段： [!UICONTROL 人員名稱空間] 和 [!UICONTROL 裝置或Cookie名稱空間]. 個人名稱空間是適用於單一個人的識別碼。 可以是跨裝置ID、電子郵件地址和電話號碼。 裝置或Cookie名稱空間是裝置和網頁瀏覽器的識別碼，優先順序不能高於人員名稱空間。 您也不能將裝置或Cookie名稱空間指定為唯一的名稱空間。

### 指定您的唯一名稱空間

若要指定唯一的名稱空間，請選取 [!UICONTROL 每個圖表不重複] 與該名稱空間對應的核取方塊。 您可以為您的身分設定組態選取多個唯一的名稱空間。

![已選取兩個不重複的名稱空間。](../images/rules/unique-namespaces.png)

建立唯一名稱空間後，圖表將無法再擁有多個包含唯一名稱空間的身分。 例如，如果您指定Analytics自訂ID作為唯一的名稱空間，則圖表只能有一個具有Analytics自訂ID名稱空間的身分。 如需詳細資訊，請閱讀 [身分最佳化演演算法概述](./identity-optimization-algorithm.md#unique-namespace).

### 設定名稱空間優先順序

若要設定名稱空間優先順序，請在身分設定功能表中選取名稱空間，然後將該名稱空間拖放至您喜歡的順序。 將名稱空間放在清單上較高的位置，給予它較高的優先順序，反之，將名稱空間放在清單上較低的位置，給予它較低的優先順序。 具有最高優先順序的名稱空間也應指定為唯一的名稱空間。

完成設定後，選取「 」 **[!UICONTROL 下一個]**. 確認訊息隨即出現，請利用此機會確認您的設定是否正確，然後選取 **[!UICONTROL 完成]**.

![驗證頁面。](../images/rules/validate.png)

系統會顯示警告，指出您的新設定不會對身分圖表中的現有連結，以及已內嵌的體驗事件設定檔片段有任何影響。 若要確認，請輸入您的沙箱名稱，然後選取 **[!UICONTROL 確認]**.

![確認視窗。](../images/rules/confirm.png)