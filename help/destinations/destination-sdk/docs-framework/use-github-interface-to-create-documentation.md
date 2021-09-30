---
title: '使用GitHub網頁介面建立目的地檔案頁面 '
description: 本頁指示會示範如何使用GitHub網頁介面，為您的Experience Platform目的地製作檔案頁面並提交以供審核。
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: 83539a9aa2fddcae0c9a44302d8bfa9d9f56de0c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# 使用GitHub網頁介面建立目的地檔案頁面 {#github-interface}

以下指示說明如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)。 在執行此處指示的步驟之前，請務必閱讀[Adobe Experience Platform目的地的檔案](./documentation-instructions.md)。

>[!TIP]
>
>另請參閱Adobe貢獻者指南中的支援檔案：
>* [安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本機設定供文件使用的 Git 存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [適用於重大變更的 GitHub 貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 設定您的GitHub製作環境 {#set-up-environment}

1. 在您的瀏覽器中，導覽至`https://github.com/AdobeDocs/experience-platform.en`。
2. 若要取用存放庫[取用](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository)，請按一下&#x200B;**取用**，如下圖所示。

   ![分支Adobe檔案存放庫](./assets/ssd-fork-repository.gif)

3. 在存放庫的復本中，為專案建立新分支，如下所示。 使用這個新分支進行工作。

   ![建立新的GitHub分支](./assets/new-branch-github.gif)

4. 在取用存放庫的GitHub資料夾結構中，導覽至`experience-platform.en/help/destinations/catalog/[...]`，其中`[...]`是您目的地的所需類別。 例如，如果您要新增個人化目的地以Experience Platform，請選取`personalization`類別。 選擇&#x200B;**添加檔案>建立新檔案**。

   ![新增檔案](./assets/github-navigate-and-create-file.gif)

5. 將目的地命名為`YOURDESTINATION.md`，其中YOURDESTINATION是Adobe Experience Platform中目的地的名稱。 例如，如果貴公司稱為Moviestar，您可將檔案命名為`moviestar.md`。

## 編寫您目的地的檔案頁面 {#author-documentation}

1. 您將根據[檔案自助服務範本](./self-service-template.md)建立目的地頁面的內容。 **[](assets/yourdestination-template.zip)** 下載範本並將其解壓縮以解壓縮 `.md` 檔案範本。
2. 線上上Markdown編輯器中，貼上並編輯範本的內容，其中包含您目的地的相關資訊，例如[dillinger.io](https://dillinger.io/)。 請依照範本中的指示，詳細了解您應填入的內容，以及可以移除哪些段落。

   >[!TIP]
   >
   >您可以隨時關閉瀏覽器視窗，稍後重新開啟。 您的工作會自動儲存，當您重新開啟瀏覽器時，將會等候您。
3. 將Markdown編輯器中的內容複製到GitHub的新檔案中。
4. 對於您打算使用的任何螢幕擷取畫面或影像，請使用GitHub介面將檔案上傳至`experience-platform.en/help/destinations/assets/catalog/[...]`，其中`[...]`是您目的地的所需類別。 例如，如果您要新增個人化目的地以Experience Platform，請選取`personalization`類別。 您必須從編寫頁面連結至影像。 請參閱[指示如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images)。

   ![上傳影像至GitHub](./assets/upload-image.gif)

5. 準備好後，將檔案儲存在分支中。

![確認檔案建立](./assets/ssd-confirm-file-creation.png)

## 提交您的檔案以供審核 {#submit-review}

>[!TIP]
>
>請注意，這裡沒有什麼可以打破的。 依照本節中的指示，您只是建議進行檔案更新。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 儲存檔案並上傳所需影像後，您可以開啟提取請求(PR)，將工作分支合併至Adobe檔案存放庫的主分支。 請確定已選取您所處理的分支，並選取&#x200B;**Contribute > Pull request**。

![建立提取請求](./assets/ssd-create-pull-request-1.gif)

1. 請確定基分支和比較分支正確。 新增附註至PR，說明您的更新，並選取&#x200B;**建立提取請求**。 這會開啟PR，將復本的工作分支合併至Adobe存放庫的主分支。

   >[!TIP]
   >
   >保留「允許維護者編輯&#x200B;**」核取方塊，讓Adobe檔案團隊可以編輯PR。**

   ![建立提取請求以Adobe檔案存放庫](./assets/ssd-create-pull-request-2.png)

1. 此時會出現通知，提示您簽署Adobe貢獻者授權合約(CLA)。 這是必要步驟。 簽署CLA後，請重新整理PR頁面並提交提取請求。

1. 您可以檢查`https://github.com/AdobeDocs/experience-platform.en`中的&#x200B;**提取請求**&#x200B;標籤，以確認提取請求已提交。

   ![PR成功](./assets/ssd-pr-successful.png)

1. 感謝支持！Adobe檔案團隊會在PR中聯絡，以備您需要任何編輯作業時使用，並通知您檔案將於何時發佈。

>[!TIP]
>
>若要新增影像和連結至您的檔案，以及有關Markdown的任何其他問題，請參閱Adobe協作撰寫指南中的[使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)。
