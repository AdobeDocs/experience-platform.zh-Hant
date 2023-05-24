---
keywords: 飛艇屬性；飛艇目的地
title: 飛艇屬性連接
description: 將Adobe受眾資料無縫地傳遞到飛艇中，作為飛艇內目標的受眾屬性。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# [!DNL Airship Attributes] 連接 {#airship-attributes-destination}

## 總覽 {#overview}

[!DNL Airship] 是領先的客戶接洽平台，幫助您在客戶生命週期的每個階段向用戶提供有意義、個性化的渠道資訊。

此整合將Adobe配置檔案資料傳遞到 [!DNL Airship] 如 [屬性](https://docs.airship.com/guides/audience/attributes/) 用於目標或觸發。

瞭解有關 [!DNL Airship]，請參見 [飛艇文檔](https://docs.airship.com)。

>[!TIP]
>
>此文檔頁面由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： [support.fapher.com](https://support.airship.com/)。

## 先決條件 {#prerequisites}

在將受眾段發送到 [!DNL Airship]，您必須：

* 在 [!DNL Airship] 項目。
* 生成用於驗證的承載令牌。

>[!TIP]
>
>建立 [!DNL Airship] 帳戶 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 你還沒有。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：根據您的欄位映射，發送電子郵件地址、電話號碼、姓氏)和/或身份。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 啟用屬性 {#enable-attributes}

Adobe Experience Platform配置檔案屬性類似 [!DNL Airship] 屬性，並且可以使用本頁下面進一步演示的映射工具在平台中輕鬆地相互映射。

[!DNL Airship] 項目具有多個預定義和預設屬性。 如果您有自定義屬性，則必須在 [!DNL Airship] 。 請參閱 [設定和管理屬性](https://docs.airship.com/tutorials/audience/attributes/) 的雙曲餘切值。

## 生成持有者令牌 {#bearer-token}

轉到 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 的 [飛艇儀表板](https://go.airship.com) 選擇 **[!UICONTROL 令牌]** 的上界。

按一下 **[!UICONTROL 建立令牌]**。

提供令牌的用戶友好名稱，例如「Adobe屬性目標」，並選擇「所有訪問」作為角色。

按一下 **[!UICONTROL 建立令牌]** 並將細節保密。

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!DNL Airship Attributes] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1

利用在Adobe Experience Platform收集的配置檔案資料，將消息和豐富內容個性化到任何 [!DNL Airship]s頻道。 例如，利用 [!DNL Experience Platform] 配置檔案資料以在 [!DNL Airship]。 這將使酒店品牌能夠為每個用戶顯示最近的酒店位置的影像。

### 用例#2

利用Adobe Experience Platform的屬性進一步豐富 [!DNL Airship] 配置檔案並與SDK或 [!DNL Airship] 預測資料。 例如，零售商可以建立具有會員狀態和地點資料（來自平台的屬性）的段， [!DNL Airship] 預計會篡改資料，向身居內華達州拉斯維加斯的黃金忠誠度用戶發送高度有針對性的資訊，這些用戶很可能會被篡改。

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

[!DNL Airship] 可以在表示設備實例(例如，iPhone)的通道上設定屬性，或者在將用戶的所有設備映射到公共標識符（例如客戶ID）上的命名用戶上設定屬性。 如果在架構中將純文字檔案（未散列）電子郵件地址作為主標識，請選擇您的 **[!UICONTROL 源屬性]** 並映射到 [!DNL Airship] 右列中的命名用戶 **[!UICONTROL 目標標識]**，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應映射到通道（即設備）的標識符，基於源映射到相應的通道。 下圖顯示了如何建立兩個映射：

* IDFAiOS廣告ID [!DNL Airship] iOS
* Adobe `fullName` 屬性 [!DNL Airship] &quot;全名&quot;屬性

>[!NOTE]
>
>使用中顯示的用戶友好名稱 [!DNL Airship] 為屬性映射選擇目標欄位時使用儀表板。

**映射標識**

選擇源欄位：

![連接到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選擇目標欄位：

![連接到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**映射屬性**

選擇源屬性：

![選擇源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選擇目標屬性：

![選擇目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證映射：

![通道映射](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](../../../data-governance/home.md)。
