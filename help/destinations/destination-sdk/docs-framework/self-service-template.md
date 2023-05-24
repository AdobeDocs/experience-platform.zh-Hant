---
title: 文檔自助模板//替換為目標名稱
description: 使用此模板可在Adobe Experience Platform目錄中為目標建立公共文檔。//替換為「概述」部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 1773edff56059cf5bc57ebaaa133216423fcfe10
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# 您的目標連接 {#your-destination}

*在完成此模板時，替換或刪除斜體中的所有段落（從此段開始）。*

*首先更新頁面頂部的元資料（標題和說明）。 請忽略此頁上UICONTROL的所有實例。 這是一個標籤，它幫助我們的機器翻譯流程將頁面正確翻譯成我們支援的多種語言。 在您提交文檔後，我們將向其添加標籤。*

>[!IMPORTANT]
>
>* 按模板中概述的順序填充此模板中的所有部分。
>* 根據合作夥伴反饋，此模板不經常更新。 在開始為目標創作文檔之前，請確保已下載 [模板的最新版本](../assets/docs-framework/yourdestination-template.zip)。


## 總覽 {#overview}

*提供您公司的簡短概述，包括它為客戶提供的價值。 包括指向產品文檔首頁的連結，以供進一步閱讀。*

>[!IMPORTANT]
>
>此文檔頁面由 *目標* 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： *插入連結或電子郵件地址，以便可以訪問您進行更新，例如 `support@YourDestination.com`。*

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 *目標* 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1 {#use-case-1}

*對於移動消息平台：*

*一個房屋租賃和銷售平台希望將移動通知推送給客戶的Android和iOS設備，讓他們知道，在他們之前搜索的租房區域，有100個更新的房源。*

### 用例#2 {#use-case-2}

*對於社交網路平台：*

*一個運動服裝品牌希望通過社交媒體賬戶接觸現有客戶。 服裝品牌可以將電子郵件地址從自己的CRM接收到Adobe Experience Platform，從自己的離線資料構建段，並將這些段發送到YourDestination，以在客戶的社交媒體源中顯示廣告。*

## 先決條件 {#prerequisites}

*在本節中添加有關客戶在開始在Adobe Experience Platform用戶介面中設定目標之前需要瞭解的任何資訊。 這可以是：*

* *需要添加到允許清單*
* *電子郵件散列要求*
* *任何有關您的帳戶的詳細資訊*
* *如何獲取API密鑰以連接到您的平台*

*如果對客戶有用，您可以連結到相關文檔。*

## 支援的身份 {#supported-identities}

*在本節中添加有關目標支援的標識的資訊。 我們用一些標準值預填了表。 刪除不適用於目標的值和未預填充的任何值。*

*目標* 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇IDFA目標標識。 |
| ECID | Experience Cloud ID | 表示ECID的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 閱讀以下文檔 [ECID](/help/identity-service/ecid.md) 的子菜單。 |
| phone_sha256 | 使用SHA256算法散列的電話號碼 | 純文字檔案和SHA256散列電話號碼都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| 外部ID | 自定義用戶ID | 如果源標識是自定義命名空間，請選擇此目標標識。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

*在表中，僅保留與目標對應的行。 您應該有一行表示「導出」類型，一行表示「導出」頻率。 刪除不適用於目標的值。*

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） *目標* 目標。 |
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出類型 | **[!UICONTROL 資料集導出]** | 您正在導出未按受眾興趣或資格進行分組或結構化的原始資料集。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

*添加客戶在向目標進行身份驗證時必須填寫的欄位。 這些欄位是特定於目標的，取決於您在Destination SDK中的配置。 目標的欄位可能與下面列出的欄位不同。 還請包括與下面顯示的示例螢幕快照類似的螢幕快照。*

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

![示例螢幕截圖，顯示如何驗證到目標](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL 持有者令牌]**:填寫承載令牌以驗證到目標。

### 填寫目標詳細資訊 {#destination-details}

*添加配置新目標時客戶必須填寫的欄位。 這些欄位是特定於目標的，取決於您在Destination SDK中的配置。 目標的欄位可能與下面列出的欄位不同。 還請包括與下面顯示的示例螢幕快照類似的螢幕快照。*

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![示例螢幕截圖，顯示如何填寫目標的詳細資訊](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 *目標* 帳戶ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請閱讀上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

*酌情刪除 — 如果正在記錄新的流式傳輸目標，請保留下面的第一段。 如果您正在記錄新的基於檔案的目標，請保留第二段。 如果您正在記錄導出資料集的目標，請保留第三段。*

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

閱讀 [將受眾資料激活到批配置檔案導出目標](/help/destinations/ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

閱讀 [(Beta)導出資料集](/help/destinations/ui/export-datasets.md) 有關將資料集導出到此目標的詳細說明。

### 映射屬性和標識 {#map}

*在激活工作流的「映射」步驟中，添加有關源欄位和目標欄位之間支援的映射的資訊。 目標可能支援導出配置檔案屬性、標識命名空間或兩者。 某些欄位可能是必需的。 目標屬性可能是預定義的或自定義的。 指出重要注意事項，並使用示例，最好帶螢幕截圖。 可以用作參考的目標頁的兩個示例是：*

* *[佩加](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅達利亞](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 導出的資料/驗證資料導出 {#exported-data}

*添加有關如何將資料導出到目標的段落。 這將幫助客戶確保他們已正確整合到您的目標。 例如，您可以提供類似於下面的JSON示例。 或者，您可以從目標的介面提供螢幕截圖和資訊，以顯示客戶應如何期望在目標平台中填充段。*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

*您可以提供指向產品文檔或您認為對客戶成功非常重要的任何其他資源的進一步連結。*