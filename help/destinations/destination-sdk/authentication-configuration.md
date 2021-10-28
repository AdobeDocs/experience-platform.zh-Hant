---
description: 使用Adobe Experience Platform Destination SDK中支援的驗證設定，驗證使用者並啟用資料至您的目的地端點。
title: 驗證配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 驗證配置 {#credentials}

## 支援的驗證類型 {#supported-authentication-types}

Adobe Experience Platform目標SDK支援數種驗證類型：

* 承載驗證
* OAuth 2，含授權碼
* 具有密碼授權的第2個非統組織
* 具有客戶端憑據授予的OAuth 2

您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。 請參閱 [客戶驗證設定區段](./destination-configuration.md#customer-authentication-configurations) 在目的地設定文章及以下各節，以取得各驗證類型設定的詳細資訊。

## 承載驗證 {#bearer}

若要為目的地設定承載類型驗證，您只需要設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2驗證 {#oauth2}

如需如何設定各種支援的OAuth 2流程，以及自訂OAuth 2支援的詳細資訊，請參閱以下的Destination SDK檔案： [OAuth 2驗證](./oauth2-authentication.md).


## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 *不* 需要使用 `/credentials` API端點。 反之，您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。

此 `/credentials` 當Adobe與您的目的地和 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。

在此情況下，您必須使用 `/credentials` API端點。 您也必須選取 `PLATFORM_AUTHENTICATION` 在 [目的地配置](./destination-configuration.md#destination-delivery). 閱讀 [憑證API端點操作](./credentials-configuration-api.md) 以取得您可在 `/credentials` 端點。
