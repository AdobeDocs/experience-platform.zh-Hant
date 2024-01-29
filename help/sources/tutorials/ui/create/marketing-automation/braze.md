---
title: 在UI中為Braze資料建立資料流
description: 瞭解如何使用Adobe Experience Platform UI為您的Braze帳戶建立資料流。
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 92d3a7143edc81cc5266ef5a33a8c53dcfdf1074
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# 建立 [!DNL Braze] ui中的來源連線

>[!NOTE]
>
>此 [!DNL Braze] 來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

[!DNL Braze] 促進消費者與品牌之間以客戶為中心的即時互動。 [!DNL Braze Currents] 是來自Braze平台的參與事件即時資料流，是最強大但最精細的匯出專案 [!DNL Braze] 平台。

請閱讀下列教學課程，瞭解如何從匯入參與事件資料 [!DNL Braze] 在UI中帳戶至Adobe Experience Platform。

## 先決條件

若要完成本指南中的步驟，您將需要：

* 登入 [Adobe Experience Platform](https://platform.adobe.com) 和建立新串流來源連線的許可權。
* 登入您的 [[!DNL Braze] 儀表板](https://dashboard.braze.com/sign_in)，未使用 [電流聯結器授權](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)和建立聯結器的許可權。 如需詳細資訊，請閱讀 [設定需求 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

本教學課程也需要您實際瞭解 [[!DNL Braze] 電流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

如果您已有 [!DNL Braze] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/marketing-automation.md).

## 連線您的 [!DNL Braze] 要Experience Platform的帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *行銷自動化* 類別，選取 **[!UICONTROL 釺焊]**，然後選取 **[!UICONTROL 新增資料]**.

![已選取「釺焊電流」來源的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/braze/catalog.png)

接下來，上傳提供的 [「銅線電流」範例檔案](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). 此檔案包含Braze在事件中可能傳送的所有可能欄位。

![「新增資料」畫面。](../../../../images/tutorials/create/braze/select-data.png)

上傳檔案後，您必須提供資料流詳細資訊，包括資料集和您對應至的結構描述的相關資訊。
![「資料流詳細資料」畫面會醒目提示「資料集詳細資料」。](../../../../images/tutorials/create/braze/dataflow-detail.png)

然後，使用對應介面為資料設定對應。

![「對應」畫面。](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>銅製時間戳記不是以毫秒表示，而是以秒表示。 為了準確反映Experience Platform中的時間戳記，您需要建立以毫秒為單位的計算欄位。 計算「時間* 1000」將正確地轉換為毫秒，適合對應到Experience Platform內的時間戳記欄位。
>
>![建立時間戳記的計算欄位 ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### 收集必要的認證

建立連線後，您必須收集下列認證值，然後您會在「硬碟控制面板」中提供這些值，以傳送資料至 [!DNL Platform]. 如需詳細資訊，請閱讀 [!DNL Braze] [導覽至洋流的指南](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| 欄位 | 說明 |
| ---------- | ----------- |
| `Client ID` | 與您的關聯的使用者端ID [!DNL Platform] 來源。 |
| `Client Secret` | 與您的關聯的使用者端密碼 [!DNL Platform] 來源。 |
| `Tenant ID` | 與您的相關聯的租使用者ID [!DNL Platform] 來源。 |
| `Sandbox Name` | 與您的關聯的沙箱 [!DNL Platform] 來源。 |
| `Dataflow ID` | 與您的關聯的資料流ID [!DNL Platform] 來源。 |
| `Streaming Endpoint` | 與您的相關聯的串流端點 [!DNL Platform] 來源。 請注意，Braze會自動將其轉換為批次串流端點。 |

### 設定 [!DNL Braze Currents] 將資料串流至您的資料來源

在 [!DNL Braze Dashboard]，導覽至合作夥伴整合 **->** 資料匯出，然後選取 **[!DNL Create New Current]**. 系統會提示您提供聯結器的名稱、聯結器的相關通知連絡資訊，以及上方列出的憑證。 選取您要接收的事件，選擇性地設定任何所需的欄位排除/轉換，然後選取 **[!DNL Launch Current]**.

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL Braze] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將行銷自動化系統資料帶入 [!DNL Platform]](../../dataflow/marketing-automation.md).