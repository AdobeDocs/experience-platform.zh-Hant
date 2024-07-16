---
keywords: Experience Platform；首頁；熱門主題；onetrust；OneTrust
solution: Experience Platform
title: 在使用者介面中建立OneTrust Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立OneTrust來源連線。
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL OneTrust Integration]來源連線

>[!NOTE]
>
>[!DNL OneTrust Integration]來源僅支援同意和偏好設定資料的擷取，不支援Cookie。

本教學課程提供建立[[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US)來源連線的步驟，以使用Platform使用者介面將歷史資料和排程同意資料擷取到Adobe Experience Platform。

## 先決條件

>[!IMPORTANT]
>
>[!DNL OneTrust Integration]來源聯結器和檔案是由[!DNL OneTrust Integration]團隊所建立。 若有任何查詢或更新要求，請直接連絡[[!DNL OneTrust] 團隊](https://my.onetrust.com/s/contactsupport?language=en_US)。

在將[!DNL OneTrust Integration]連線到平台之前，您必須先擷取您的存取權杖。 如需尋找存取Token的詳細指示，請參閱[[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

存取權杖到期後不會自動重新整理，因為[!DNL OneTrust]不支援系統間重新整理權杖。 因此，在連線過期之前，必須確定您的存取權杖已在連線中更新。 存取權杖的最大可設定存留期為一年。 若要深入瞭解如何更新您的存取權杖，請參閱有關管理您的OAuth 2.0使用者端認證](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials)的[[!DNL OneTrust] 檔案。

### 收集必要的認證

為了將[!DNL OneTrust Integration]連線到Platform，您必須提供下列驗證認證的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 主機名稱 | 需要從中提取[!DNL OneTrust Integration]資料的環境。 | `app.onetrust.com` |
| 授權測試URL | （選用）建立基本連線時，授權測試URL會用於驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 | |
| 存取權杖 | 與您的[!DNL OneTrust Integration]帳戶對應的存取權杖。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

如需這些認證的詳細資訊，請參閱[[!DNL OneTrust Integration] 驗證檔案](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

## 連線您的[!DNL OneTrust Integration]帳戶

>[!NOTE]
>
>[!DNL OneTrust Integration] API規格正在與Adobe共用以進行資料擷取。

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取Experience Platform中可用來源目錄的[!UICONTROL 來源]工作區。

使用&#x200B;*[!UICONTROL 類別]*&#x200B;功能表，依類別篩選來源。 或者，在搜尋列中輸入來源名稱，從目錄中尋找特定來源。

移至[!DNL OneTrust Integration]來源卡片的[!UICONTROL 同意和偏好設定]類別。 若要開始，請選取&#x200B;**[!UICONTROL 新增資料]**。

![Experience PlatformUI來源目錄。](../../../../images/tutorials/create/onetrust/catalog.png)

**[!UICONTROL 連線OneTrust整合帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL OneTrust Integration]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![來源工作流程中的現有帳戶驗證步驟。](../../../../images/tutorials/create/onetrust/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![來源工作流程中的新帳戶驗證步驟。](../../../../images/tutorials/create/onetrust/new.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL OneTrust Integration]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將同意資料帶入Platform](../../dataflow/consent-and-preferences.md)。
