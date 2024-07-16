---
title: 使用GitHub網頁介面建立目的地檔案頁面
description: 此頁面上的指示會示範如何使用GitHub網頁介面為您的Experience Platform目的地製作檔案頁面，並提交以供檢閱。
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# 使用GitHub網頁介面建立目的地檔案頁面 {#github-interface}

以下指示說明如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)。 在依照這裡指示的步驟進行之前，請務必閱讀[在Adobe Experience Platform目的地中記錄您的目的地](./documentation-instructions.md)。

>[!TIP]
>
>另請參閱Adobe貢獻者指南中的支援檔案：
>* [安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [在本機設定檔案的Git存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [重大變更的GitHub貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)。

## 設定您的GitHub製作環境 {#set-up-environment}

1. 在您的瀏覽器中，瀏覽至`https://github.com/AdobeDocs/experience-platform.en`。
2. 若要[分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository)存放庫，請按一下&#x200B;**分支**，如下所示。 這會在您自己的GitHub帳戶中建立Experience Platform存放庫的復本。

   ![分支Adobe檔案存放庫](../assets/docs-framework/ssd-fork-repository.gif)

3. 在存放庫復本中，為您的專案建立新分支，如下所示。 將此新分支用於您的工作。

   ![建立新的GitHub分支](../assets/docs-framework/new-branch-github.gif)

4. 在取用存放庫的GitHub資料夾結構中，導覽至`experience-platform.en/help/destinations/catalog/[...]`，其中`[...]`是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取`personalization`類別。 選取&#x200B;**新增檔案>建立新檔案**。

   ![新增檔案](../assets/docs-framework/github-navigate-and-create-file.gif)

5. 為您的目的地命名`YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目的地名稱。 例如，如果您的公司名為Moviestar，您可將您的檔案命名為`moviestar.md`。

## 為您的目的地編寫檔案頁面 {#author-documentation}

1. 您將根據[檔案自助服務範本](./self-service-template.md)建立目的地頁面的內容。 **[下載](../assets/docs-framework/yourdestination-template.zip)**&#x200B;範本並將其解壓縮，以解壓縮`.md`檔案範本。
2. 線上上Markdown編輯器（例如[dillinger.io](https://dillinger.io/)）中，使用您目的地的相關資訊貼上並編輯範本內容。 請依照範本中的指示操作，以取得您應填寫的內容以及哪些段落可以移除的詳細資訊。

   >[!TIP]
   >
   >您可以隨時關閉瀏覽器視窗，稍後再重新開啟。 系統會自動儲存您的工作，當您重新開啟瀏覽器時，系統會在您等待您完成工作。
3. 將內容從Markdown編輯器複製到GitHub的新檔案中。
4. 對於您打算使用的任何熒幕擷取畫面或影像，請使用GitHub介面將檔案上傳到`experience-platform.en/help/destinations/assets/catalog/[...]`，其中`[...]`是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取`personalization`類別。 您需要從正在編寫的頁面連結到影像。 請參閱[如何連結至影像的說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images)。

   ![將影像上傳到GitHub](../assets/docs-framework/upload-image.gif)

5. 準備就緒後，將檔案儲存在分支中。

![確認檔案建立](../assets/docs-framework/ssd-confirm-file-creation.png)

## 提交您的檔案以供檢閱 {#submit-review}

>[!TIP]
>
>請注意，您無法在此處中斷任何內容。 依照本節的指示，您只是建議更新說明檔案。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 儲存檔案並上傳所需影像後，您可以開啟提取請求(PR)，將您的工作分支合併至Adobe檔案存放庫的主分支。 確定已選取您處理的分支，並選取&#x200B;**Contribute >開啟提取請求**。

![建立提取請求](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 請確定基礎分支和比較分支正確無誤。 將說明您更新的附註新增至PR，並選取&#x200B;**建立提取請求**。 這會開啟PR，以將復本的工作分支合併至Adobe存放庫的主分支。

   >[!TIP]
   >
   >保留&#x200B;**允許維護者編輯**&#x200B;核取方塊為已選取狀態，讓Adobe檔案團隊可以編輯PR。

   ![建立提取要求以Adobe檔案存放庫](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 此時，系統會顯示通知，提示您簽署Adobe貢獻者授權合約(CLA)。 此為必要步驟。 簽署CLA後，請重新整理PR頁面並提交提取請求。

1. 您可以檢查`https://github.com/AdobeDocs/experience-platform.en`中的&#x200B;**提取請求**&#x200B;索引標籤，以確認提取請求已提交。

   ![PR成功](../assets/docs-framework/ssd-pr-successful.png)

1. 感謝支持！Adobe檔案團隊會聯絡PR，以備需要編輯時使用，並告知您檔案將於何時發佈。

>[!TIP]
>
>若要新增影像和連結至您的檔案，以及有關Markdown的任何其他問題，請閱讀Adobe合作撰寫指南中的[使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)。
