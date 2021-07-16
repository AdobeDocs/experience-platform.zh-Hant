---
title: 上傳並實作擴充功能的端對端測試
description: 了解如何在Adobe Experience Platform中驗證、上傳和測試您的擴充功能。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 33%

---

# 上傳並實作端對端測試

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

若要在Adobe Experience Platform中測試標籤擴充功能，請使用標籤API和/或命令列工具來上傳您的擴充功能套件。 接下來，使用資料收集UI將您的擴充功能套件安裝至屬性，並在標籤程式庫和組建中執行其功能。

本檔案說明如何針對擴充功能實作端對端測試。

>[!NOTE]
>
>本指南假設您使用MacOS搭配Node.js和已安裝且可用的npm。

## 驗證您的擴充功能 {#validate}

如果您的團隊對擴充功能的效能和展現於[沙箱](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox)工具中的結果感到滿意，您就可以將擴充功能套件上傳至標籤。

上傳之前，請先驗證是否有任何必要欄位或設定需完成。例如，檢閱[擴充功能資訊清單](../manifest.md)、[擴充功能組態](../configuration.md)、[檢視](../web/views.md)和[程式庫模組](../web/format.md)（至少），都是不錯的作法。

您的標誌檔案就是明確的範例：請在 `"iconPath": "example.svg",` 檔案中加上 `extension.json` 這一行，並將標誌影像檔案納入您的專案中。這是將針對擴充功能顯示之圖示的相對路徑。 此路徑不應以斜線開頭。它必須參考副檔名為 `.svg` 的 SVG 檔案。SVG在呈現為正方形時應正常顯示，並可由使用者介面調整。 如需詳細資訊，請參閱[如何縮放SVG文章](https://css-tricks.com/scale-svg/) 。

>[!NOTE]
>
>針對公開擴充功能，請在您的 `extension.json` 中納入並附有 Exchange 清單連結的項目。您的[擴充功能資訊清單](../manifest.md)應包含 `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"` 之類的項目，指向您 Exchange 清單的 URL。

## 建立 Adobe I/O 整合 {#integration}

若要使用API或命令列工具，您需要具有Adobe I/O的技術帳戶。您必須在I/O主控台中建立技術帳戶，然後使用上傳程式工具來上傳擴充功能套件。

如需建立技術帳戶以在Adobe Experience Platform中與標籤搭配使用的資訊，請參閱[存取Token](https://developer.adobelaunch.com/api/guides/access_tokens/)指南。

>[!IMPORTANT]
>
>若要在 Adobe I/O 中建立整合，您必須是 Experience Cloud 組織管理員或 Experience Cloud 組織開發人員。

如果您無法建立整合，表示您可能沒有正確的權限。 這需要組織管理員為您完成步驟，或將您指派為開發人員。

## 上傳您的擴充功能套件 {#upload}

現在您已取得認證，即可端對端測試擴充功能套件。

第一次上傳擴充功能套件時，套件會進入 `development` 狀態。這表示它只會顯示給您自己的組織，而且只會顯示已標示為要進行擴充功能的屬性。

使用命令列在包含.zip套件的目錄內執行下列命令。

```bash
npx @adobe/reactor-uploader
```

`npx` 可讓您下載並直接執行 npm 套件，而無需在機器上實際安裝。這是上傳程式最簡單的執行方式。

上傳程式會要求您輸入數個資訊。 技術帳戶ID、API金鑰和其他資訊位可從Adobe I/O主控台擷取。 導覽至 I/O 主控台中的[整合頁面](https://console.adobe.io/tw/integrations)。從下拉式清單中選取正確的組織，尋找正確的整合，然後選取&#x200B;**[!UICONTROL 檢視]**。

- 您的私密金鑰路徑為何？/path/to/private.key。這是您先前在步驟 2 中儲存私密金鑰的位置。
- 您的組織 ID 為何？請從您先前開啟的I/O主控台概觀頁面複製並貼上此檔案。
- 您的技術帳戶 ID 為何？從I/O主控台複製並貼上此檔案。
- 您的 API 金鑰為何？從I/O主控台複製並貼上此檔案。
- 用戶端密碼為何？ 從I/O主控台複製並貼上此檔案。
- 您要上傳的 extension_package 的路徑為何？/path/to/extension_package.zip。如果從包含 .zip 套件的目錄中叫用上傳程式，您可以直接從清單中選取，而無需輸入路徑。

您的擴充功能套件將隨即上傳，且上傳程式會為您提供 extension_package 的 ID。

>[!NOTE]
>
>上傳或修補時，系統以非同步的方式擷取及部署擴充功能套件期間，該套件會進入擱置狀態。在進行此程式時，您可以使用API和資料收集UI輪詢`extension_package` ID的狀態。 您會在目錄中看到標示為「擱置中」的擴充功能卡片。

>[!NOTE]
>
>如果您打算經常執行上傳程式，則每次都輸入這些資訊可能會造成負擔。 您也可以從命令列將這些參數傳入。 如需詳細資訊，請查看 NPM 文件的[命令列引數](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments)一節。

## 建立開發屬性 {#property}

登入資料收集UI後，屬性畫面會隨即顯示。 屬性是一個容器，內含您要部署的標記，可用於一或多個網站。

![](../images/getting-started/properties-screen.png)

第一次登入時，畫面上不會顯示任何屬性。 選取&#x200B;**「新增屬性」**&#x200B;以建立屬性。輸入名稱和 URL。使用測試網站的URL，或您將在其中測試擴充功能的頁面。 此網域欄位可供某些擴充功能使用，或供使用核心擴充功能的條件使用。

>[!NOTE]
>
>`localhost` 將無法作為URL值運作。如果您使用`localhost` URL，請改為使用任何模擬值進行測試。 例如， example.com。

若要將此屬性用於擴充功能開發測試，您必須展開&#x200B;**進階OPTIONS**，並務必勾選&#x200B;**設定以進行擴充功能開發**&#x200B;的方塊。

![](../images/getting-started/launch-create-a-dev-property.png)

選取底部的&#x200B;**「儲存」**&#x200B;以儲存新屬性。

出現「Properties（屬性）」螢幕。 選取您剛建立的屬性名稱。「屬性概述」畫面隨即顯示。 它提供指向系統每個區域的連結，左側列中包含全局導航連結。

## 安裝您的擴充功能 {#install-extension}

若要在此屬性中安裝您的擴充功能，請在左欄的主導覽連結中選取&#x200B;**擴充功能**&#x200B;連結。 **Core**&#x200B;擴充功能顯示在&#x200B;**Installed**&#x200B;畫面上。 核心擴充功能包含資料收集中的所有標籤管理功能。

![](../images/getting-started/extensions.png)

若要新增擴充功能，請選取&#x200B;**Catalog**&#x200B;標籤。

![](../images/getting-started/catalog.png)

目錄會顯示每個可用擴充功能的卡片圖示。如果您的擴充功能未顯示在目錄中，請確定您已完成「Adobe管理控制台設定」和「建立您的擴充功能套件」區段中的上述步驟。 如果Platform尚未完成初始處理，您的擴充功能套件也可能會顯示為「擱置中」。

如果您已依照先前步驟操作，但目錄中仍未顯示「擱置中」或「失敗」擴充功能套件，則應直接使用API檢查擴充功能套件的狀態。 如需如何進行適當API呼叫的詳細資訊，請參閱API檔案中的[擷取ExtensionPackage](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/fetch/)。

在您的擴充功能套件完成處理後，選取卡片底部的&#x200B;**Install**。

![](../images/getting-started/install-extension.png)

設定畫面隨即開啟（若擴充功能有一個）。 新增設定擴充功能所需的任何資訊，然後選取底部的&#x200B;**「儲存」**。此處顯示的設定畫面範例使用Facebook擴充功能，其需有像素ID。

![](../images/getting-started/fb-extension.png)

您現在應該會看到&#x200B;**已安裝**&#x200B;擴充功能畫面，其中顯示核心擴充功能和您的擴充功能。

![](../images/getting-started/extension-installed.png)

## 建立用來測試擴充功能的資源 {#resources}

擴充功能為Adobe Experience Platform的使用者提供新功能。 這些項目通常會顯示在資料元素或規則產生器中。

### 資料元素

標籤資料元素的用途是協助使用者保留值。 每個資料元素都是來源資料的對應或指標。單一資料元素是可對應至查詢字串、URL、Cookie 值、JavaScript 變數的變數。從左側導航欄中選擇&#x200B;**資料元素**，然後選擇&#x200B;**建立新資料元素**。

![](../images/getting-started/data-element-create-new-link.png)

擴充功能可視需要定義資料元素類型，供擴充功能運作之用，或方便使用者操作\。當擴充功能提供資料元素類型時，這些類型會顯示在&#x200B;**建立資料元素**&#x200B;畫面上的下拉式清單中，供使用者使用：

![](../images/getting-started/create-data-element.png)

當使用者從&#x200B;**擴充功能**&#x200B;下拉式清單中選取您的擴充功能時，**資料元素類型**&#x200B;下拉式清單會填入您擴充功能提供的任何資料元素類型。 使用者可將每個資料元素對應至其來源值。然後，在「資料元素變更事件」或「自訂程式碼事件」中建立規則時，可使用資料元素來觸發要執行的規則。資料元素也可用於資料元素條件或規則中的其他條件、例外或動作。

建立資料元素 (設定對應) 後，使用者只需參考資料元素即可參考來源資料。如果值的來源有所變更 (網站重新設計等)，使用者只需在資料收集UI中更新一次對應，所有資料元素就會自動接收新的來源值。

### 規則

在左側導覽中選取&#x200B;**Rules**&#x200B;連結，然後選取&#x200B;**Create New Rule**。

![](../images/getting-started/rules-link.png)

首先，輸入規則的描述性名稱。 **建立規則**&#x200B;畫面的設定方式與`if-then`陳述式相同。

![](../images/getting-started/create-new-rule.png)

如果發生事件，且符合條件，而且沒有例外，則會觸發動作。擴充功能中也存在相同的流程，您可在其中建立或運用事件、條件、例外、資料元素或動作。

使用Facebook擴充功能範例，針對頁面在測試網站上載入的每次事件新增事件。

![](../images/getting-started/load-event.png)

`Window Loaded` **事件類型**&#x200B;可確保每當頁面載入測試網站時，就會觸發此規則。 選擇&#x200B;**保留更改**。 在此範例中，請忽略&#x200B;**條件**，因為應針對測試網站上的任何頁面觸發規則。

在&#x200B;**ACTIONS**&#x200B;下，選擇&#x200B;**Add**。 將出現&#x200B;**Action Configuration**&#x200B;螢幕。接下來，您必須選擇要應用規則的擴展以及觸發規則時要發生的操作。 從&#x200B;**Extension**&#x200B;下拉清單中選擇&#x200B;**Facebook Pixel**，從&#x200B;**Action Type**&#x200B;下拉清單中選擇&#x200B;**Send Page View**。 在以下&#x200B;**編輯規則**&#x200B;螢幕上選擇&#x200B;**保留更改**，然後選擇&#x200B;**保存**。

![](../images/getting-started/action-configuration.png)

測試擴充功能時，請選取任何相關事件、條件等。 任何數量的規則中提供的任何事件、條件等。

## 發佈您的變更 {#publish}

在主要導覽區中選取&#x200B;**「發佈」**，然後選取&#x200B;**「新增程式庫」**&#x200B;連結：

![](../images/getting-started/add-new-library.png)

程式庫是擴充功能、資料元素和規則部署後，彼此間以及與網站間將如何互動的一組指示。程式庫會編譯到組建中。一個程式庫可以包含使用者想一次進行或測試的所有變更，數量不限。

在&#x200B;**建立程式庫**&#x200B;畫面中，在&#x200B;**名稱**&#x200B;文字欄位中新增名稱。 標籤提供名為&#x200B;**Development**&#x200B;的預設開發環境。 從&#x200B;**Environment**&#x200B;下拉清單中選擇&#x200B;**Development**。 為簡單起見，請新增所有可用資源。 選擇&#x200B;**添加所有更改的資源**，然後選擇&#x200B;**保存**。

>[!NOTE]
>
>將資源新增至程式庫時，系統會建立該資源當下的快照，並新增至程式庫。若您之後變更資源 (例如因執行必要的修正作業而變更)，將必須同時更新程式庫，以納入資源的最新變更。為此，您也可以使用&#x200B;**「新增所有已變更的資源」**&#x200B;按鈕。

![](../images/getting-started/create-new-library.png)

現在，所有變更皆已納入新建立的程式庫（在提供的範例中命名為&#x200B;**dev**），請選取&#x200B;**儲存並建置至開發**。

![](../images/getting-started/build-for-dev.png)

建置程式完成後，程式庫名稱旁會顯示綠色的&#x200B;**success**&#x200B;指標。

![](../images/getting-started/successful-build.png)

標籤程式庫現在已發佈且可供使用。 測試頁面必須使用新建立的程式庫，才能測試瀏覽器中使用者的頁面行為。

## 在測試網站上安裝標籤 {#install-data-collection-tags}

「環境」索引標籤提供安裝指示。 此頁面會顯示所有可用的環境，也可讓您建立更多環境。 當程式庫發佈至開發環境時，請選取&#x200B;**Development**&#x200B;列上&#x200B;**INSTALL**&#x200B;欄中的方塊圖示。

![](../images/getting-started/launch-installation-instructions.png)

此時會顯示「開發」環境的「**Web安裝指示**」對話框。 選擇複製表徵圖以複製整個`<script>`標籤。

![](../images/getting-started/launch-installation-instructions-dialogue.png)

將此單個`<script>`標籤放在文檔或站點模板的`<head>`部分內，完成安裝。 接下來，請造訪測試網站，檢查已發佈標籤庫的行為。

## 測試 {#test}

以下是實用控制台命令清單，用於驗證您的測試頁或站點上的擴展。

- `_satellite.setDebug(true);` 會啟用除錯模式，並將有用的記錄陳述式輸出至主控台。
- `_satellite._container`物件包含有關已部署程式庫的有用資訊，包括有關組建、資料元素、規則和擴充功能的詳細資訊。

此測試的目標是檢查已部署程式庫的功能，並確保擴充功能套件在整合至程式庫後，會如預期般運作。

當您發現需要對擴充功能套件進行的變更時，其反覆運算程序與開發程序相類似。

1. 對您專案中的程式碼進行變更。
1. 使用沙箱工具驗證變更.
1. 使用封裝程式工具建立新的 .zip 套件
1. 使用上傳程式工具上傳新的.zip套件。 程式會依照與前次上傳相同的指示執行。 不過，您會發現，由於在開發模式中已有該名稱的擴充功能套件，因此這個新套件將會覆寫較舊的版本，而非建立新的套件。

   >[!NOTE]
   >
   >可以在命令行上傳遞參數，以避免重複輸入憑據以節省時間。 如需詳細資訊，請參閱[reactor-uploader檔案](https://www.npmjs.com/package/@adobe/reactor-uploader)。
1. 更新現有包時，可以跳過安裝步驟。
1. 修改資源 — 如果任何擴充功能元件的設定已變更，您需要在資料收集UI中更新這些資源。
1. 將您的最新變更新增至程式庫，然後重新建置.
1. 完成另一輪測試。

<!--
## Document {#document}

Your [exchange listing](./create-listing.md) is a great place for marketing and support information for your extension, but our tags [Help Docs](https://experienceleague.adobe.com/docs/launch/using/overview.html) are used every day by our customers. We encourage you to submit a pull request to [add your extension documentation](https://github.com/AdobeDocs/launch.en/blob/master/help/extension-reference/3rd-party-extensions.md) into the tags user docs. Open source docs for the win! 🚀
-->
