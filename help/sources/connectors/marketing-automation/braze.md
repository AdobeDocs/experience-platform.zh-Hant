---
title: 釺焊電流來源概述
description: 瞭解如何從釺焊電流將資料串流到Experience Platform。
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>此 [!DNL Braze Currents] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括 [!DNL Braze Currents].

[!DNL Braze] 促進消費者與品牌之間以客戶為中心的即時互動。 [!DNL Braze Currents] 是來自Braze平台的參與事件即時資料流，是最強大但最精細的匯出專案 [!DNL Braze] 平台。

## 先決條件

若要完成本指南中的步驟，您將需要：

* 登入 [Adobe Experience Platform](https://platform.adobe.com) 和建立新串流來源連線的許可權。
* 登入您的 [[!DNL Braze] 儀表板](https://dashboard.braze.com/sign_in)，未使用 [電流聯結器授權](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)和建立聯結器的許可權。 如需詳細資訊，請閱讀 [設定需求 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### 收集必要的認證

若要成功提交您的 [!DNL Braze Currents] 資料若要Experience Platform Experience Platform，您必須在以下的 [!DNL Braze] UI儀表板。

| 欄位 | 說明 |
| --- | --- |
| 使用者端ID | 與您的Experience Platform來源相關聯的使用者端ID。 |
| 使用者端密碼 | 與您的Experience Platform來源相關聯的使用者端密碼。 |
| 租使用者ID | 與您的Experience Platform來源相關聯的租使用者ID。 |
| 沙箱名稱 | 與您的Experience Platform來源關聯的沙箱。 |
| 資料流ID | 與您的Experience Platform來源相關聯的資料流ID。 |
| 串流端點 | 與您的Experience Platform來源相關聯的串流端點。 **注意**： [!DNL Braze] 自動將其轉換為批次串流端點。 |

如需如何擷取這些值的詳細資訊，請閱讀以下指南： [Platform API快速入門](../../../landing/api-authentication.md). 有關使用的資訊 [!DNL Braze] 儀表板，讀取 [!DNL Braze] 操作方法指南 [導覽至電流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## 後續步驟

閱讀本檔案後，您已完成從串流處理資料所需的先決條件設定 [!DNL Braze Currents] 要Experience Platform的帳戶。 您現在可以在以下位置繼續參閱指南： [正在連線 [!DNL Braze Currents] 以使用使用者介面Experience Platform](../../tutorials/ui/create/marketing-automation/braze.md).