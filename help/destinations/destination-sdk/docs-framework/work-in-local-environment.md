---
title: 在本機環境中使用文字編輯器來建立目的地檔案頁面
description: 本頁的說明會示範如何使用文字編輯器在本機環境中運作，為您的Experience Platform目的地製作檔案頁面並提交以供審核。
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 83539a9aa2fddcae0c9a44302d8bfa9d9f56de0c
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---

# 在本機環境中使用文字編輯器來建立目的地檔案頁面 {#local-authoring}

本頁的指示會示範如何使用文字編輯器，在您的本機環境中運作，以編寫檔案並提交提取請求(PR)。 在執行此處指示的步驟之前，請務必閱讀[Adobe Experience Platform目的地的檔案](./documentation-instructions.md)。

>[!TIP]
>
>另請參閱Adobe貢獻者指南中的支援檔案：
>* [安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本機設定供文件使用的 Git 存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [適用於重大變更的 GitHub 貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 連線至GitHub並設定本機製作環境 {#set-up-environment}

1. 在您的瀏覽器中，導覽至`https://github.com/AdobeDocs/experience-platform.en`
2. 若要取用存放庫[fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository)，請按一下&#x200B;**Fork** ，如螢幕擷取所示。

   ![分支Adobe檔案存放庫](./assets/ssd-fork-repository.gif)

3. 將存放庫複製到本機電腦. 選取「**代碼> HTTPS >使用GitHub Desktop**&#x200B;開啟」，如下所示。 請確定您已安裝[GitHub Desktop](https://desktop.github.com/)。 如需進一步參考，請參閱Adobe貢獻者指南中的[建立存放庫的本機複製](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) 。

   ![將Adobe檔案存放庫複製至本機環境](./assets/clone-local.png)

4. 在您的本機檔案結構中，導覽至`experience-platform.en/help/destinations/catalog/[...]`，其中`[...]`是目的地的所需類別。 例如，如果您要新增個人化目標以Experience Platform，請選取`personalization`資料夾。

## 編寫您目的地的檔案頁面 {#author-documentation}

1. 您的檔案頁面是以[自助服務目的地範本](./self-service-template.md)為基礎。 下載[目標範本](assets/yourdestination-template.zip)。 將其解壓縮，並將檔案`yourdestination-template.md`解壓縮至上述步驟4中提及的目錄。  重新命名檔案`YOURDESTINATION.md`，其中YOURDESTINATION是Adobe Experience Platform中目的地的名稱。 例如，如果貴公司稱為Moviestar，您可將檔案命名為`moviestar.md`。
2. 在選擇的[文本編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors)中開啟新檔案。 Adobe建議您使用[Visual Studio Code](https://code.visualstudio.com/)並安裝AdobeMarkdown Authoring擴充功能。 若要安裝擴充功能，請開啟Visual Studio Code，選取畫面左側的&#x200B;**[!DNL Extensions]**&#x200B;標籤，然後搜尋`adobe markdown authoring`。 選取擴充功能，然後按一下&#x200B;**[!DNL Install]**。
   ![安裝AdobeMarkdown編寫擴充功能](./assets/install-adobe-markdown-extension.gif)
3. 編輯範本並附上目的地的相關資訊。 遵循範本中的指示。
4. 對於您打算添加到文檔的任何螢幕截圖或影像，請轉至`GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`，其中`[...]`是目標的所需類別。 例如，如果您要新增個人化目標以Experience Platform，請選取`personalization`資料夾。 為目的地建立新資料夾，並將影像儲存在此處。 您必須從編寫的頁面連結至這些頁面。 請參閱[指示如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images)。
5. 準備就緒後，儲存您正在使用的檔案。

## 提交您的檔案以供審核 {#submit-review}

>[!TIP]
>
>請注意，這裡沒有什麼可以打破的。 依照本節中的指示，您只是建議進行檔案更新。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 在GitHub Desktop中，為您的更新建立工作分支，並選取&#x200B;**發佈分支**&#x200B;以將分支發佈至GitHub。

![本地新建分支](./assets/new-branch-local.gif)

1. 在GitHub Desktop中，[commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit)您的工作，如下所示。

   ![提交本地](./assets/commit-local.png)

1. 在GitHub Desktop中，將您的作品推送至[remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote)分支，如下所示。[](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push)

   ![推送您的提交](./assets/push-local-to-remote.png)

1. 在GitHub網頁介面中，開啟提取請求(PR)，將您的工作分支合併至Adobe檔案存放庫的主分支。 請確定已選取您所使用的分支，並選取&#x200B;**提取請求**。

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
