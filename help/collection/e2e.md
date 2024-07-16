---
title: 資料收集端對端總覽
description: 有關如何使用Adobe Experience Platform的資料收集功能將事件資料傳送至Adobe Experience Cloud解決方案的高層級概觀。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '2616'
ht-degree: 0%

---

# 資料收集端對端總覽

Adobe Experience Platform會收集您的資料並傳輸至其他Adobe產品和第三方目的地。 若要將事件資料從您的應用程式傳送至Experience PlatformEdge Network，請務必瞭解這些核心技術，以及如何設定這些技術，以在需要時將資料傳送至您所需的目的地。

本指南提供高階教學課程，說明如何使用Platform的資料收集功能，透過Edge Network傳送事件。 本教學課程會具體說明在資料收集UI (前身為Adobe Experience Platform Launch)中安裝和設定Adobe Experience Platform Web SDK標籤擴充功能的步驟。

>[!NOTE]
>
>如果您不想使用標籤，也可以選擇手動安裝及設定SDK，但周圍的步驟仍必須如以下所述完成。
>
>所有涉及資料收集UI的步驟也可在Experience Platform UI中執行。

## 先決條件

本教學課程使用資料收集UI來建立結構、設定資料串流及安裝Web SDK。 若要在UI中執行這些動作，您必須被授與至少一個Web屬性的存取權以及下列[屬性權利](../tags/ui/administration/user-permissions.md#property-rights)：

* 開發
* 管理擴充功能

請參閱[管理資料彙集](./permissions.md)的許可權指南，瞭解如何授予屬性和屬性許可權的存取權。

若要使用本指南中提到的各種資料收集產品，您也必須有權存取資料串流，並能夠建立和管理結構描述。 如果您需要存取其中任何一項功能，請聯絡您的Adobe帳戶團隊以協助您取得必要的存取權。 請注意，如果您尚未購買Adobe Experience Platform，Adobe會免費提供您使用SDK的必要存取權。

如果您已經擁有Platform的存取權，您必須確定您已啟用下列類別下的所有[許可權](../access-control/home.md#permissions)：

* 資料模型製作
* 身分

請參閱[存取控制UI總覽](../access-control/ui/overview.md)，瞭解如何將Platform功能的許可權授與使用者。

## 程式摘要

為您的網站設定資料收集的流程可概括如下：

1. [建立結構描述](#schema)，以決定資料傳送至Edge Network時的結構方式。
1. [建立資料流](#datastream)以設定要將您的資料傳送到哪些目的地。
1. [安裝並設定Web SDK](#sdk)，以便在您的網站上發生某些事件時，將資料傳送至資料流。

一旦您能夠將資料傳送至Edge Network，如果您組織擁有事件轉送的授權，您也可選擇性[設定事件轉送](#event-forwarding)。

## 建立結構描述 {#schema}

[Experience Data Model (XDM)](../xdm/home.md)是開放原始碼規格，以結構描述的形式提供資料的一般結構和定義。 換句話說，XDM是以可由Edge Network和其他Adobe Experience Cloud應用程式執行的方式建構和格式化您的資料的一種方式。

設定資料收集作業的第一步，是建立XDM結構描述來代表您的資料。 在本教學課程的稍後步驟中，您會將您要傳送的資料對應至此結構描述的結構。

>[!NOTE]
>
>XDM結構描述很容易自訂。 以下概述的步驟並非過度規範化，而是特別針對Web SDK的結構需求。 在這些引數之外，您可以任意定義資料的其他結構。

在UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**。 從這裡，您可以看到先前建立的、屬於您組織的結構描述清單。 若要繼續，請選取&#x200B;**[!UICONTROL 建立結構描述]**，然後從下拉式選單中選取&#x200B;**[!UICONTROL XDM ExperienceEvent]**。

![結構描述工作區](./images/e2e/schemas.png)

會出現一個對話方塊，提示您開始將欄位群組新增到結構描述。 若要使用Web SDK傳送事件，您必須新增欄位群組&#x200B;**[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**。 此欄位群組包含由Web SDK程式庫自動收集之資料屬性的定義。

使用搜尋列縮小清單的範圍，協助您更輕鬆地尋找此欄位群組。 找到後，請先從清單中選取它，再選取&#x200B;**[!UICONTROL 新增欄位群組]**。

![結構描述工作區](./images/e2e/add-field-group.png)

結構描述畫布隨即顯示，顯示XDM結構描述的樹狀結構，包括Web SDK欄位群組提供的欄位。

![綱要結構](./images/e2e/schema-structure.png)

選取樹狀結構中的根欄位以開啟右側邊欄中的&#x200B;**[!UICONTROL 結構描述屬性]**，您可以在其中提供結構描述的名稱和選擇性描述。

![命名結構描述](./images/e2e/name-schema.png)

如果您想要將更多欄位新增到結構描述中，您可以選取左側邊欄中&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下的&#x200B;**[!UICONTROL 新增]**&#x200B;來執行此操作。

![新增欄位群組](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>請參閱XDM檔案中有關[新增欄位群組](../xdm/ui/resources/schemas.md#add-field-groups)的指南，以取得有關如何搜尋不同欄位群組以符合您使用案例的詳細步驟。
>
>最佳實務是僅為您計畫透過Edge Network傳送的資料新增欄位。 將欄位新增到結構描述並儲存後，之後只能對結構描述進行附加變更。 如需詳細資訊，請參閱結構描述演化[規則](../xdm/schema/composition.md#evolution)的相關章節。

新增您需要的欄位後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存結構描述。

![儲存結構描述](./images/e2e/save-schema.png)

## 建立資料串流 {#datastream}

資料串流是一種設定，可告知Edge Network您希望將資料傳送到的位置。 具體而言，資料串流會指定您要將資料傳送至哪些Experience Cloud產品，以及您想要如何在每個產品中處理和儲存資料。

>[!NOTE]
>
>如果您想要使用[事件轉送](../tags/ui/event-forwarding/overview.md) （假設您的組織已獲得功能授權），您必須以啟用Adobe產品的相同方式，為資料流啟用它。 有關此程式的詳細資訊，請參閱[稍後的章節](#event-forwarding)。

在左側導覽中選取&#x200B;**[!UICONTROL 資料串流]**。 從這裡，您可以從清單中選取要編輯的現有資料流，或是選取&#x200B;**[!UICONTROL 新增資料流]**&#x200B;以建立新的設定。

![資料串流](./images/e2e/datastreams.png)

資料串流的設定需求取決於您要將資料傳送至哪些產品和功能。 如需每個產品組態選項的詳細資訊，請參閱[資料串流總覽](../datastreams/overview.md)。

## 安裝及設定Web SDK {#install}

建立方案和資料流後，下一步就是安裝和設定Platform Web SDK，以開始傳送資料給Edge Network。

>[!NOTE]
>
>本節使用資料收集UI來設定Web SDK標籤擴充功能，但您也可以改用原始程式碼來安裝和設定。 如需詳細資訊，請參閱下列指南：
>
>* [安裝SDK](/help/web-sdk/install/overview.md)
>* [設定SDK](/help/web-sdk/commands/configure/overview.md)
>
>另請注意，即使您只想使用事件轉送，您仍必須如所述安裝和設定SDK，才能在[稍後步驟](#event-forwarding)設定事件轉送。

此程式可彙總如下：

1. [在標籤屬性](#install-sdk)上安裝Adobe Experience Platform Web SDK以存取其功能。
1. [建立XDM物件資料元素](#data-element)，將您網站上的變數對應到您先前建立的XDM結構描述結構。
1. [建立規則](#rule)以告知SDK何時應將資料傳送至Edge Network。
1. [建置並安裝程式庫](#library)以在您的網站上實作規則。

### 在標籤屬性上安裝SDK {#install-sdk}

在左側導覽中選取&#x200B;**[!UICONTROL 標籤]**&#x200B;以顯示標籤屬性清單。 您可以視需要選擇現有屬性進行編輯，也可以改為選取&#x200B;**[!UICONTROL 新增屬性]**。

![屬性](./images/e2e/properties.png)

如果建立新屬性，請提供描述性名稱，並將[!UICONTROL 平台]設定為&#x200B;**[!UICONTROL Web]**。 提供Web屬性的完整網域，然後選取&#x200B;**[!UICONTROL 儲存]**。

![建立屬性](./images/e2e/create-property.png)

屬性的概述頁面隨即顯示。 從這裡，在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**。 尋找Platform Web SDK的清單（可選擇使用搜尋列來縮小結果範圍），並選取&#x200B;**[!UICONTROL 安裝]**。

![安裝Web SDK](./images/e2e/install-sdk.png)

SDK的設定頁面隨即顯示。 大部分必要值都會自動填入預設值，您可以視需要選擇變更。

![設定Web SDK](./images/e2e/configure-sdk.png)

不過，在安裝SDK之前，您必須選取資料流，讓資料流知道要將您的資料傳送至何處。 在&#x200B;**[!UICONTROL 資料串流]**&#x200B;底下，使用下拉式功能表選取您在[先前步驟](#datastream)設定的資料串流。 設定資料串流後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成將SDK安裝到屬性。

![設定資料流並儲存](./images/e2e/set-datastream.png)

### 建立XDM資料元素 {#data-element}

為了讓SDK將資料傳送至Edge Network，該資料必須對應至您在[先前步驟](#schema)中建立的XDM結構描述。 此對應可透過使用資料元素來完成。

在UI中，選取&#x200B;**[!UICONTROL 資料元素]**，然後選取&#x200B;**[!UICONTROL 建立新資料元素]**。

![建立新資料元素](./images/e2e/data-elements.png)

在下一個畫面中，選取[!UICONTROL 擴充功能]下拉式清單中的&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後為資料元素型別選取&#x200B;**[!UICONTROL XDM物件]**。

![XDM物件型別](./images/e2e/xdm-object.png)

隨即顯示XDM物件型別的組態對話方塊。 該對話方塊會自動選取您的Platform沙箱，從這裡您可以看到在該沙箱中建立的所有結構描述。 從清單中選取您先前建立的XDM結構描述。

![XDM物件型別](./images/e2e/select-schema.png)

結構描述的結構隨即顯示。 所有具有星號(**\***)的欄位都表示在觸發事件時自動填入的欄位。 對於所有其他欄位，您可以探索結構描述的結構並填寫其餘資料。

![將資料對應至XDM欄位](./images/e2e/map-schema.png)

>[!NOTE]
>
>上方的熒幕擷圖示範如何透過在[!UICONTROL 值]欄位中參照變數的名稱(由百分比符號(`%`)包圍)，將可全域存取的變數從您網站的使用者端(`cartAbandonsTotal`)對應至XDM欄位。
>
>您也可以使用其他先前建立的資料元素來填入這些欄位。 如需詳細資訊，請參閱標籤檔案中[資料元素](../tags/ui/managing-resources/data-elements.md)的參考。

完成將資料對應到結構描述後，請先提供資料元素的名稱，再選取&#x200B;**[!UICONTROL 儲存]**。

![命名並儲存資料元素](./images/e2e/name-and-save.png)

### 建立規則

儲存資料元素後，下一步就是建立規則，每當網站上發生特定事件（例如客戶將產品新增至購物車時）時，就會傳送給Edge Network。

您幾乎可以為任何可能發生在您網站上的事件設定規則。 例如，本節說明如何建立客戶提交表單時會觸發的規則。 以下HTML代表具有「加入購物車」表單的簡單網頁，此表單將成為規則的主題：

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

在資料收集UI中，選取左側導覽中的&#x200B;**[!UICONTROL 規則]**，然後選取&#x200B;**[!UICONTROL 建立新規則]**。

![規則](./images/e2e/rules.png)

在下一個畫面中，提供規則的名稱。 從這裡，下一步是決定規則的事件（換句話說，規則將於何時引發）。 選取[!UICONTROL 事件]下的&#x200B;**[!UICONTROL 新增]**。

![名稱規則](./images/e2e/name-rule.png)

事件組態頁面即會顯示。 若要設定事件，您必須先選取事件型別。 事件型別由擴充功能提供。 若要設定「表單提交」事件，例如，請選取&#x200B;**[!UICONTROL 核心]**&#x200B;擴充功能，然後在&#x200B;**[!UICONTROL 表單]**&#x200B;類別下選取&#x200B;**[!UICONTROL 提交]**&#x200B;事件型別。

>[!NOTE]
>
>如需AdobeWeb擴充功能所提供之不同事件型別的詳細資訊，包括設定方式，請參閱標籤檔案中的[Adobe擴充功能參考](../tags/extensions/client/overview.md)。

表單提交事件可讓您使用[CSS選取器](https://www.w3schools.com/css/css_selectors.asp)來參照要引發規則的特定元素。 在下列範例中，已使用ID `add-to-cart-form`，因此此規則只會針對「加入購物車」表單觸發。 選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將事件新增至規則。

![事件設定](./images/e2e/event-config.png)

規則設定頁面會重新顯示，顯示事件已新增。 您可以進一步新增條件至規則，以縮小&quot;[!UICONTROL If]&quot;的範圍。

否則，下一步就是新增動作，讓規則在觸發時執行。 選取&#x200B;**[!UICONTROL 動作]**&#x200B;下的&#x200B;**[!UICONTROL 新增]**&#x200B;以繼續。

![新增動作](./images/e2e/add-action.png)

動作組態頁面隨即顯示。 若要取得傳送資料給Edge Network的規則，請為擴充功能選取&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並為動作型別選取&#x200B;**[!UICONTROL 傳送事件]**。

![動作型別](./images/e2e/action-type.png)

畫面會更新，以顯示其他選項來設定傳送事件動作。 在&#x200B;**[!UICONTROL 型別]**&#x200B;底下，您可以提供自訂型別值來填入`eventType` XDM欄位。 在&#x200B;**[!UICONTROL XDM資料]**&#x200B;下，提供您先前建立的XDM資料型別的名稱（以百分比符號包圍），或選取資料庫圖示（![資料庫圖示](./images/e2e/database-symbol.png)）以從清單中選取它。 這是最終將傳送至Edge Network的資料。

完成時選取&#x200B;**[!UICONTROL 保留變更]**。

![動作設定](./images/e2e/action-config.png)

完成規則設定後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成程式。

![儲存規則](./images/e2e/save-rule.png)

### 建置及安裝程式庫 {#library}

設定規則後，您就可以將其新增至標籤程式庫、將該程式庫建置至環境，並在您的網站上安裝該建置。

>[!NOTE]
>
>如果您尚未在資料收集UI中設定環境，您必須先設定環境，然後才能建立組建。 如需詳細資訊，請參閱標籤檔案中有關[為Web屬性設定環境](../tags/ui/publishing/environments.md#web-configuration)的章節。

若要瞭解如何建立程式庫、將擴充功能和規則新增至程式庫，以及將該程式庫建置至環境，請參閱標籤檔案中有關[管理程式庫](../tags/ui/publishing/libraries.md)的指南。 建立程式庫時，請務必包含Platform Web SDK擴充功能以及您先前建立的資料收集規則。

建立程式庫並將其組建指派給環境後，您就可以將該環境安裝在網站的使用者端。 如需詳細資訊，請參閱[安裝環境](../tags/ui/publishing/environments.md#installation)的相關章節。

在網站上安裝環境後，您就可以使用Adobe Experience Platform Debugger[測試您的實作](../tags/ui/publishing/embed-code-testing.md)。

## 設定事件轉送（選擇性） {#event-forwarding}

>[!NOTE]
>
>事件轉送僅適用於已獲得授權的組織。

在設定SDK將資料傳送至Edge Network後，您就可以設定事件轉送，以告知Edge Network您要將資料傳送至何處。

若要使用事件轉送，您必須先建立事件轉送屬性。 在左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**，然後選取&#x200B;**[!UICONTROL 新增屬性]**。 在選取&#x200B;**[!UICONTROL 儲存]**&#x200B;之前，提供屬性的名稱。

建立事件轉送屬性後，下一步就是建立規則以決定應傳送資料的位置。 事件轉送屬性的規則與標籤屬性的建構方式大致相同，唯一例外是不能指定任何事件（因為事件轉送只會處理直接從資料流接收的事件）。 對於規則的動作，您可以使用其中一個可用的事件轉送擴充功能，或改用自訂程式碼來傳送事件。

![事件轉送規則](./images/e2e/event-forwarding-rule.png)

與之前類似，設定規則後，您必須將其新增至程式庫，並將該程式庫建置至環境。

建置完成後，最後一個步驟是更新您[先前設定的](#datastream)資料流，並啟用事件轉送。 若要開始，請導覽至&#x200B;**[!UICONTROL 資料串流]**，並從清單中選取有問題的資料串流。 從這裡，啟用事件轉送的切換，並提供您剛設定的屬性和環境名稱。

![事件轉送資料流](./images/e2e/event-forwarding-datastream.png)

## 後續步驟

本指南提供如何使用Platform Web SDK傳送資料給Edge Network的高階端對端總覽。 如需各種相關元件和服務的詳細資訊，請參閱本指南中的檔案連結。
