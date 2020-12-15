---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform, Intelligent Services
title: 內容與商務AI快速入門
topic: Getting started
description: 內容與商務AI運用Adobe I/O API。 若要呼叫Adobe I/O API和I/O Console整合，您必須先完成驗證教學課程。
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# 內容與商務AI快速入門

>[!NOTE]
>
>內容與商務AI為測試版。 說明檔案可能會有所變更。

[!DNL Content and Commerce AI] 運用Adobe I/O API。 若要呼叫Adobe I/O API和I/O Console整合，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。

不過，當您進入「新增 **API** 」步驟時，API會位於Experience Cloud下方，而非Adobe Experience Platform，如下列螢幕擷取所示：

![新增內容與商務AI](./images/add-api.png)

完成驗證教學課程後，所有Adobe I/O API呼叫中每個必要標題的值都會顯示，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 建立郵遞員環境（可選）

在Adobe Developer Console中設定專案和API後，您就可以選擇下載Postman的環境檔案。 在 **[!UICONTROL 專案]** 左側導軌的API下，選取「 **[!UICONTROL 內容與商務AI」]**。 隨即開啟新的標籤，其中包含標示為「[!DNL Try it out]」的卡片。 選 **取「下載郵遞員** 」，下載用來設定郵遞員環境的JSON檔案。

![下載為postman](./images/add-to-postman.png)

下載檔案後，請開啟Postman並選取右上 **方的齒輪圖示** ，以開啟管理 **環境對話** 框。

![齒輪表徵圖](./images/select-gear-icon.png)

接著，在「管 **理環境** 」對話方 **塊中選擇「匯入** 」。

![導入](./images/import.png)

系統會重定向您，並要求您從電腦中選擇環境檔案。 選取您先前下載的JSON檔案，然後選 **取** 「開啟」以載入環境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系統會將您重新導向至「管 *理環境* 」標籤，並填入新的環境名稱。 選擇環境名稱，以檢視並編輯Postman中可用的變數。 您仍需手動填入 `JWT_TOKEN` 和 `ACCESS_TOKEN`。 這些值應在完成驗證教程時 [獲得](../../tutorials/authentication.md)。

![](./images/re-direct.png)

完成後，您的變數看起來應類似下方的螢幕擷取。 選擇 **更新** ，完成環境設定。

![](./images/final-environment.png)

您現在可以從右上角的下拉式選單中選取您的環境，並自動填入任何儲存的值。 只要隨時重新編輯值，即可更新所有API呼叫。

![示例](./images/select-environment.png)

如需使用Postman使用Adobe I/O API的詳細資訊，請參閱Adobe I/O [上使用Postman進行JWT驗證的中篇貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md) 。

## 下一步 {#next-steps}

一旦您擁有了所有憑據，就可以為設定自定義工作器 [!DNL Content and Commerce AI]。 以下檔案有助於瞭解擴充性架構與環境設定。

若要進一步瞭解擴充性架構，請先閱讀擴充性文 [件的簡介](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) 。 本檔案概述必要條件和布建需求。

若要進一步瞭解如何設定環境， [!DNL Content and Commerce AI]請先閱讀設定開發人 [員環境的指南](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)。 本檔案提供設定指示，可讓您針對資產計算服務進行開發。