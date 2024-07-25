---
title: Google Cloud Platform事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Edge Network事件傳送至Google Cloud Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 事件轉送擴充功能

[[!DNL Google Cloud Platform]](https://cloud.google.com/)是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及客戶關係管理(CRM)和企業資源規劃(ERP)的軟體即服務(SaaS)整合服務。

[!DNL Google Cloud Platform] [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能運用[[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub)將事件從Adobe Experience PlatformEdge Network傳送至[!DNL Google Cloud Platform]以進行進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先決條件

若要使用此延伸模組，您必須擁有具有現有[!DNL Cloud Pub/Sub]主題的[!DNL Google Cloud Platform]帳戶。 如果您沒有既存的主題，請參閱有關建立和管理主題的[[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic)檔案。

### 建立密碼和資料元素

首先，建立新的`Google OAuth 2` [事件轉送密碼](../../../ui/event-forwarding/secrets.md)，它將會用來驗證您帳戶的連線，同時保證值的安全。

接著，[使用&#x200B;**[!UICONTROL Core]**&#x200B;擴充功能和&#x200B;**[!UICONTROL Secret]**&#x200B;資料元素型別，建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)以參考您剛才建立的`Google OAuth 2`密碼。

## 安裝並設定[!DNL Google Cloud Platform]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選擇現有的屬性來編輯。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取[!DNL Google Cloud Platform]擴充功能的卡片上的&#x200B;**[!UICONTROL 安裝]**。

![目錄[!DNL Google Cloud Platform]延伸模組醒目提示安裝。](../../../images/extensions/server/google-cloud-platform/install-extension.png)

在設定畫面上，將您先前建立的資料元素密碼輸入至&#x200B;**[!UICONTROL 存取Token]**&#x200B;欄位。 資料元素密碼將包含您的[!DNL Google Cloud Platform] OAuth 2權杖。 完成時選取&#x200B;**[!UICONTROL 儲存]**。

![擴充功能組態頁面[!DNL Google Cloud Platform]。](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## 建立[!DNL Send Data to Cloud Pub/Sub]規則 {#tracking-rule}

安裝擴充功能後，請建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)，並視需要設定其條件。 設定規則的動作時，請選取&#x200B;**[!UICONTROL Google Cloud Platform]**&#x200B;擴充功能，然後針對動作型別選取&#x200B;**[!UICONTROL 將資料傳送至Cloud Pub/Sub]**。

![ [!UICONTROL Google Cloud Platform]的動作設定檢視（反白顯示動作）和[!UICONTROL 將資料傳送到Cloud Pub/Sub]。](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 主題] | 將從事件轉送接收事件的主題。 值的格式必須為`projects/{projectName}/topics/{topicName}`。 |
| [!UICONTROL 資料] | 此欄位包含要以JSON格式轉送至[!DNL Cloud Pub/Sub]主題的資料。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;選項下，您可以將JSON物件直接貼上到提供的文字欄位中，或者您可以選取資料元素圖示（![資料集圖示](/help/images/icons/database.png)），從現有資料元素清單中選取以代表資料。<br><br>您也可以使用&#x200B;**[!UICONTROL JSON索引鍵/值組編輯器]**&#x200B;選項，透過UI編輯器手動新增每個索引鍵/值組。 每個值都可表示為原始輸入，或是可改為選取資料元素。 |
| [!UICONTROL 屬性] | 此欄位包含JSON物件，以及要連同訊息一起傳送的額外屬性。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;選項下，您可以將JSON物件直接貼上到提供的文字欄位中，或者您可以選取資料元素圖示（![資料集圖示](/help/images/icons/database.png)），從現有資料元素清單中選取以代表資料。<br><br>您也可以使用&#x200B;**[!UICONTROL JSON索引鍵/值組編輯器]**&#x200B;選項，透過UI編輯器手動新增每個索引鍵/值組。 每個值都可表示為原始輸入，或是可改為選取資料元素。 |

{style="table-layout:auto"}

## 後續步驟

本指南涵蓋如何使用[!DNL Google Cloud Platform]事件轉送擴充功能將資料傳送至[!DNL Cloud Pub/Sub]。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
