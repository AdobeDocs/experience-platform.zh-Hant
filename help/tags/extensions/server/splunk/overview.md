---
title: Splunk擴展概述
description: 瞭解Splunk在Adobe Experience Platform的事件轉發擴展。
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 1%

---

# Splunk擴展概述

[斯普隆克](https://www.splunk.com) 是一個可觀察的平台，它提供搜索、分析和可視化功能，以便對您的資料進行可操作的洞見。 斯普隆克 [事件轉發](../../../ui/event-forwarding/overview.md) 擴展利用 [Splunk HTTP事件收集器REST API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) 將事件從Adobe Experience Platform邊緣網路發送到 [Splunk HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)。

Splunk使用承載令牌作為驗證機制與Splunk事件收集器API通信。

## 使用案例 {#use-cases}

市場營銷團隊可以將擴展用於以下使用案例：

| 使用案例 | 說明 |
| --- | --- |
| 客戶行為分析 | 組織可以從其網站捕獲客戶交互事件資料並將相關事件轉發到Splunk。 然後，營銷和分析團隊可以在Splunk平台內執行後續分析，以瞭解關鍵用戶交互和行為。 Splunk平台可用於生成圖形、儀表板或其他可視化，以通知業務利益相關方。 |
| 在大型資料集上可擴展的搜索 | 組織可以將事務性或會話性輸入作為事件資料從網站捕獲，並將事件轉發到Splunk。 然後，分析團隊可以利用Splunk的可擴展索引能力篩選和處理大型資料集，從而得出任何業務見解並做出明智的決策。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

您必須具有Splunk帳戶才能使用此擴展。 您可以在上註冊Splunk帳戶 [Splunk首頁](https://www.splunk.com/page/sign_up)。

>[!NOTE]
>
> Splunk擴展支援Splunk雲和Splunk企業實例。 本指南記錄了使用 [斯普隆克雲](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) 的雙曲餘切值。 的配置過程 [斯普隆克企業](https://www.splunk.com/en_us/products/splunk-enterprise.html) 類似，但需要Splunk Enterprise管理員提供特定指導。

您還必須具有以下技術值才能配置擴展：

* 安 [事件收集器標籤](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform)。 令牌通常為UUIDv4格式，如下所示： `12345678-1234-1234-1234-1234567890AB`。
* 組織的Splunk平台實例地址和埠。 平台實例地址和埠通常具有以下格式： `mysplunkserver.example.com:443`。
   >[!IMPORTANT]
   >
   > 事件轉發中引用的Splunk端點只應使用埠 `443`。 在事件轉發實現中，當前不支援非標準埠。

## 安裝Splunk擴展 {#install}

要在UI中安裝Splunk事件收集器擴展，請導航至 **事件轉發** 並選擇一個屬性以將擴展添加到，或改為建立新屬性。

選擇或建立所需屬性後，導航到 **擴展** > **目錄**。 搜索「」[!DNL Splunk]&quot;，然後選擇 **[!DNL Install]** 在斯普隆克分機上。

![在UI中選擇的Splunk擴展的安裝按鈕](../../../images/extensions/server/splunk/install.png)

## 配置Splunk擴展 {#configure_extension}

>[!IMPORTANT]
>
>根據您的實施需要，在配置擴展之前，可能需要建立架構、資料元素和資料集。 請在開始之前查看所有配置步驟，以確定您需要為使用案例設定哪些實體。

選擇 **擴展** 的子菜單。 下 **已安裝**&#x200B;選中 **配置** 在斯普隆克分機上。

![在UI中選擇的Splunk擴展的配置按鈕](../../../images/extensions/server/splunk/configure.png)

對於 **[!UICONTROL HTTP事件收集器URL]**，輸入Splunk平台實例地址和埠。 下 **[!UICONTROL 訪問令牌]**&#x200B;輸入 [!DNL Event Collector Token] 值。 完成後，選擇 **[!UICONTROL 保存]**。

![在UI中填寫的配置選項](../../../images/extensions/server/splunk/input.png)

## 配置事件轉發規則 {#config_rule}

開始建立新事件轉發規則 [規則](../../../ui/managing-resources/rules.md) 並根據需要配置其條件。 為規則選擇操作時，選擇 [!UICONTROL 斯普隆克] ，然後選擇 [!UICONTROL 建立事件] 操作類型。 其他控制項將顯示為進一步配置Splunk事件。

![定義操作配置](../../../images/extensions/server/splunk/action-configurations.png)

下一步是將Splunk事件屬性映射到先前建立的資料元素。 下面給出了基於可設定的輸入事件資料的支援的可選映射。 請參閱 [Splunk文檔](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) 的上界。

| 欄位名稱 | 說明 |
| --- | --- |
| [!UICONTROL 事件&#x200B;]<br><br>**（必需）** | 指明要如何提供事件資料。 事件資料可以分配給 `event` HTTP請求中JSON對象中的鍵，或者它可以是原始文本。 的 `event` 鍵與元資料鍵在JSON事件包中處於相同的級別。 在 `event` key-value花括弧，資料可以是您需要的任何形式（如字串、數字、其他JSON對象等）。 |
| [!UICONTROL Host] | 從中發送資料的客戶端的主機名。 |
| [!UICONTROL 來源類型] | 要分配給事件資料的源類型。 |
| [!UICONTROL 來源] | 要分配給事件資料的源值。 例如，如果您正在從正在開發的應用程式發送資料，請將此鍵設定為應用程式的名稱。 |
| [!UICONTROL 索引] | 事件資料索引的名稱。 如果令牌具有索引參數集，則此處指定的索引必須位於允許的索引清單中。 |
| [!UICONTROL 時間] | 事件時間。 預設時間格式為UNIX時間(格式為 `<sec>.<ms>`)並取決於您的本地時區。 比如說， `1433188255.500` 表示1433188255秒和500毫秒後，或2015年6月1日星期一，7:50:格林尼治時間下午5點 |
| [!UICONTROL 欄位] | 指定原始JSON對象或一組鍵值對，這些對包含要在索引時定義的顯式自定義欄位。  的 `fields` 鍵不適用於原始資料。<br><br>包含 `fields` 必須將屬性發送到 `/collector/event` 終結點，否則將不為它們編入索引。 有關詳細資訊，請參閱上的Splunk文檔 [索引欄位提取](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC)。 |

### 驗證Splunk中的資料 {#validate}

建立並執行事件轉發規則後，驗證發送到Splunk API的事件是否按預期顯示在Splunk UI中。 如果事件收集和Experience Platform整合成功，您將在Splunk控制台中看到以下事件：

![驗證期間在Splunk UI中出現的事件資料](../../../images/extensions/server/splunk/splunk-data.png)

## 後續步驟

本文檔介紹如何在UI中安裝和配置Splunk事件轉發擴展。 有關在Splunk收集事件資料的詳細資訊，請參閱官方文檔：

* [在Splunk Web中設定和使用HTTP事件收集器 ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [使用令牌設定身份驗證](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [排除HTTP事件收集器故障](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (並列出 [可能的錯誤代碼](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
