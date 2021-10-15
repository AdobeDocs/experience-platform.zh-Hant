---
description: 使用Adobe Experience Platform Destination SDK中支援的驗證設定，驗證使用者並啟用資料至您的目的地端點。
title: 驗證配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 驗證配置 {#credentials}

## 支援的驗證類型 {#supported-authentication-types}

Adobe Experience Platform目標SDK支援數種驗證類型：

* 承載驗證
* OAuth 2，含授權碼
* 具有密碼授權的第2個非統組織
* 具有客戶端憑據授予的OAuth 2

如需各種支援的OAuth 2流程，以及自訂OAuth 2支援，請參閱[OAuth 2 authentication](./oauth2-authentication.md)上的目的地SDK檔案。

您可以透過`/destinations`端點的`customerAuthenticationConfigurations`參數來設定目的地的驗證資訊。 請參閱目標設定文章中的[客戶驗證設定區段](./destination-configuration.md#customer-authentication-configurations)。

## 何時使用`/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您&#x200B;*不*&#x200B;需要使用`/credentials` API端點。 反之，您可以透過`/destinations`端點的`customerAuthenticationConfigurations`參數來設定目的地的驗證資訊。

如果Adobe和目標之間存在全局身份驗證系統，且[!DNL Platform]客戶不需要提供任何身份驗證憑據來連接到您的目標，請使用`activation/authoring/credentials` API端點，並在[目標配置](./destination-configuration.md#destination-delivery)中選擇`PLATFORM_AUTHENTICATION`。 在此情況下，您必須使用`/credentials` API端點建立憑證物件。 請閱讀[憑證API端點操作](./credentials-configuration-api.md)以獲得可在`/credentials`端點上執行的完整操作清單。
