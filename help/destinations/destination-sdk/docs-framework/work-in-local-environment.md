---
title: 在本機環境中使用文字編輯器建立目的地檔案頁面
description: 本頁上的指示會示範如何使用文字編輯器在本機環境中運作，以撰寫適用於Experience Platform目的地的檔案頁面並提交以供檢閱。
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 在本機環境中使用文字編輯器建立目的地檔案頁面 {#local-authoring}

本頁上的指示會示範如何使用文字編輯器在本機環境中運作，以撰寫檔案並提交提取請求(PR)。 在依照這裡指示的步驟進行之前，請務必閱讀[在Adobe Experience Platform目的地中記錄您的目的地](./documentation-instructions.md)。

>[!TIP]
>
>另請參閱Adobe貢獻者指南中的支援檔案：
>* [安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [在本機設定檔案的Git存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [重大變更的GitHub貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)。

## 連線至GitHub並設定您的本機編寫環境 {#set-up-environment}

1. 在您的瀏覽器中，瀏覽至`https://github.com/AdobeDocs/experience-platform.en`
2. 若要[分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository)存放庫，請按一下&#x200B;**分支**，如下所示。 這會在您自己的GitHub帳戶中建立Experience Platform存放庫的復本。

   ![取用Adobe檔案存放庫](../assets/docs-framework/ssd-fork-repository.gif)

3. 將存放庫複製到本機電腦。 選取「**程式碼> HTTPS >使用GitHub Desktop**&#x200B;開啟」，如下所示。 確定您已安裝[GitHub Desktop](https://desktop.github.com/)。 如需進一步參考，請參閱Adobe貢獻者指南中的[建立存放庫的本機複製](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository)。

   ![將Adobe檔案存放庫複製到本機環境](../assets/docs-framework/clone-local.png)

4. 在您的本機檔案結構中，導覽至`experience-platform.en/help/destinations/catalog/[...]`，其中`[...]`是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取「`personalization`」資料夾。

## 為您的目的地編寫檔案頁面 {#author-documentation}

1. 您的檔案頁面是以[自助服務目的地範本](../docs-framework/self-service-template.md)為基礎。 下載[目的地範本](../assets/docs-framework/yourdestination-template.zip)。 解壓縮檔案`yourdestination-template.md`，並將檔案解壓縮至上述步驟4提及的目錄。  重新命名檔案`YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目的地名稱。 例如，如果您的公司名為Moviestar，您可將您的檔案命名為`moviestar.md`。
2. 使用您選擇的[文字編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors)開啟新檔案。 Adobe建議您使用[Visual Studio Code](https://code.visualstudio.com/)並安裝Adobe Markdown Authoring擴充功能。 若要安裝擴充功能，請開啟Visual Studio Code，選取畫面左側的&#x200B;**[!DNL Extensions]**&#x200B;索引標籤，然後搜尋`adobe markdown authoring`。 選取擴充功能並按一下&#x200B;**[!DNL Install]**。
   ![安裝Adobe Markdown Authoring擴充功能](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. 使用目的地的相關資訊編輯範本。 請依照範本中的指示操作。
4. 對於您打算新增至檔案的任何熒幕擷取畫面或影像，請移至`GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`，其中`[...]`是您想要的目的地類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取「`personalization`」資料夾。 為您的目的地建立新資料夾，並將影像儲存於此處。 您必須從正在編寫的頁面連結至這些專案。 請參閱[如何連結至影像的說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images)。
5. 準備就緒後，儲存您正在處理的檔案。

## 提交您的檔案以供檢閱 {#submit-review}

>[!TIP]
>
>請注意，您無法在此處中斷任何內容。 依照本節的指示，您只是建議更新說明檔案。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 在GitHub Desktop中，為您的更新建立工作分支，並選取&#x200B;**發佈分支**&#x200B;以將分支發佈至GitHub。

![新增本機分支](../assets/docs-framework/new-branch-local.gif)

1. 在GitHub Desktop中，[認可](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit)您的工作，如下所示。

   ![認可本機](../assets/docs-framework/commit-local.png)

1. 在GitHub Desktop中，[將您的工作](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push)推送到[遠端](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote)分支，如下所示。

   ![推送您的認可](../assets/docs-framework/push-local-to-remote.png)

1. 在GitHub網頁介面中，開啟提取請求(PR)，將您的工作分支合併至Adobe檔案存放庫的主分支。 確定已選取您處理的分支，並選取&#x200B;**Contribute >開啟提取請求**。

   ![建立提取請求](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 請確定基礎分支和比較分支正確無誤。 將說明您更新的附註新增至PR，並選取&#x200B;**建立提取請求**。 這會開啟PR，將復本的工作分支合併至Adobe存放庫的主分支。

   >[!TIP]
   >
   >保留&#x200B;**允許維護者編輯**&#x200B;核取方塊為已選取狀態，讓Adobe檔案團隊可以編輯PR。

   ![建立對Adobe檔案存放庫的提取請求](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 此時，系統會顯示通知，提示您簽署Adobe貢獻者授權合約(CLA)。 此為必要步驟。 簽署CLA後，請重新整理PR頁面並提交提取請求。

1. 您可以檢查`https://github.com/AdobeDocs/experience-platform.en`中的&#x200B;**提取請求**&#x200B;索引標籤，以確認提取請求已提交。

![PR成功](../assets/docs-framework/ssd-pr-successful.png)

1. 感謝支持！Adobe檔案團隊會聯絡PR，以備需要編輯檔案時使用，並通知您檔案何時發佈。

>[!TIP]
>
>若要新增影像和連結至您的檔案，以及有關Markdown的其他問題，請閱讀Adobe合作撰寫指南中的[使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)。
