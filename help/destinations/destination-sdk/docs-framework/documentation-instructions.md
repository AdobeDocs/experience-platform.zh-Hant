---
title: 在Adobe Experience Platform中記錄您的目的地
description: 協助您在Adobe Experience Platform中為目的地建立檔案頁面的逐步指示
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 在Adobe Experience Platform中記錄您的目的地

>[!IMPORTANT]
>
>此處記錄的程式僅適用於提交生產（公用）目的地的合作夥伴。 如果您要建立供您自用的私人目的地，則不需要建立和發佈目的地的檔案。

## 概觀 {#overview}

歡迎使用Adobe Experience Platform，很高興在這裡見到您！
記錄您的目的地是可在Adobe Experience Platform中即時設定之前的最後一步。

本檔案區段包含：

* 逐步指示讓您為新目的地建立檔案頁面；
* 範本供您填寫目的地；
* [使用Markdown的一般指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)；
* [AdobeMarkdown風格的特定指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (AdobeMarkdown風格與一般Markdown非常類似)。
* [最佳實務頁面](./authoring-best-practices.md)可協助您為目的地頁面撰寫符合Experience Platform檔案品質標準的檔案頁面。

## 先決條件 {#prerequisites}

若要根據本文的指示建立目的地的檔案，需有下列專案：

* **GitHub帳戶**。 如果您還沒有帳戶，請註冊[GitHub](https://github.com/)。
* **GitHub案頭**。 如果您選擇在您的本機環境中[建立檔案](./work-in-local-environment.md)，則必須使用[GitHub Desktop](https://desktop.github.com/)。
* 您與Adobe的整合必須處於測試階段，且您的目的地部署在Adobe Experience Platform中的中繼環境。

## 在Adobe Experience Platform中建立目的地檔案的高層級指示 {#high-level-instructions}

整體而言，若要為目的地建立檔案，您需要[建立Adobe Experience Platform檔案存放庫的分叉](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository)，並在新分支中編輯[提供的檔案範本](./self-service-template.md)。 使用Adobe提供的範本來建立新的目的地頁面。 準備就緒後，開啟提取請求(PR)。 下面是建立新目的地頁面的[步驟中的進一步指示](./documentation-instructions.md#steps-to-create-docs-page)。

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 檔案範本 {#documentation-template}

為協助您建立說明檔案頁面，Adobe已為您預先填入[說明檔案範本](./self-service-template.md)。 您可以在下方找到如何編輯範本及開啟提取請求的指示。 Adobe檔案團隊將檢閱並發佈您新目的地的檔案。

[在此下載範本](../assets/docs-framework/yourdestination-template.zip)並解壓縮檔案以解壓縮`yourdestination.md`檔案。

下面是使用範本建立檔案頁面的說明。

## 建立新目的地頁面的步驟 {#steps-to-create-docs-page}

您可以使用GitHub網頁介面或本機環境，在Adobe Experience Platform中建立新目的地的檔案。 請在下列連結中找到這兩個選項的指示：

* [使用GitHub網頁介面建立目的地檔案頁面](./use-github-interface-to-create-documentation.md)
* [在本機環境中使用文字編輯器建立目的地檔案頁面](./work-in-local-environment.md)

## 最佳作法 {#best-practices}

在建立目的地檔案頁面之前和期間，請檢閱[撰寫最佳實務](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md)。 也請務必閱讀Adobe檔案的[撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html)，以取得Adobe檔案團隊在撰寫檔案時所使用的更多撰寫提示。