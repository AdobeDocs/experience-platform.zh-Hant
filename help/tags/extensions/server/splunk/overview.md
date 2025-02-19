---
title: Splunk擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Splunk擴充功能。
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 1%

---

# Splunk擴充功能概觀

[Splunk](https://www.splunk.com)是可觀察性平台，可提供針對您資料的可操作深入分析之搜尋、分析和視覺化。 Splunk [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能運用[Splunk HTTP事件收集器REST API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints)，將事件從Adobe Experience Platform Edge Network傳送至[Splunk HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)。

Splunk使用持有人權杖作為驗證機制，與Splunk事件收集器API通訊。

## 使用案例 {#use-cases}

行銷團隊可在下列使用案例中使用此擴充功能：

| 使用實例 | 說明 |
| --- | --- |
| 客戶行為分析 | 組織可以從其網站擷取客戶互動事件資料，並將相關事件轉送至Splunk。 行銷與分析團隊可以在Splunk平台內執行後續分析，以瞭解關鍵使用者的互動和行為。 Splunk平台可用來產生圖表、儀表板或其他視覺效果，以告知業務利害關係人。 |
| 在大型資料集上可擴充的搜尋 | 組織可以從網站擷取交易或對話輸入作為事件資料，並將事件轉送到Splunk。 然後，Analytics團隊可以利用Splunk的可擴充索引功能，篩選及處理大型資料集，以獲得任何業務分析並做出明智決策。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

您必須有Splunk帳戶才能使用此擴充功能。 您可以在[Splunk首頁](https://www.splunk.com/page/sign_up)註冊Splunk帳戶。

>[!NOTE]
>
> Splunk擴充功能同時支援Splunk Cloud和Splunk Enterprise執行個體。 本指南會記錄使用[Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html)作為參考的實作。 [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html)的組態程式類似，但需要您的Splunk Enterprise管理員提供特定指引。

您也必須具備下列技術值才能設定擴充功能：

* [事件收集器權杖](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform)。 Token通常是UUIDv4格式，如下所示： `12345678-1234-1234-1234-1234567890AB`。
* 貴組織的Splunk平台執行個體位址和連線埠。 Platform執行個體位址和連線埠通常具有下列格式： `mysplunkserver.example.com:443`。

  >[!IMPORTANT]
  >
  > 在事件轉送中參考的Splunk端點應僅使用連線埠`443`。 事件轉送實作目前不支援非標準連線埠。

## 安裝Splunk擴充功能 {#install}

若要在UI中安裝Splunk事件收集器擴充功能，請導覽至&#x200B;**事件轉送**&#x200B;並選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，請瀏覽至&#x200B;**擴充功能** > **目錄**。 搜尋&quot;[!DNL Splunk]&quot;，然後在Splunk擴充功能上選取&#x200B;**[!DNL Install]**。

在UI中選取之Splunk擴充功能的![安裝按鈕](../../../images/extensions/server/splunk/install.png)

## 設定Splunk擴充功能 {#configure_extension}

>[!IMPORTANT]
>
>根據您的實作需求，您可能需要在設定擴充功能前建立結構、資料元素和資料集。 開始之前，請先檢閱所有設定步驟，以決定您需要為使用案例設定的實體。

在左側導覽中選取&#x200B;**擴充功能**。 在&#x200B;**已安裝**&#x200B;下，選取Splunk擴充功能上的&#x200B;**設定**。

在UI中選取的Splunk擴充功能的![設定按鈕](../../../images/extensions/server/splunk/configure.png)

針對&#x200B;**[!UICONTROL HTTP事件收集器URL]**，請輸入您的Splunk平台執行個體位址和連線埠。 在&#x200B;**[!UICONTROL 存取Token]**&#x200B;下，輸入您的[!DNL Event Collector Token]值。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。

![組態選項已在UI中填寫](../../../images/extensions/server/splunk/input.png)

## 設定事件轉送規則 {#config_rule}

開始建立新的事件轉送規則[規則](../../../ui/managing-resources/rules.md)，並視需要設定其條件。 選取規則的動作時，請選取[!UICONTROL Splunk]擴充功能，然後選取[!UICONTROL 建立事件]動作型別。 似乎有其他控制項可進一步設定Splunk事件。

![定義動作組態](../../../images/extensions/server/splunk/action-configurations.png)

下一步是將該Splunk事件屬性對應至您先前建立的資料元素。 以下提供根據可設定的輸入事件資料支援的選用對應。 如需詳細資訊，請參閱[Splunk檔案](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata)。

| 欄位名稱 | 說明 |
| --- | --- |
| [!UICONTROL 事件&#x200B;]<br><br>**（必要）** | 指定您要如何提供事件資料。 事件資料可以指派給HTTP請求中JSON物件內的`event`索引鍵，也可以是原始文字。 `event`金鑰與JSON事件封包內的中繼資料金鑰位於相同層級。 在`event`鍵值大括弧內，資料可以採行您所需的任何形式（例如字串、數字、其他JSON物件等）。 |
| [!UICONTROL 主機] | 您傳送資料之來源使用者端的主機名稱。 |
| [!UICONTROL Source型別] | 要指派給事件資料的來源型別。 |
| [!UICONTROL Source] | 要指派給事件資料的來源值。 例如，如果您從正在開發的應用程式傳送資料，請將此索引鍵設為應用程式的名稱。 |
| [!UICONTROL 索引] | 事件資料索引的名稱。 如果權杖設定了索引引數，您在此指定的索引必須在允許的索引清單中。 |
| [!UICONTROL 時間] | 事件時間。 預設時間格式為UNIX時間（格式為`<sec>.<ms>`），取決於您的當地時區。 例如，`1433188255.500`表示紀元後1433188255秒和500毫秒，或2015年6月1日星期一晚上7:50:55 GMT。 |
| [!UICONTROL 欄位] | 指定原始JSON物件或包含要在索引時間定義的明確自訂欄位的一組索引鍵/值組。  `fields`金鑰不適用於原始資料。<br><br>包含`fields`屬性的要求必須傳送至`/collector/event`端點，否則將不會編制索引。 如需詳細資訊，請參閱有關[索引欄位擷取](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC)的Splunk檔案。 |

### 驗證Splunk中的資料 {#validate}

建立並執行事件轉送規則後，驗證傳送至Splunk API的事件是否如預期般顯示在Splunk UI中。 如果事件收集和Experience Platform整合成功，您會在Splunk主控台中看到事件，如下所示：

![驗證期間出現在Splunk UI中的事件資料](../../../images/extensions/server/splunk/splunk-data.png)

## 後續步驟

本檔案說明如何在UI中安裝和設定Splunk事件轉送擴充功能。 如需在Splunk中收集事件資料的詳細資訊，請參閱正式檔案：

* [在Splunk Web中設定及使用HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [使用權杖設定驗證](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [疑難排解HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) （也列出[可能的錯誤碼](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes)的彙編）
