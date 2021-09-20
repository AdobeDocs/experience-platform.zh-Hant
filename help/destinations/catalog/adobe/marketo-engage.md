---
title: Marketo Engage目標
description: Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1f18e07af7ef0d90f882fa668c5659330bce5960
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# （測試版）Marketo Engage目的地 {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform中的Marketo Engage目的地目前為測試版。 檔案和功能可能會有所變更。

## 總覽 {#overview}

Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。

區段連接器可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，這些區段會顯示為靜態清單。

## 支援的身分 {#supported-identities}

| Target身分 | 說明 |
|---|---|
| ECID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 如需詳細資訊，請參閱以下關於[ECID](/help/identity-service/ecid.md)的檔案。 |
| 電子郵件 | 代表電子郵件地址的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

## 匯出類型 {#export-type}

區段匯出 — 您會匯出區段（對象）的所有成員，並匯出Marketo Engage目的地所使用的識別碼（名稱、電話號碼或其他）。

## 設定目的地和啟用區段 {#set-up}

如需如何設定目的地和啟用區段的詳細指示，請參閱Marketo檔案中的[將Adobe Experience Platform區段推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)。

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->