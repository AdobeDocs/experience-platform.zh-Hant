---
description: Adobe Experience Platform的目標服務使用配置模板來構建目標功能的多個元件。 這些元件結合起來，使Experience Platform能夠連接到目標合作夥伴、發送自定義消息並激活整個數字生態系統中的配置檔案資料。
title: 配置選項在Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# 配置選項在Destination SDK

## 總覽 {#overview}

Adobe Experience Platform的目標服務使用配置模板來構建目標功能的多個元件。 這些元件結合起來，使Experience Platform能夠連接到目標合作夥伴、發送自定義消息並激活整個數字生態系統中的配置檔案資料。 Adobe Experience Platform使用的模板有：

* **目標配置**:包含有關目標的基本資訊。 此配置包括目標可支援的標識類型以及Adobe Experience Platform用戶介面中目標卡的各種UI屬性。
* **伺服器和模板規範**:將有關伺服器規格的資訊和Adobe用於將負載傳遞到目標的模板聯繫起來。
   * **伺服器規格**:儲存終結點詳細資訊的模板。
   * **模板規格**:在此模板中，可以定義如何在XDM架構和平台支援的格式之間轉換配置檔案屬性欄位。 有關支援的模板語言、消息格式以及Adobe設定與平台整合所需資訊的詳細資訊，請閱讀 [消息格式](./message-format.md)。
* **驗證配置**:這些設定定義了Adobe Experience Platform用戶如何連接到目標。
* **受眾元資料配置**:此模板允許您配置如何以寫程式方式在目標中建立、更新或刪除受眾/網段。

![Destination SDK模板和配置](./assets/self-service-configuration.png)

## 相關連結 {#related-links}

下面的頁面提供了有關Destination SDK中可用的功能和配置選項以及可執行的相應API操作的更多詳細資訊。

| 功能說明 | API 參考資料 |
|--- |--- |
| [目標配置](./destination-configuration.md) | [目標API終結點操作](./destination-configuration-api.md) |
| [伺服器和模板規範](./server-and-template-configuration.md) | [目標伺服器API終結點操作](./destination-server-api.md) |
| [驗證配置](./authentication-configuration.md) | [憑據終結點API操作](./credentials-configuration-api.md) |
| [受眾元資料管理](./audience-metadata-management.md) | [受眾元資料終結點API操作](./audience-metadata-api.md) |
| [OAuth 2配置](./oauth2-authentication.md) | 使用 `customerAuthenticationConfigurations` 參數 [/目標API終結點](./destination-configuration-api.md)。 |
| [訊息格式](./message-format.md) | - |
| [目標測試](./test-destination.md) | [目標測試API操作](./destination-testing-api.md) |
| [目標發佈](./configure-destination-instructions.md#publish-destination) | [目標發佈API操作](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
