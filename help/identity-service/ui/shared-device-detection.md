---
keywords: Experience Platform；首頁；熱門主題；身份服務；共用設備；共用設備
title: 共用設備概述(Beta)
description: 共用設備檢測識別同一設備的不同經過驗證的用戶，允許在身份圖中更準確地表示客戶資料
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 共用設備檢測概述(Beta)

>[!IMPORTANT]
>
>的 [!DNL Shared Device Detection] 功能為beta。 其功能和文檔可能會更改。

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

[!DNL Shared Device] 指由多個個人使用的設備。 共用設備的示例包括平板電腦、庫電腦和亭子。 通過 [!DNL Shared Device Detection] 可以防止同一設備的不同用戶被合併到單個標識中，從而允許更準確地表示個人。

與 [!DNL Shared Device Detection] 您可以：

* 為同一設備的不同用戶建立單獨的標識圖；
* 防止使用同一設備的不同個體的資料混合；
* 生成更清潔、更準確的客戶視圖。

>[!TIP]
>
>配置 [!DNL Shared Device Detection] 必須在為資料集啟用配置檔案之前完成，因為一旦生成圖形，您就無法再修改設定 [!DNL Identity Service]。

## 入門 [!DNL Shared Device Detection]

使用 [!DNL Shared Device Detection] 需要瞭解所涉及的各種平台服務。 開始使用之前 [!DNL Shared Device Detection]，請查看以下服務的文檔：

* [[!DNL Identity Service]](../home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
   * [標識圖形查看器](./identity-graph-viewer.md):直觀顯示並與身份圖查看器交互，以便更好地瞭解客戶身份是如何拼合在一起的，以及以何種方式縫合的。
   * [標識命名空間](../namespaces.md):請參閱完全限定身份的元件，以及標識命名空間如何允許您區分身份的上下文和類型。

## 瞭解 [!DNL Shared Device Detection]

使用以下術語時瞭解這些術語非常重要
[!DNL Shared Device Detection]。 請參見下表，瞭解對瞭解 [!DNL Shared Device Detection]。

### 術語

| 詞彙 | 定義 |
| --- | --- |
| 共用設備 | 共用設備是由多個個人使用的任何設備。 共用設備的示例包括平板電腦、庫電腦和亭子。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 指允許同一設備的不同用戶的資料彼此分離的配置設定。 |
| 共用標識命名空間 | 共用標識命名空間表示可供多個用戶使用的設備。 共用標識命名空間通常是ECID，但可以設定為其他設備ID。 |
| 用戶標識命名空間 | 用戶標識命名空間表示共用設備的已驗證（已登錄）用戶。 |
| 上次驗證的用戶 | 如果設備正由多個帳戶登錄，則最後一個經過身份驗證的用戶代表上次登錄到設備的用戶。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection] 通過建立兩個命名空間來工作。這樣 **共用標識命名空間** 和 **用戶標識命名空間**。

* 共用標識命名空間表示可供多個用戶使用的設備。 Adobe建議客戶使用ECID作為共用設備標識符。
* 用戶標識名稱空間映射到與用戶登錄ID對應的標識名稱空間，這可以是用戶的CRM ID、電子郵件地址、散列電子郵件或電話號碼。

共用設備與平板電腦一樣，具有 **共用標識命名空間**。 另一方面，共用設備的每個用戶都有自己的指定 **用戶標識命名空間** 與各自的登錄ID對應。 例如，Kevin和Nora共用用於電子商務的平板電腦具有自己的ECID `1234`，而Kevin有自己的用戶標識名稱空間映射到其 `kevin@email.com` 帳戶和諾拉的用戶標識名稱空間映射到她 `nora@email.com` 帳戶。

[!DNL Shared Device Detection] 能夠通過連結共用標識名稱空間(例如， ECID)，具有上一個已驗證用戶的用戶標識命名空間（登錄ID）。

### 如何將身份資料發送到身份圖

請考慮以下示例來幫助您瞭解 [!DNL Shared Device Detection] 工作：

>[!NOTE]
>
>在此圖中，將共用標識命名空間配置為ECID，將用戶標識命名空間配置為CRM ID。

![圖](../images/shared-device/diagram.png)

* 凱文和諾拉共用一個平板電腦訪問一個電子商務網站。 不過，他們都有自己的獨立賬戶，每個賬戶都用來瀏覽和網上購物；
   * 作為共用設備，平板電腦具有相應的ECID，表示平板電腦的Web瀏覽器Cookie ID;
