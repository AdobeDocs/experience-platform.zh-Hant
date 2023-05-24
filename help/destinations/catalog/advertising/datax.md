---
title: Verizon MediaYahoo DataX連接
description: DataX是Verizon Media/Yahoo的聚合基礎架構，它承載著各種元件，使Verizon Media/Yahoo能夠以安全、自動和可擴展的方式與外部合作夥伴交換資料。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] 連接

## 總覽 {#overview}

[!DNL DataX] 是聚合 [!DNL Verizon Media/Yahoo] 承載各種元件的基礎架構 [!DNL Verizon Media/Yahoo] 以安全、自動化和可擴展的方式與外部合作夥伴交換資料。

>[!IMPORTANT]
>
>此文檔頁面由 [!DNL Verizon Media/Yahoo]`s [!DNL DataX] 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先決條件 {#prerequisites}

**MDM ID**

這是中的唯一標識符 [!DNL Yahoo DataX] 並且它是用於設定資料導出到此目標的必填欄位。 如果您不知道此ID，請與 [!DNL Yahoo DataX] 客戶經理。

**分類元資料**

分類資源在基上定義擴展 [!DNL DataX] 元資料結構

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

閱讀有關 [分類元資料](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 的 [!DNL DataX] 開發人員文檔。

## 費率限制和護欄 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>當激活100多個段時 [!DNL Verizon Media/Yahoo DataX]，您可能會從目標接收速率限制錯誤。 激活此目標的段時，嘗試在一個激活資料流中激活少於100個段。 如果需要激活更多段，請在同一帳戶上建立新目標。

[!DNL DataX] 是按分類和訪問群體帖子的配額限制進行的速率限制 [DataX文檔](https://developer.verizonmedia.com/datax/guide/rate-limits/)。


| 錯誤代碼 | 錯誤消息 | 說明 |
|---------|----------|---------|
| 429請求過多 | 超過每小時的速率限制 **(限制：100)** | 每個提供程式一小時內允許的請求數。 |

{style="table-layout:auto"}

## 支援的身份 {#supported-identities}

[!DNL Verizon Media] 支援激活下表中描述的身份。 瞭解有關 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇IDFA目標標識。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含Verizon媒體目標中使用的標識符（電子郵件、GAID、IDFA）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

[!DNL DataX] API可用於要針對特定受眾群的廣告商，這些特定受眾群在 [!DNL Verizon Media] (VMG)可以使用VMG的近即時API快速建立新段並推送所需的觀眾群。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

![平台UI中的Yahoo DataX目標卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL MDM ID]**:這是中的唯一標識符 [!DNL Yahoo DataX] 並且它是用於設定資料導出到此目標的必填欄位。 如果您不知道此ID，請與 [!DNL Yahoo DataX] 客戶經理。  使用MDM ID時，資料可以被限制為僅用於特定的一組獨佔用戶（例如廣告商的第一方資料）。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段到目標](../../ui/activate-segment-streaming-destinations.md) 有關激活目標受眾段的說明。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

有關詳細資訊，請閱讀 [!DNL Yahoo/Verizon Media] [文檔 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/)。
