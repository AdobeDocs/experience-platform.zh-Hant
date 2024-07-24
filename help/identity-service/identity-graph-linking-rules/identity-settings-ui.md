---
title: 身分設定UI
description: 瞭解如何使用身分設定使用者介面。
badge: Beta
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 身分設定UI

>[!AVAILABILITY]
>
>身分圖表連結規則目前處於Beta版。 如需參與率條件的詳細資訊，請聯絡您的Adobe客戶團隊。 功能和檔案可能會有所變更。

身分設定是Adobe Experience Platform Identity Service UI中的功能，可用來指定唯一的名稱空間及設定名稱空間優先順序。

請閱讀本指南，瞭解如何在UI中設定身分設定。

## 先決條件

開始使用身分設定前，請先閱讀下列檔案：

* [身分圖表連結規則設定指南](./configuration.md)
* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [名稱空間優先順序](./namespace-priority.md)
* [圖表模擬](./graph-simulation.md)

## 設定您的身分設定

若要存取身分設定，請瀏覽至Adobe Experience Platform UI中的身分服務工作區，然後選取&#x200B;**[!UICONTROL 設定]**。

![已選取身分設定按鈕。](../images/rules/identities-ui.png)

身分設定頁面分為兩個區段： [!UICONTROL 個人名稱空間]和[!UICONTROL 裝置或Cookie名稱空間]。 個人名稱空間是適用於單一個人的識別碼。 可以是跨裝置ID、電子郵件地址和電話號碼。 裝置或Cookie名稱空間是裝置和網頁瀏覽器的識別碼，優先順序不能高於人員名稱空間。 您也不能將裝置或Cookie名稱空間指定為唯一的名稱空間。

### 設定名稱空間優先順序

若要設定名稱空間優先順序，請在身分設定功能表中選取名稱空間，然後將該名稱空間拖放至您喜歡的順序。 將名稱空間放在清單上較高位置，給予它較高的優先順序，反之，將名稱空間放在清單上較低位置，給予它較低的優先順序。 具有最高優先順序的名稱空間也應指定為唯一的名稱空間。

![識別設定工作區中反白了人員名稱空間。](../images/rules/namespace-priority.png)

### 指定您的唯一名稱空間

若要指定唯一的名稱空間，請選取與該名稱空間相對應的[!UICONTROL 每個圖表唯一的]核取方塊。 您可以為您的身分設定組態選取多個唯一的名稱空間。

![選取並定義為唯一的兩個名稱空間。](../images/rules/unique-namespace.png)

建立唯一名稱空間後，圖表將無法再擁有多個包含唯一名稱空間的身分。 例如，若您指定CRM ID作為唯一的名稱空間，則圖表只能有一個具有CRM ID名稱空間的身分。 如需詳細資訊，請閱讀[身分最佳化演演算法總覽](./identity-optimization-algorithm.md#unique-namespace)。

完成設定後，請選取&#x200B;**[!UICONTROL 下一步]**。 出現確認訊息，請利用此機會確認您的設定是否正確，然後選取&#x200B;**[!UICONTROL 完成]**。

![標示完成狀態的驗證頁面。](../images/rules/finish.png)

系統會顯示警告，指出您的新設定不會對身分圖表中的現有連結，以及已內嵌的體驗事件設定檔片段有任何影響。 此外，您會收到通知，新設定最多需要6小時才會反映在系統中。 若要確認輸入您的沙箱名稱，然後選取&#x200B;**[!UICONTROL 確認]**。

![確認視窗會顯示有關處理設定前延遲6小時的警告。](../images/rules/confirm-settings.png)

## 後續步驟

您現在已設定名稱空間優先順序，並使用身分設定UI頁面指定唯一的名稱空間。 如需詳細資訊，請閱讀[身分圖表連結規則總覽](./overview.md)。