* 假設凱文用平板電腦 **登錄** 到他的電子商務帳戶瀏覽耳機，這表示Kevin的CRM ID(**用戶標識命名空間**)現在與平板電腦的ECID(**共用標識命名空間**)。 平板電腦的瀏覽資料現在與凱文的身份圖相結合。
   * 如果凱文 **註銷** 諾拉用平板電腦 **登錄** 她自己賬戶里買了一台相機，然後她的CRM ID就與平板電腦的ECID相連。 因此，平板電腦的瀏覽資料現在與諾拉的身份圖相結合。
   * 如果諾拉 **不註銷** 凱文用了平板電腦，但 **未登錄**&#x200B;然後，平板電腦的瀏覽資料仍與Nora結合，因為她仍然是經過驗證的用戶，並且她的CRM ID仍與平板電腦的ECID連結。
   * 如果諾拉 **註銷** 凱文用了平板電腦，但 **未登錄**，則平板電腦的瀏覽資料仍與諾拉的身份圖相結合，因為 **上一個經過驗證的用戶**&#x200B;她的CRM ID仍與平板電腦的ECID關聯。
   * 如果凱文 **登錄** 同樣，他的CRM ID現在被連結到平板電腦的ECID，因為他現在是最後一個經過驗證的用戶，平板電腦的瀏覽資料現在與他的身份圖結合在一起。

### 如何 [!DNL Profile Service] 合併配置檔案片段 [!DNL Shared Device Detection] 啟用

[!DNL Profile Service] 記錄配置檔案片段和合併的配置檔案。 每個單獨的客戶配置檔案由多個配置檔案片段組成，這些片段已合併以形成該客戶的單個視圖。 例如，如果客戶通過多個渠道與您的品牌進行交互，您的組織將具有多個與該單個客戶相關的配置檔案片段，這些配置檔案片段出現在多個資料集中。 當這些片段被放入平台中時，它們會合併在一起，以便為該客戶建立單個配置檔案。

當 [!DNL Shared Device Detection] 啟用， [!DNL Profile] 基於體驗事件是經過驗證還是未經驗證來定義配置檔案片段的主標識

安 **經過驗證的體驗事件** 是用戶在登錄到設備時完成的操作。 對於經過身份驗證的體驗事件，主標識為 **用戶標識命名空間** （登錄ID）。 安 **未經驗證的體驗事件** 是未登錄到設備的用戶完成的操作。 對於未經身份驗證的體驗事件，主標識為 **共用標識命名空間** (ECID)。

有關詳細資訊，請參見  [[!DNL Real-Time Customer Profile] 概述](../../profile/home.md)。

## 共用設備UI

在平台UI中，選擇 **[!UICONTROL 身份]** 從左導航，然後選擇 **[!UICONTROL 標識設定]**。

![身份儀表板](../images/shared-device/identity-dashboard.png)

的 [!UICONTROL 共用設備設定] 的子菜單。 預設情況下禁用共用設備設定。

啟用後，共用設備設定允許來自同一設備的不同用戶的資料彼此分離。 此配置設定允許更清潔和更準確地表示身份圖，其中不將同一設備的用戶身份組合在一起。

選擇 **[!UICONTROL 啟用]** 開始修改共用設備設定。

![啟用共用設備](../images/shared-device/enable-shared-device.png)

的 [!UICONTROL 共用標識命名空間] 和 [!UICONTROL 用戶標識命名空間] 將顯示配置選項，允許您修改要使用的標識命名空間。

![set命名空間](../images/shared-device/set-namespaces.png)

[!UICONTROL 共用標識命名空間] 表示由多個不同用戶使用的單個設備。 此命名空間始終設定為 **[!UICONTROL ECID]** 因為所有平台用戶都使用 **[!UICONTROL ECID]** 作為Web瀏覽器標識符。

![共用標識命名空間](../images/shared-device/shared-identity-namespace.png)

的 [!UICONTROL 用戶標識命名空間] 允許您識別同一設備的不同用戶，並防止資料合併到同一身份圖中。

![用戶標識命名空間](../images/shared-device/user-identity-namespace.png)

選擇 **[!UICONTROL 用戶標識命名空間]** 搜索欄，然後輸入標識命名空間或從下拉菜單中選擇標識命名空間。

>[!TIP]
>
>的 [!UICONTROL 用戶標識命名空間] 應映射到與最終用戶的登錄ID對應的標識名稱空間。 選項包括客戶ID、電子郵件和散列電子郵件。

![電子郵件](../images/shared-device/emails.png)

配置完 [!UICONTROL 共用設備設定]選中 **[!UICONTROL 保存]**。

![保存](../images/shared-device/save.png)

出現彈出窗口，提示您確認選擇。 選擇 **[!UICONTROL 是]** 完成配置設定。

![confirm](../images/shared-device/confirm.png)
