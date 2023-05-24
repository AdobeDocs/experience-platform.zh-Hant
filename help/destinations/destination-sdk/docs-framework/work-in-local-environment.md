---
title: 使用本地環境中的文本編輯器建立目標文檔頁
description: 本頁上的說明顯示了如何使用文本編輯器在本地環境中工作，為Experience Platform目標建立文檔頁並提交以供審閱。
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# 使用本地環境中的文本編輯器建立目標文檔頁 {#local-authoring}

此頁上的說明說明了如何使用文本編輯器在本地環境中工作來編寫文檔並提交拉入請求(PR)。 在完成此處指定的步驟之前，請確保您已閱讀 [在Adobe Experience Platform目標中記錄目標](./documentation-instructions.md)。

>[!TIP]
>
>另請參閱《Adobe貢獻者指南》中的支援文檔：
>* [安裝Git和Markdown創作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本機設定供文件使用的 Git 存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [適用於重大變更的 GitHub 貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 連接到GitHub並設定本地創作環境 {#set-up-environment}

1. 在瀏覽器中，導航到 `https://github.com/AdobeDocs/experience-platform.en`
2. 至 [叉](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 儲存庫，按一下 **叉** 如下所示。 這將在您自己的GitHub帳戶中建立Experience Platform儲存庫的副本。

   ![分叉Adobe文檔儲存庫](../assets/docs-framework/ssd-fork-repository.gif)

3. 將存放庫複製到本機電腦. 選擇 **代碼> HTTPS >使用GitHub案頭開啟**，如下所示。 確保你 [GitHub案頭](https://desktop.github.com/) 已安裝。 請閱讀 [建立儲存庫的本地克隆](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) Adobe貢獻者指南。

   ![將Adobe文檔儲存庫克隆到本地環境](../assets/docs-framework/clone-local.png)

4. 在本地檔案結構中，導航到 `experience-platform.en/help/destinations/catalog/[...]`，也請參見Wiki頁。 `[...]` 是目標的所需類別。 例如，如果要將個性化目標添加到Experience Platform，請選擇 `personalization` 的子菜單。

## 為目標建立文檔頁面 {#author-documentation}

1. 文檔頁面基於 [自服務目標模板](../docs-framework/self-service-template.md)。 下載 [目標模板](../assets/docs-framework/yourdestination-template.zip)。 解壓並解壓檔案 `yourdestination-template.md` 到上面步驟4中提到的目錄。  更名檔案 `YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform的目標名稱。 例如，如果您的公司叫做Moviestar，您會將檔案命名為 `moviestar.md`。
2. 在 [文本編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors)。 Adobe建議您使用 [Visual Studio代碼](https://code.visualstudio.com/) 並安裝AdobeMarkdown Authoring擴展。 要安裝擴展，請開啟Visual Studio代碼，選擇 **[!DNL Extensions]** 頁籤，然後搜索 `adobe markdown authoring`。 選擇副檔名並按一下 **[!DNL Install]**。
   ![安裝AdobeMarkdown創作擴展](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. 編輯模板，其中包含目標的相關資訊。 按照模板中的說明操作。
4. 有關計畫添加到文檔的任何螢幕截圖或影像，請轉至 `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`，也請參見Wiki頁。 `[...]` 是目標的所需類別。 例如，如果要將個性化目標添加到Experience Platform，請選擇 `personalization` 的子菜單。 為目標建立新資料夾並將映像保存到此處。 必須從您正在創作的頁面連結到它們。 請參閱 [說明如何連結到影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images)。
5. 準備好後，保存正在處理的檔案。

## 提交文檔以供審閱 {#submit-review}

>[!TIP]
>
>注意，這裡沒有你能破的。 按照本節中的說明，您只是建議進行文檔更新。 您建議的更新將由Adobe Experience Platform文檔小組批准或編輯。

1. 在GitHub案頭中，為更新建立工作分支並選擇 **發佈分支** 將分支發佈到GitHub。

![本地新分支](../assets/docs-framework/new-branch-local.gif)

1. 在GitHub案頭中， [提交](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) 如下所示。

   ![提交本地](../assets/docs-framework/commit-local.png)

1. 在GitHub案頭中， [推](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) 你的工作 [遠程](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) 分支，如下所示。

   ![推送您的提交](../assets/docs-framework/push-local-to-remote.png)

1. 在GitHub Web介面中，開啟拉入請求(PR)，將工作分支合併到Adobe文檔儲存庫的主分支中。 確保已選擇您所處理的分支並選擇 **Contribute >開啟拉式請求**。

   ![建立拉入請求](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 確保基分支和比較分支正確。 向PR添加註釋，描述更新，然後選擇 **建立拉入請求**。 這將開啟一個PR，將叉的工作分支合併到Adobe儲存庫的主分支中。
   >[!TIP]
   >
   >離開 **允許維護人員編輯** 複選框，以便Adobe文檔團隊可以編輯PR。

   ![建立拉入請求以Adobe文檔儲存庫](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 此時，將出現一條通知，提示您簽署Adobe參與者許可協定(CLA)。 這是必須的步驟。 簽署CLA後，刷新PR頁並提交拉入請求。

1. 您可以通過檢查 **拉取請求** 頁籤 `https://github.com/AdobeDocs/experience-platform.en`。

![PR成功](../assets/docs-framework/ssd-pr-successful.png)

1. 感謝支持！Adobe文檔團隊將在需要進行任何編輯時在PR中聯繫，並告知您文檔將在何時發佈。

>[!TIP]
>
>要向文檔添加影像和連結，以及有關Markdown的任何其他問題，請閱讀 [使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) 在Adobe的合作寫作指南中。
