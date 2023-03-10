---
keywords: Experience Platform；快速入門；content ai;commerce ai；內容標籤
solution: Experience Platform
title: 內容標籤快速入門
description: 內容標籤採用Adobe I/OAPI。 若要呼叫Adobe I/OAPI和I/O主控台整合，您必須先完成驗證教學課程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a98639851e7245b9cbd6fe42b35b4730dd19c3f8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 內容標籤快速入門

[!DNL Content tagging] 利用Adobe I/OAPI。 若要呼叫Adobe I/OAPI和I/O主控台整合，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

不過，當您進入 **新增API** 步驟中，API位於「Experience Cloud」下，而非「Adobe Experience Platform」下，如下列螢幕擷取所示：

![新增內容標籤](./images/add-api-updated.png)

完成驗證教學課程，可提供所有Adobe I/OAPI呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## 建立Postman環境（可選）

在Adobe Developer Console中設定專案和API後，您就可以選擇下載Postman的環境檔案。 在 **[!UICONTROL API]** 選取專案的左側邊欄， **[!UICONTROL 內容標籤]**. 隨即開啟新索引標籤，其中包含標示為「[!DNL Try it out]」。 選擇 **下載Postman** 下載用來設定postman環境的JSON檔案。

![下載postman](./images/add-to-postman-updated.png)

下載檔案後，請開啟Postman並選取 **齒輪表徵圖** 開啟 **管理環境** 對話框。

![齒輪表徵圖](./images/select-gear-icon.png)

下一步，選擇 **匯入** 從 **管理環境** 對話框。

![匯入](./images/import-updated.png)

系統會將您重新導向，並要求您從電腦中選取環境檔案。 選取您先前下載的JSON檔案，然後選取 **開啟** 來載入環境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系統會將您重新導向回 *管理環境* 標籤中填入新環境名稱。 選取環境名稱以檢視及編輯Postman中可用的變數。 您仍需手動填入 `JWT_TOKEN` 和 `ACCESS_TOKEN`. 這些值應已在完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

完成後，您的變數應該會像下方的螢幕擷圖一樣。 選擇 **更新** 完成環境設定。

![](./images/final-environment-updated.png)

您現在可以從右上角的下拉式功能表中選取您的環境，並自動填入任何儲存的值。 您隨時只需重新編輯值，以更新所有API呼叫。

![範例](./images/select-environment-updated.png)

如需使用Postman使用Adobe I/OAPI的詳細資訊，請參閱上的媒體貼文 [在Adobe I/O上使用Postman進行JWT驗證](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md) Experience Platform疑難排解指南中。

## 後續步驟 {#next-steps}

擁有所有憑據後，您就可以為 [!DNL Content tagging]. 以下文檔有助於了解Extensibility Framework和環境設定。

若要深入了解Extensibility Framework，請從閱讀 [擴充性簡介](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) 檔案。 本檔案概述必要條件和布建需求。

深入了解如何為 [!DNL Content tagging]，請從閱讀的指南開始 [設定開發人員環境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). 本檔案提供設定指示，可讓您針對Asset compute服務進行開發。
