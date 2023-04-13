---
title: Pendo源概述
description: 了解如何使用API或使用者介面，透過Webhook將Pendo連線至Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>此 [!DNL Pendo] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商分析應用程式擷取資料。 支援分析提供者包括 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 是產品分析應用程式，專為協助軟體公司開發能與客戶產生共鳴的產品而打造。 此應用程式可讓軟體製造商運用多種工具嵌入產品，為使用者提供更佳的產品體驗，並為產品團隊提供全新見解。

此 [!DNL Pendo] 來源可讓您從擷取支援的網頁連結事件結構及其相關事件資料 [!DNL Pendo.io] 使用 [[!DNL Pendo] Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 此 [!DNL Pendo] 源使用 [!DNL Pendo] URL Webhook。

支援的Webhook包括：

* [指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 顯示
* [輪詢](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 顯示/已提交
* [淨啟動子分數](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 顯示/已提交

## 先決條件 {#prerequisites}

建立 [!DNL Pendo] 源連接時，必須首先確保您具有以下內容：

A [!DNL Pendo] 帳戶。 如果您還沒有看到 [[!DNL Pendo] 註冊](https://app.pendo.io/register) 頁面來註冊和建立您的帳戶。

### 設定 [!DNL Pendo] Webhook {#set-up-webhook}

成功建立資料流後，必須設定Webhook以通知Platform [!DNL Pendo] 事件。 [!DNL Pendo] Webhook可在發生特定事件時推送即時通知至其他服務，並將此資訊傳送至您的 [!DNL Pendo] 來源。 如需詳細資訊，請參閱 [取得串流端點URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 連接 [!DNL Pendo] 到平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Pendo] 串流連接器與 [!DNL Platform] 使用API或使用者介面：

### Connect [!DNL Pendo] 使用API到平台 {#connect-to-platform-using-api}

* [建立源連接以 [!DNL Pendo] 使用API將資料傳送至Platform。](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connect [!DNL Pendo] 使用UI設為Platform {#connect-to-platform-using-ui}

* [建立源連接以 [!DNL Pendo] 使用者介面將資料傳送至Platform](../../tutorials/ui/create/analytics/pendo-webhook.md)
