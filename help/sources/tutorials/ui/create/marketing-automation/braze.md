---
title: 在UI中為Braze資料建立資料流
description: 瞭解如何使用Adobe Experience Platform UI為您的Braze帳戶建立資料流。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 59600165328181e41750b9b2a1f4fbf162dd1df5
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# 在使用者介面中建立[!DNL Braze Currents]來源連線

>[!NOTE]
>
>[!DNL Braze Currents]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

[!DNL Braze]可即時促進消費者與品牌之間以客戶為中心的互動。 [!DNL Braze Currents]是來自Braze平台的參與事件即時資料流，是[!DNL Braze]平台中最穩健但最精細的匯出專案。

請閱讀下列教學課程，瞭解如何在UI中將[!DNL Braze]帳戶的參與事件資料帶入Adobe Experience Platform。

## 先決條件

若要完成本指南中的步驟，您將需要：

* 登入[Adobe Experience Platform](https://platform.adobe.com)並取得建立新串流來源連線的許可權。
* 登入您的[[!DNL Braze] 儀表板](https://dashboard.braze.com/sign_in)、未使用的[Currences Connector授權](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)，以及建立聯結器的許可權。 如需詳細資訊，請閱讀設定 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements)的[需求。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

此教學課程也需要實際瞭解[[!DNL Braze] 電流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)。

如果您已有[!DNL Braze]連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/marketing-automation.md)的教學課程。

## 建立 XDM 結構描述

>[!TIP]
>
>如果您是第一次建立[!DNL Braze Currents]連線，則必須建立體驗資料模型(XDM)結構描述。 如果您已建立[!DNL Braze Currents]的結構描述，則可以跳過此步驟，繼續進行[將您的帳戶連線到Experience Platform](#connect)。

在Platform UI中，使用左側導覽，然後選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;以存取[!UICONTROL 結構描述]工作區。 接著，選取&#x200B;**[!UICONTROL 建立結構描述]**，然後選取&#x200B;**[!UICONTROL 體驗事件]**。 若要繼續，請選取&#x200B;**[!UICONTROL 下一步]**。

![已完成的結構描述。](../../../../images/tutorials/create/braze/schema.png)

提供結構描述的名稱和說明。 然後，使用[!UICONTROL 構成]面板來設定結構描述屬性。 在[!UICONTROL 欄位群組]下，選取&#x200B;**[!UICONTROL 新增]**&#x200B;並新增[!UICONTROL Braze Currences使用者事件]欄位群組。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。

如需結構描述的詳細資訊，請參閱[在UI](../../../../../xdm/tutorials/create-schema-ui.md)中建立結構描述的指南。

## 將您的[!DNL Braze]帳戶連線至Experience Platform {#connect}

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*行銷自動化*&#x200B;類別下，選取&#x200B;**[!UICONTROL 硬碟電流]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取「硬碟電流」來源的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/braze/catalog.png)

接著，上傳提供的[Braze Currences範例檔案](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json)。 此檔案包含Braze在事件中可能傳送的所有可能欄位。

![「新增資料」畫面。](../../../../images/tutorials/create/braze/select-data.png)

上傳檔案後，您必須提供資料流詳細資訊，包括資料集和您對應至的結構描述的相關資訊。  如果這是您第一次連線銅製電流來源，請建立新的資料集。  否則，您可以使用任何參照Braze結構的現有資料集。  如果建立新資料集，請使用我們在上一節中建立的結構描述。
![「資料流詳細資料」畫面醒目提示「資料集詳細資料」。](../../../../images/tutorials/create/braze/dataflow-detail.png)

然後，使用對應介面為資料設定對應。

![「對應」畫面。](../../../../images/tutorials/create/braze/mapping_errors.png)

對應將有以下需要解決的問題。

在來源資料中，*id*&#x200B;將錯誤對應到&#x200B;*_braze.appID*。 您必須在結構描述的根層級將目標對應欄位變更為&#x200B;*_id*。 接下來，確定&#x200B;*properties.is_amp*&#x200B;對應至&#x200B;*_braze.messaging.email.isAMP*。

接著，刪除&#x200B;*time*&#x200B;到&#x200B;*timestamp*&#x200B;的對應，然後選取新增(`+`)圖示，然後選取&#x200B;**[!UICONTROL 新增計算欄位]**。 在提供的方塊中，輸入&#x200B;*time \* 1000*&#x200B;並選取&#x200B;**[!UICONTROL 儲存]**。

新增新的計算欄位後，選取新的來源欄位旁的&#x200B;**[!UICONTROL 對應目標欄位]**，並將其對應到結構描述根層級的&#x200B;*時間戳記*。 然後您應該選取&#x200B;**[!UICONTROL 驗證]**，以確保您沒有其他錯誤。

>[!IMPORTANT]
>
>銅製時間戳記不是以毫秒表示，而是以秒表示。 為了準確反映Experience Platform中的時間戳記，您需要建立以毫秒為單位的計算欄位。 計算「時間* 1000」將正確地轉換為毫秒，適合對應到Experience Platform內的時間戳記欄位。
>
>![正在建立時間戳記](../../../../images/tutorials/create/braze/create-calculated-field.png)的計算欄位

![沒有錯誤的對應。](../../../../images/tutorials/create/braze/completed_mapping.png)

完成後，選取&#x200B;**[!UICONTROL 下一步]**。 使用檢閱頁面確認資料流的詳細資料，然後選取&#x200B;**[!UICONTROL 完成]**。

### 收集必要的認證

建立連線後，您必須收集下列認證值，然後您會在「硬碟控制面板」中提供這些值，以將資料傳送至Experience Platform。 如需詳細資訊，請閱讀瀏覽至Currences](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents)的[!DNL Braze] [指南。

| 欄位 | 說明 |
| --- | --- |
| 用戶端 ID | 與您的Experience Platform來源相關聯的使用者端ID。 |
| 使用者端密碼 | 與您的Experience Platform來源相關聯的使用者端密碼。 |
| 租使用者ID | 與您的Experience Platform來源相關聯的租使用者ID。 |
| 沙箱名稱 | 與您的Experience Platform來源關聯的沙箱。 |
| 資料流 ID | 與您的Experience Platform來源相關聯的資料流ID。 |
| 串流端點 | 與您的Experience Platform來源相關聯的串流端點。 **注意**： [!DNL Braze]會自動將此轉換為批次串流端點。 |

### 設定[!DNL Braze Currents]將資料串流至您的資料來源

在[!DNL Braze Dashboard]中，導覽至「合作夥伴整合&#x200B;**->**&#x200B;資料匯出」，然後選取&#x200B;**[!DNL Create New Current]**。 系統會提示您提供聯結器的名稱、聯結器的相關通知連絡資訊，以及上方列出的憑證。 選取您要接收的事件，選擇性地設定任何想要的欄位排除/轉換，然後選取&#x200B;**[!DNL Launch Current]**。

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Braze]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，以將行銷自動化系統資料匯入 [!DNL Platform]](../../dataflow/marketing-automation.md)。
