---
title: Google Cloud Platform事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Edge Network事件傳送至Google Cloud Platform。
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 事件轉送擴充功能

[[!DNL Google Cloud Platform]](https://cloud.google.com/) 是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及軟體即服務(SaaS)整合服務，用於客戶關係管理(CRM)和企業資源規劃(ERP)。

此 [!DNL Google Cloud Platform] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能運用範圍 [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) 將事件從Adobe Experience Platform Edge Network傳送至 [!DNL Google Cloud Platform] 以進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先決條件

若要使用此擴充功能，您必須具備一個 [!DNL Google Cloud Platform] 帳戶與現有 [!DNL Cloud Pub/Sub] 主題。 如果您沒有既存的主題，請參閱 [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) 有關建立和管理主題的檔案。

### 建立密碼和資料元素

首先，建立新的 `Google OAuth 2` [事件轉送密碼](../../../ui/event-forwarding/secrets.md)，用來驗證您帳戶的連線，同時確保值的安全。

下一個， [建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 **[!UICONTROL 核心]** 擴充功能和 **[!UICONTROL 密碼]** 資料元素型別以參照 `Google OAuth 2` 您剛才建立的密碼。

## 安裝並設定 [!DNL Google Cloud Platform] 副檔名 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇現有的屬性來編輯。

選取 **[!UICONTROL 擴充功能]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在的卡片上 [!DNL Google Cloud Platform] 副檔名。

![目錄 [!DNL Google Cloud Platform] 擴充功能醒目提示安裝。](../../../images/extensions/server/google-cloud-platform/install-extension.png)

在設定畫面上，將您先前建立的資料元素密碼輸入至 **[!UICONTROL 存取權杖]** 欄位。 資料元素密碼將包含 [!DNL Google Cloud Platform] OAuth 2 Token。 選取 **[!UICONTROL 儲存]** 完成後。

![此 [!DNL Google Cloud Platform] 擴充功能組態頁面。](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## 建立 [!DNL Send Data to Cloud Pub/Sub] 規則 {#tracking-rule}

安裝擴充功能後，請建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，選取 **[!UICONTROL Google Cloud平台]** 擴充功能，然後選取「 」 **[!UICONTROL 傳送資料至雲端Pub/Sub]** （適用於動作型別）。

![的動作設定檢視 [!UICONTROL Google Cloud平台]，並醒目提示動作 [!UICONTROL 傳送資料至雲端Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 主題] | 將從事件轉送接收事件的主題。 值必須採用格式 `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL 資料] | 此欄位包含要轉送至 [!DNL Cloud Pub/Sub] JSON格式的主題。<br><br>在 **[!UICONTROL 原始]** 選項，您可以將JSON物件直接貼到提供的文字欄位中，或選取資料元素圖示(![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png))從現有資料元素清單中選取以代表資料。<br><br>您也可以使用 **[!UICONTROL JSON索引鍵值配對編輯器]** 用於透過UI編輯器手動新增每個索引鍵/值組的選項。 每個值都可表示為原始輸入，或是可改為選取資料元素。 |
| [!UICONTROL 屬性] | 此欄位包含JSON物件，以及要連同訊息一起傳送的額外屬性。<br><br>在 **[!UICONTROL 原始]** 選項，您可以將JSON物件直接貼到提供的文字欄位中，或選取資料元素圖示(![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png))從現有資料元素清單中選取以代表資料。<br><br>您也可以使用 **[!UICONTROL JSON索引鍵值配對編輯器]** 用於透過UI編輯器手動新增每個索引鍵/值組的選項。 每個值都可表示為原始輸入，或是可改為選取資料元素。 |

{style="table-layout:auto"}

## 後續步驟

本指南說明如何將資料傳送至 [!DNL Cloud Pub/Sub] 使用 [!DNL Google Cloud Platform] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).