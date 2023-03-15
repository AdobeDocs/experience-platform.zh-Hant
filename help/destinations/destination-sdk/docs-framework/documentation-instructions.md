---
title: 在Adobe Experience Platform中記錄您的目的地
description: 在Adobe Experience Platform中為目的地建立檔案頁面的逐步指示
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: dd4a150351b5e0c41586cf663324aeb345a896e4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 在Adobe Experience Platform中記錄您的目的地

>[!IMPORTANT]
>
>此處記錄的流程僅對提交產品化（公開）目的地的合作夥伴是必需的。 如果您要建立私人目的地供自己使用，則不需要為目的地建立和發佈檔案。

## 總覽 {#overview}

歡迎來到Adobe Experience Platform，真高興有你來！
記錄目的地是在Adobe Experience Platform中即時設定目的地的最後一步。

本檔案章節包含：

* 逐步指示您為新目的地建立檔案頁面；
* 可供您填寫目的地的範本；
* [使用Markdown的一般指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [AdobeMarkdown風味的特定指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (AdobeMarkdown的味道與一般Markdown非常類似)。
* A [最佳實務頁面](./authoring-best-practices.md) 可協助您為目的地頁面製作檔案頁面，且頁面符合Experience Platform檔案品質標準。

## 先決條件 {#prerequisites}

若要根據本文的指示建立目的地的檔案，需要下列項目：

* **GitHub帳戶**. 註冊 [GitHub](https://github.com/) 如果你還沒有帳戶。
* **GitHub案頭版**. 如果您選擇 [在本機環境中建立檔案](./work-in-local-environment.md)，您必須使用 [GitHub案頭版](https://desktop.github.com/).
* 您與Adobe的整合必須處於測試階段，且目的地已部署在Adobe Experience Platform的中繼環境中。

## 在Adobe Experience Platform中建立目的地檔案的高階指示 {#high-level-instructions}

從高層面來說，若要建立目的地的檔案，您必須 [建立分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) Adobe Experience Platform檔案存放庫，並編輯 [提供的檔案範本](./self-service-template.md) 在新分支里。 使用Adobe提供的範本建立新的目的地頁面。 準備就緒時，請開啟提取請求(PR)。 下文將進一步說明執行此操作： [建立新目的地頁面的步驟](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 檔案範本 {#documentation-template}

為協助您建立檔案頁面，Adobe已預填 [檔案範本](./self-service-template.md) 為了你。 在下方，您可以找到如何編輯範本和開啟提取請求的指示。 Adobe檔案團隊將檢閱並發佈您新目的地的檔案。

[在此處下載範本](assets/yourdestination-template.zip) 並將檔案解壓縮以解壓縮 `yourdestination.md` 檔案。

下文將詳細說明如何使用範本建立檔案頁面。

## 建立新目的地頁面的步驟 {#steps-to-create-docs-page}

您可以使用GitHub網頁介面或本機環境，在Adobe Experience Platform中建立新目的地的檔案。 請在以下連結中找到兩個選項的指示：

* [使用GitHub網頁介面建立目的地檔案頁面](./use-github-interface-to-create-documentation.md)
* [在本機環境中使用文字編輯器來建立目的地檔案頁面](./work-in-local-environment.md)

## 最佳做法 {#best-practices}

檢閱 [編寫最佳實務](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) 建立目的地檔案頁面之前和期間。 也請務必閱讀 [Adobe檔案撰寫指引](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) Adobe檔案團隊在編寫檔案時會使用的更多撰寫秘訣。