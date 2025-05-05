---
title: 釺焊電流Source概述
description: 瞭解如何將資料從釺焊電流串流到Experience Platform。
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>[!DNL Braze Currents]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括[!DNL Braze Currents]。

[!DNL Braze]可即時促進消費者與品牌之間以客戶為中心的互動。 [!DNL Braze Currents]是來自Braze平台的參與事件即時資料流，是[!DNL Braze]平台中最穩健但最精細的匯出專案。

## 先決條件

若要完成本指南中的步驟，您將需要：

* 登入[Adobe Experience Platform](https://platform.adobe.com)並取得建立新串流來源連線的許可權。
* 登入您的[[!DNL Braze] 儀表板](https://dashboard.braze.com/sign_in)、未使用的[Currences Connector授權](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)，以及建立聯結器的許可權。 如需詳細資訊，請閱讀設定 [!DNL Currents][&#128279;](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements)的需求。

### 收集必要的認證

若要成功將您的[!DNL Braze Currents]資料提交至Experience Platform，您必須在[!DNL Braze] UI儀表板中輸入下列Experience Platform認證。

| 欄位 | 說明 |
| --- | --- |
| 用戶端 ID | 與您的Experience Platform來源相關聯的使用者端ID。 |
| 使用者端密碼 | 與您的Experience Platform來源相關聯的使用者端密碼。 |
| 租用戶 ID | 與您的Experience Platform來源相關聯的租使用者ID。 |
| 沙箱名稱 | 與您的Experience Platform來源關聯的沙箱。 |
| 資料流 ID | 與您的Experience Platform來源相關聯的資料流ID。 |
| 串流端點 | 與您的Experience Platform來源相關聯的串流端點。 **注意**： [!DNL Braze]會自動將此轉換為批次串流端點。 |

如需如何擷取這些值的詳細資訊，請閱讀[Experience Platform API快速入門](../../../landing/api-authentication.md)的指南。 如需有關使用[!DNL Braze]儀表板的資訊，請閱讀如何[瀏覽至Currences](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents)的[!DNL Braze]指南。

## 後續步驟

閱讀本檔案後，您已完成從[!DNL Braze Currents]帳戶將資料串流至Experience Platform所需的先決條件設定。 您現在可以使用使用者介面[&#128279;](../../tutorials/ui/create/marketing-automation/braze.md)在連線 [!DNL Braze Currents] 至Experience Platform時繼續參閱指南。
