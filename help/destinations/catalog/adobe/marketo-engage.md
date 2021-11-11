---
title: Marketo Engage目標
description: Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 3e2382cf4b02ea4fd40e3638b52b4719938a2ea2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Marketo Engage目標 {#beta-marketo-engage-destination}

## 總覽 {#overview}

Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。

目的地可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，這些區段會顯示為靜態清單。

## 支援的身分 {#supported-identities}

| Target身分 | 說明 |
|---|---|
| ECID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱下列檔案，內容如下 [ECID](/help/identity-service/ecid.md) 以取得更多資訊。 |
| 電子郵件 | 代表電子郵件地址的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

## 匯出類型 {#export-type}

區段匯出 — 您會匯出區段（對象）的所有成員，並在Marketo Engage目的地中使用識別碼（電子郵件、ECID）。

## 設定目的地和啟用區段 {#set-up}

如需如何設定目的地和啟用區段的詳細指示，請參閱 [推送Adobe Experience Platform區段至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) 在Marketo檔案中。

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->