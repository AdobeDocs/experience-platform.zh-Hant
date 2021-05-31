---
keywords: Experience Platform；快速入門；content ai;commerce ai;content and commerce ai
solution: Experience Platform, Intelligent Services
title: 內容與商務AI快速入門
topic-legacy: Getting started
description: Content and Commerce AI利用Adobe I/OAPI。 若要呼叫Adobe I/OAPI和I/O主控台整合，您必須先完成驗證教學課程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# 內容與商務AI快速入門

>[!NOTE]
>
>內容與商務AI正在測試中。 說明檔案可能會有所變更。

[!DNL Content and Commerce AI] 利用Adobe I/OAPI。若要呼叫Adobe I/OAPI和I/O主控台整合，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。

不過，當您進入&#x200B;**新增API**&#x200B;步驟時，API會位於「Experience Cloud」下，而非Adobe Experience Platform，如下列螢幕擷取所示：

![新增內容與商務AI](./images/add-api.png)

完成驗證教學課程，可提供所有Adobe I/OAPI呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 建立Postman環境（可選）

在「Adobe開發人員控制台」中設定專案和API後，您就可以選擇下載Postman的環境檔案。 在專案的左側邊欄&#x200B;**[!UICONTROL API]**&#x200B;下，選取&#x200B;**[!UICONTROL 內容與商務AI]**。 隨即開啟新索引標籤，其中包含標示為「[!DNL Try it out]」的資訊卡。 選取「**下載Postman**」 ，以下載用於設定Postman環境的JSON檔案。

![下載postman](./images/add-to-postman.png)

下載檔案後，請開啟Postman並選取右上角的&#x200B;**齒輪圖示**&#x200B;以開啟&#x200B;**管理環境**&#x200B;對話方塊。

![齒輪表徵圖](./images/select-gear-icon.png)

接下來，從&#x200B;**管理環境**&#x200B;對話方塊內選擇&#x200B;**匯入**。

![匯入](./images/import.png)

系統會將您重新導向，並要求您從電腦中選取環境檔案。 選取您先前下載的JSON檔案，然後選取&#x200B;**Open**&#x200B;以載入環境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系統會將您重新導向回「*管理環境*」標籤，並填入新環境名稱。 選取環境名稱以檢視及編輯Postman中可用的變數。 您仍需手動填入`JWT_TOKEN`和`ACCESS_TOKEN`。 完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)時應已取得這些值。

![](./images/re-direct.png)

完成後，您的變數應該會像下方的螢幕擷圖一樣。 選擇&#x200B;**更新**&#x200B;以完成環境設定。

![](./images/final-environment.png)

您現在可以從右上角的下拉式功能表中選取您的環境，並自動填入任何儲存的值。 您隨時只需重新編輯值，以更新所有API呼叫。

![範例](./images/select-environment.png)

如需使用Postman使用Adobe I/OAPI的詳細資訊，請參閱[上的使用Postman進行Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)上JWT驗證的媒體貼文。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md)的區段。

## 下一步 {#next-steps}

擁有所有憑據後，您就可以為[!DNL Content and Commerce AI]設定自定義工作器。 以下文檔有助於了解Extensibility Framework和環境設定。

要了解有關Extensibility Framework的詳細資訊，請從閱讀Extensibility](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)文檔的[簡介開始。 本檔案概述必要條件和布建需求。

若要進一步了解如何設定[!DNL Content and Commerce AI]的環境，請從閱讀[設定開發人員環境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html)的指南開始。 本檔案提供設定指示，可讓您針對Asset compute服務進行開發。
