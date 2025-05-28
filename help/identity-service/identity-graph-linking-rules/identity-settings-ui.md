---
title: 身分設定UI
description: 瞭解如何使用身分設定使用者介面。
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 38d331bd9265f25a3aebdcbd20ae5fc30a93e960
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 2%

---

# 身分設定UI

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules]現已正式可用。 如果您有現有的沙箱，在啟用身分設定後，需要取消收合的圖形（「已修正」），請聯絡您的Adobe帳戶團隊或Adobe支援。

身分設定是Adobe Experience Platform Identity Service UI中的功能，可用來指定唯一的名稱空間及設定名稱空間優先順序。

請觀看下列影片，瞭解在Identity Service UI工作區中使用[!DNL Graph Simulation]介面的其他資訊：

>[!VIDEO](https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops)

請閱讀本指南，瞭解如何在UI中設定身分設定。

## 先決條件

開始使用身分設定前，請先閱讀下列檔案：

* [[!DNL Identity Graph Linking Rules]](./overview.md)
* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [實作指南](./implementation-guide.md)
* [圖表設定範例](./example-configurations.md)
* [命名空間優先順序](./namespace-priority.md)
* [圖表模擬](./graph-simulation.md)

### 設定許可權 {#set-permissions}

接下來，您必須確保您的帳戶已布建下列許可權：

* **[!UICONTROL 檢視身分設定]**：套用此許可權，以便在身分名稱空間瀏覽頁面中檢視唯一的名稱空間和名稱空間優先順序。
* **[!UICONTROL 編輯身分設定]**：套用此許可權，以便能夠編輯並儲存您的身分設定。

如果您沒有這些許可權，請聯絡管理員。 如需詳細資訊，請閱讀[許可權指南](../../access-control/abac/ui/permissions.md)。

## 設定您的身分設定

若要存取身分設定，請瀏覽至Adobe Experience Platform UI中的身分服務工作區，然後選取&#x200B;**[!UICONTROL 設定]**。

![已選取[設定]按鈕的身分儀表板介面。](../images/rules/dashboard.png)

身分設定頁面分為兩個區段： [!UICONTROL 個人名稱空間]和[!UICONTROL 裝置或Cookie名稱空間]。 個人名稱空間是適用於單一個人的識別碼。 可以是跨裝置ID、電子郵件地址和電話號碼。 裝置或Cookie名稱空間是裝置和網頁瀏覽器的識別碼，優先順序不能高於人員名稱空間。 您也不能將裝置或Cookie名稱空間指定為唯一的名稱空間。

### 設定名稱空間優先順序

若要設定名稱空間優先順序，請在身分設定功能表中選取名稱空間，然後將該名稱空間拖放至您喜歡的順序。 將名稱空間放在清單上較高位置，給予它較高的優先順序，反之，將名稱空間放在清單上較低位置，給予它較低的優先順序。 具有最高優先順序的名稱空間也應指定為唯一的名稱空間。

![識別設定工作區中反白了人員名稱空間。](../images/rules/namespace-priority.png)

### 指定您的唯一名稱空間

若要指定唯一的名稱空間，請選取與該名稱空間相對應的[!UICONTROL 每個圖表唯一的]核取方塊。 您最多可以為身分設定組態選取&#x200B;**三個唯一的名稱空間**。

建立唯一名稱空間後，圖表將無法再擁有多個包含唯一名稱空間的身分。 例如，如果您指定CRMID作為唯一的名稱空間，則圖表只能有一個身分與CRMID名稱空間。 如需詳細資訊，請閱讀[身分最佳化演演算法總覽](./identity-optimization-algorithm.md#unique-namespace)。

完成設定後，請選取[下一步] **[!UICONTROL 以繼續。]**

![選取並定義為唯一的兩個名稱空間。](../images/rules/unique-namespace.png)

在繼續進行最後一個步驟之前，您必須從這裡確認下列事項：

1. 選取的唯一名稱空間。
2. 每個已知設定檔中存在具有最高優先順序唯一名稱空間的身分。
3. 名稱空間優先順序的順序。

![已選取「確認」按鈕的確認視窗。](../images/rules/confirmation.png)

### 確認您的設定 {#confirm-your-settings}

>[!IMPORTANT]
>
>* 最後一個步驟是另一個確認訊息，指出只有在儲存您的設定&#x200B;**後更新圖形時，現有圖形才會受到圖形演演算法**&#x200B;的影響，而且即使名稱空間優先順序變更後，即時客戶設定檔上的事件片段主要身分也不會更新。
>
>* 您的新設定或更新設定最多需要&#x200B;**24小時**&#x200B;才能生效。 若要確認，請輸入您的沙箱名稱，然後選取&#x200B;**[!UICONTROL 確認]**。
>
>* 在您儲存身分設定之前，您的資料不會有任何變更。

![確認視窗會顯示有關處理設定前延遲6小時的警告。](../images/rules/complete.png)

## 後續步驟

如需[!DNL Identity Graph Linking Rules]的詳細資訊，請閱讀下列檔案：

* [[!DNL Identity Graph Linking Rules] 概觀](./overview.md)
* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [實作指南](./implementation-guide.md)
* [圖表設定範例](./example-configurations.md)
* [疑難排解和常見問答( FAQ)](./troubleshooting.md)
* [命名空間優先順序](./namespace-priority.md)
* [圖表模擬UI](./graph-simulation.md)