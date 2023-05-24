---
title: 記錄您在Adobe Experience Platform的目標
description: 逐步說明，以便您在Adobe Experience Platform為目標建立文檔頁面
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 記錄您在Adobe Experience Platform的目標

>[!IMPORTANT]
>
>此處記錄的流程僅對提交已生產化（公共）目標的合作夥伴是必需的。 如果您正在建立專用目標供自己使用，則無需為目標建立和發佈文檔。

## 總覽 {#overview}

歡迎來到Adobe Experience Platform，很高興能來！
記錄目標是在Adobe Experience Platform直播之前的最後一步。

本文檔部分包括：

* 逐步說明，以便您為新目標建立文檔頁面；
* 一個模板，供您填寫目標；
* [有關使用Markdown的一般說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [AdobeMarkdown風味的具體說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (AdobeMarkdown的味道與普通Markdown非常相似)。
* A [最佳做法頁](./authoring-best-practices.md) 幫助您為目標頁面建立文檔頁面，該頁面符合Experience Platform文檔質量標準。

## 先決條件 {#prerequisites}

要根據本文中的說明為目標建立文檔，需要以下各項：

* **GitHub帳戶**。 註冊 [GitHub](https://github.com/) 你還沒有帳戶。
* **GitHub案頭**。 如果選擇 [在本地環境中建立文檔](./work-in-local-environment.md)，必須使用 [GitHub案頭](https://desktop.github.com/)。
* 您與Adobe的整合必須處於測試階段，目標部署在Adobe Experience Platform的過渡環境中。

## 為您在Adobe Experience Platform的目標建立文檔的高級說明 {#high-level-instructions}

在較高級別，要為目標建立文檔，您需要 [建立叉](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 並編輯 [提供的文檔模板](./self-service-template.md) 新的分支。 使用Adobe提供的模板建立新的目標頁。 準備好後開啟拉入請求(PR)。 下面將進一步介紹執行此操作的說明， [建立新目標頁的步驟](./documentation-instructions.md#steps-to-create-docs-page)。

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 文檔模板 {#documentation-template}

為幫助您建立文檔頁面，Adobe已預填 [文檔模板](./self-service-template.md) 為你。 在下面，您可以找到如何編輯模板和開啟拉入請求的說明。 Adobe文檔團隊將審閱並發佈新目標的文檔。

[在此處下載模板](../assets/docs-framework/yourdestination-template.zip) 解壓縮檔案以解壓 `yourdestination.md` 的子菜單。

有關使用模板建立文檔頁面的說明如下。

## 建立新目標頁的步驟 {#steps-to-create-docs-page}

您可以使用GitHub Web介面或本地環境為新目標在Adobe Experience Platform建立文檔。 在以下連結中查找兩個選項的說明：

* [使用GitHub Web介面建立目標文檔頁](./use-github-interface-to-create-documentation.md)
* [使用本地環境中的文本編輯器建立目標文檔頁](./work-in-local-environment.md)

## 最佳做法 {#best-practices}

查看 [編寫最佳實踐](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) 建立目標文檔頁面之前和期間。 確保同時閱讀 [編寫Adobe文檔指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 有關Adobe文檔團隊在創作文檔時使用的一些更多書寫提示。