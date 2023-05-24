---
keywords: 飛艇標籤；飛艇目的地
title: 飛艇標籤連接
description: 將Adobe受眾資料無縫傳遞到飛艇上，作為飛艇內目標的受眾標籤。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# [!DNL Airship Tags] 連接 {#airship-tags-destination}

## 總覽

[!DNL Airship] 是領先的客戶接洽平台，幫助您在客戶生命週期的每個階段向用戶提供有意義、個性化的渠道資訊。

此整合將Adobe Experience Platform段資料 [!DNL Airship] 如 [標籤](https://docs.airship.com/guides/audience/tags/) 用於目標或觸發。

瞭解有關 [!DNL Airship]，請參見 [飛艇文檔](https://docs.airship.com)。


>[!TIP]
>
>此文檔頁面由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： [support.fapher.com](https://support.airship.com/)。

## 先決條件

在將您的Adobe Experience Platform段發送到 [!DNL Airship]，您必須：

* 在中建立標籤組 [!DNL Airship] 項目。
* 生成用於驗證的承載令牌。

>[!TIP]
> 
>建立 [!DNL Airship] 帳戶 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 你還沒有。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含「飛艇標籤」目標中使用的標識符。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 標籤組

Adobe Experience Platorm中段的概念與 [標籤](https://docs.airship.com/guides/audience/tags/) 在飛艇上，在實施上稍有差異。 此整合映射用戶的狀態 [Experience Platform段成員](../../../xdm/field-groups/profile/segmentation.md) 是否存在 [!DNL Airship] 標籤。 例如，在平台段中， `xdm:status` 更改 `realized`，標籤將添加到 [!DNL Airship] 此配置檔案映射到的通道或已命名用戶。 如果 `xdm:status` 更改 `exited`，標籤將被刪除。

要啟用此整合，請建立 *標籤組* 在 [!DNL Airship] 命名 `adobe-segments`。

>[!IMPORTANT]
>
>建立新標籤組時 **不檢查** 單選按鈕上寫著&quot;[!DNL Allow these tags to be set only from your server]。 這樣做將導致Adobe標籤整合失敗。

請參閱 [管理標籤組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 中。

## 生成持有者令牌

轉到 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 的 [飛艇儀表板](https://go.airship.com) 選擇 **[!UICONTROL 令牌]** 的上界。

按一下 **[!UICONTROL 建立令牌]**。

提供令牌的用戶友好名稱，例如「Adobe標籤目標」，並選擇「所有訪問」作為角色。

按一下 **[!UICONTROL 建立令牌]** 並將細節保密。

## 使用案例

幫助您更好地瞭解您應如何以及何時使用 [!DNL Airship Tags] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1

零售商或娛樂平台可以在忠誠客戶上建立用戶配置檔案，並將這些分段傳遞到 [!DNL Airship] 用於移動活動中的消息目標。

### 用例#2

當用戶進入或離開Adobe Experience Platform內的特定網段時，即時觸發一對一消息。

例如，一家零售商在Platform公司設立了一個牛仔褲品牌專業部門。 現在，只要某人將牛仔褲偏好設定在某個特定品牌，該零售商就能觸發手機消息。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL 持有者令牌]**:從 [!DNL Airship] 控制項欄。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:輸入一個名稱，以幫助您標識此目標。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 域]**:選擇美國或歐盟資料中心，具體取決於 [!DNL Airship] 資料中心適用於此目標。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 映射注意事項 {#mapping-considerations}

[!DNL Airship] 可以在表示設備實例(例如，iPhone)的頻道上設定標籤，或在將用戶的所有設備映射到公共標識符（例如客戶ID）上的命名用戶。 如果在架構中將純文字檔案（未散列）電子郵件地址作為主標識，請選擇您的 **[!UICONTROL 源屬性]** 並映射到 [!DNL Airship] 右列中的命名用戶 **[!UICONTROL 目標標識]**，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應映射到通道（即設備）的標識符，基於源映射到相應的通道。 以下影像顯示如何將Google廣告ID映射到 [!DNL Airship] 安卓頻道。

![連接到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![連接到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![通道映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](../../../data-governance/home.md)。
