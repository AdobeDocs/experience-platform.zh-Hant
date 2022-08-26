---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
solution: Experience Platform
title: 使用本地環境中的文本編輯器建立源文檔頁
topic-legacy: tutorial
description: 本文檔提供了有關如何使用本地環境為來源編寫文檔並提交拉入請求(PR)的步驟。
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: adf7dbe5e32310fee680f996ffbde0fd6ddd993a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 使用本地環境中的文本編輯器建立源文檔頁

本文檔提供了有關如何使用本地環境為來源編寫文檔並提交拉入請求(PR)的步驟。

>[!TIP]
>
>以下來自Adobe幫助指南的文檔可用於進一步支援您的文檔流程： <ul><li>[安裝Git和Markdown創作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本機設定供文件使用的 Git 存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[適用於重大變更的 GitHub 貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 先決條件

以下教程要求您在本地電腦上安裝了GitHub Desktop。 如果沒有GitHub Desktop，則可以下載應用程式 [這裡](https://desktop.github.com/)。

## 連接到GitHub並設定本地創作環境

設定本地創作環境的第一步是導航到 [Adobe Experience PlatformGitHub儲存庫](https://github.com/AdobeDocs/experience-platform.en)。

![平台回購](../assets/platform-repo.png)

在Platform GitHub儲存庫的首頁上，選擇 **叉**。

![分叉](../assets/fork.png)

要將儲存庫克隆到本地電腦，請選擇 **代碼**。 從顯示的下拉菜單中，選擇 **HTTPS** ，然後選擇 **使用GitHub案頭開啟**。

>[!TIP]
>
>有關詳細資訊，請參見上的教程 [在本地設定Git儲存庫以獲取文檔](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository)。

![開放git — 案頭](../assets/open-git-desktop.png)

接下來，讓GitHub Desktop Clone `experience-platform.en` 儲存庫。

![克隆](../assets/cloning.png)

克隆過程完成後，請轉至GitHub Desktop以建立新分支。 選擇 **母版** 從頂部導航中，然後選擇 **新建分支**

![新分支](../assets/new-branch.png)

在出現的跨距面板中，輸入分支的描述性名稱，然後選擇 **建立分支**。

![建立分支v](../assets/create-branch-vs.png)

下一步，選擇 **發佈分支**。

![發佈分支](../assets/publish-branch.png)

## 為來源編寫文檔頁面

通過將儲存庫克隆到本地電腦並建立新分支，您現在可以通過 [所選文本編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors)。

Adobe建議您使用 [Visual Studio代碼](https://code.visualstudio.com/) 並安裝AdobeMarkdown創作擴展。 要安裝擴展，請啟動Visual Studio代碼，然後選擇 **擴展** 的子菜單。

![擴充功能](../assets/extension.png)

下一步，輸入 `Adobe Markdown Authoring` 到搜索欄，然後選擇 **安裝** 的子菜單。

![安裝](../assets/install.png)

當您的本地電腦準備就緒時，下載 [源文檔模板](../assets/api-template.zip) 將檔案解壓到 `experience-platform.en/help/sources/tutorials/api/create/...` 與 [`...`] 代表您選擇的類別。 例如，如果要建立資料庫源，請選擇資料庫資料夾。

最後，按照模板上概述的說明編輯模板，並提供與源相關的相關資訊。

![編輯模板](../assets/edit-template.png)

## 提交文檔以供審閱

要建立拉入請求(PR)並提交文檔以供審閱，請首先將您的工作保存到 [!DNL Visual Studio Code] （或您選擇的文本編輯器）。 接下來，使用GitHub Desktop，輸入提交消息並選擇 **提交到create-source-documentation**。

![提交與](../assets/commit-vs.png)

下一步，選擇 **推式原點** 將您的工作上載到遠程分支。

![推式原點](../assets/push-origin.png)

要建立拉式請求，請選擇 **建立拉入請求**。

![建立 — prv](../assets/create-pr-vs.png)

確保基本分支和比較分支正確。 向PR添加註釋，描述更新，然後選擇 **建立拉入請求**。 這將開啟一個PR，將工作的工作分支合併到Adobe儲存庫的主分支中。

>[!TIP]
>
>離開 **允許維護人員編輯** 複選框，以確保Adobe文檔團隊可以編輯PR。

![建立pr](../assets/create-pr.png)

您可以通過檢查https://github.com/AdobeDocs/experience-platform.en中的拉請求頁籤來確認已提交拉請求。

![確認 — pr](../assets/confirm-pr.png)
