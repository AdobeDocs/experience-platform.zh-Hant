---
keywords: Experience Platform；快速入門；內容；內容標籤
solution: Experience Platform
title: 內容標籤快速入門
description: 內容標籤會利用Adobe I/O API。 若要呼叫Adobe I/O API和I/O主控台整合，您必須先完成驗證教學課程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---

# 內容標籤快速入門

[!DNL Content tagging]利用Adobe I/OAPI。 若要呼叫Adobe I/O API和I/O主控台整合，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

不過，當您進入&#x200B;**新增API**&#x200B;步驟時，該API位於Creative Cloud下方，而非Adobe Experience Platform下方，如下列熒幕擷圖所示：

![正在新增內容標籤](./images/add-api-updated.png)

完成驗證教學課程，在所有Adobe I/OAPI呼叫中提供每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## 建立Postman環境（可選）

在Adobe Developer Console中設定專案和API後，您就可以選擇下載Postman的環境檔案。 在專案左側邊欄的&#x200B;**[!UICONTROL API]**&#x200B;下，選取&#x200B;**[!UICONTROL 內容標籤]**。 新標籤隨即開啟，內含標示為「[!DNL Try it out]」的卡片。 選取「下載Postman **的**」以下載用來設定您的Postman環境的JSON檔案。

為postman](./images/add-to-postman-updated.png)下載![

下載檔案後，請開啟Postman並選取右上方的&#x200B;**齒輪圖示**，以開啟&#x200B;**管理環境**&#x200B;對話方塊。

![齒輪圖示](./images/select-gear-icon.png)

接下來，在&#x200B;**管理環境**&#x200B;對話方塊中選取&#x200B;**匯入**。

![匯入](./images/import-updated.png)

系統會將您重新導向，並要求您從電腦中選取環境檔案。 選取您先前下載的JSON檔案，然後選取&#x200B;**開啟**&#x200B;以載入環境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系統會將您重新導向回&#x200B;*管理環境*&#x200B;標籤，並填入新的環境名稱。 選取環境名稱，以檢視和編輯Postman中可用的變數。 您仍需要手動填入`JWT_TOKEN`和`ACCESS_TOKEN`。 完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)時，應該已取得這些值。

![](./images/re-direct-updated.png)

完成後，您的變數看起來應該類似下面的熒幕擷圖。 選取&#x200B;**更新**&#x200B;以完成環境設定。

![](./images/final-environment-updated.png)

您現在可以從右上角的下拉式選單中選取您的環境，並自動填入任何儲存的值。 您只需隨時重新編輯值，即可更新所有API呼叫。

![範例](./images/select-environment-updated.png)

如需使用Postman使用Adobe I/O API的詳細資訊，請參閱[上的Medium文章，使用Postman在Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)上進行JWT驗證。

## 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md)的章節。

## 後續步驟 {#next-steps}

取得所有認證後，您就可以為[!DNL Content tagging]設定自訂背景工作。 下列檔案可協助您瞭解「擴充性架構」和環境設定。

若要深入瞭解擴充性架構，請先閱讀[擴充性簡介](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)檔案。 本檔案會概述先決條件和布建需求。

若要深入瞭解如何設定[!DNL Content tagging]的環境，請先閱讀[設定開發人員環境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html)的指南。 本檔案提供可讓您為Asset compute服務開發的設定指示。
