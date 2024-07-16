---
title: Pendo Source概觀
description: 瞭解如何使用API或使用者介面利用Webhook將Pendo連線至Adobe Experience Platform
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>[!DNL Pendo]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商分析應用程式擷取資料。 對分析提供者的支援包括[!DNL Pendo]。

[[!DNL Pendo]](https://pendo.io/)是產品分析應用程式，建置目的是協助軟體公司開發能夠引起客戶共鳴的產品。 此應用程式可讓軟體製造商將產品與各種工具內嵌，讓使用者獲得更好的產品體驗，產品團隊獲得新的見解。

[!DNL Pendo]來源可讓您使用[[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks)，從[!DNL Pendo.io]擷取支援的Webhook事件結構描述及其相關的事件資料。 [!DNL Pendo]來源可搭配[!DNL Pendo] URL Webhook使用。

支援的Webhook包括：

* 已顯示[指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide)
* [已顯示/已提交](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-)輪詢
* 已顯示/已提交[網路推廣者分數](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey)

## 先決條件 {#prerequisites}

在建立[!DNL Pendo]來源連線之前，您必須先確定您有下列專案：

[!DNL Pendo]帳戶。 如果您還沒有帳戶，請參閱[[!DNL Pendo] 註冊](https://app.pendo.io/register)頁面來註冊並建立您的帳戶。

### 設定[!DNL Pendo] Webhook {#set-up-webhook}

成功建立資料流後，您必須設定webhook以通知Platform有關[!DNL Pendo]個事件的資訊。 [!DNL Pendo]個Webhook可以在特定事件發生時將即時通知推送至其他服務，並將此資訊傳送至您的[!DNL Pendo]來源。 如需詳細資訊，請閱讀[取得串流端點URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint)和[設定 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook)的教學課程。

## 正在將[!DNL Pendo]連線至平台 {#connect-to-platform}

以下檔案提供有關如何使用API或使用者介面建立[!DNL Pendo]串流聯結器以與[!DNL Platform]連線的資訊：

### 使用API連線[!DNL Pendo]至平台 {#connect-to-platform-using-api}

* [使用API建立來源連線，將 [!DNL Pendo] 資料帶入Platform。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 使用UI連線[!DNL Pendo]至平台 {#connect-to-platform-using-ui}

* [使用使用者介面建立來源連線，將 [!DNL Pendo] 資料帶入Platform](../../tutorials/ui/create/analytics/pendo-webhook.md)
