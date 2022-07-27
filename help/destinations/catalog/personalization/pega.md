---
title: Pega客戶決策中心連接
description: 使用Adobe Experience Platform的Pega客戶決策中心目標將配置檔案屬性和段成員資料發送到Pega客戶決策中心，以便進行下一最佳行動決策。
source-git-commit: 475b3b6dceefe968ffb451193cee4d7ed6387c86
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# Pega客戶決策中心連接

## 總覽 {#overview}

使用 [!DNL Pega Customer Decision Hub] 目的地：Adobe Experience Platform，將配置檔案屬性和段成員身份資料發送到 [!DNL Pega Customer Decision Hub] 下一個最佳動作決策。

從Adobe Experience Platform加入配置檔案段成員身份時 [!DNL Pega Customer Decision Hub]，可用作自適應模型中的預測器，並幫助提供適當的上下文和行為資料以用於下一最佳動作決策目的。

>[!IMPORTANT]
>
>此文檔頁面由Pegasystems建立。 如有任何查詢或更新請求，請直接與Pega聯繫 [這裡](mailto:support@pega.com)。

## 使用案例

幫助您更好地瞭解您應如何以及何時使用 [!DNL Customer Decision Hub] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 電信

營銷人員希望利用資料科學模型下的下一最佳行動提供的洞見 [!DNL Pega Customer Decision Hub] 用於客戶接洽。 [!DNL Pega Customer Decision Hub] 嚴重依賴客戶意圖 — 例如「Intesed_In_5G」、「Interest_in_Unlimited_Dataplan」或「Interest_in_iPhone附件」。

### 金融服務

營銷人員希望優化為訂閱或未訂閱養老金計畫或退休計畫新聞稿的客戶提供的服務。 金融服務公司可以將多個客戶ID從自己的CRM中接收到Adobe Experience Platform，從自己的離線資料構建段，並將輸入和退出段的配置檔案發送到 [!DNL Pega Customer Decision Hub] 在出站頻道進行次佳動作(NBA)決策。

## 先決條件 {#prerequisites}

在使用此目標將資料導出到Adobe Experience Platform之前，請確保在 [!DNL Pega Customer Decision Hub]:

* 在中配置Adobe段成員身份元件 [!DNL Pega Customer Decision Hub] 實例。
* 配置OAuth 2.0 [使用客戶端憑據進行客戶端註冊](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 授予類型 [!DNL Pega Customer Decision Hub] 實例。
* 配置 [即時運行資料流](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flow)  用於Adobe段成員身份資料流 [!DNL Pega Customer Decision Hub] 實例。

## 支援的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援激活下表中所述的自定義用戶ID。 有關詳細資訊，請參閱 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 |
|---|---|
| *客戶ID* | 唯一標識中配置檔案的通用用戶標識符 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 導出具有標識符的段的所有成員(*客戶ID*)、屬性（姓氏、名、位置等） 和段成員身份資料。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標始終基於API的連接。 一旦在Experience Platform中更新配置檔案，則連接器基於段評估將更新下游發送到目標平台。 有關詳細資訊，請參見 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

#### OAuth 2客戶端憑據身份驗證 {#oauth-2-client-credentials-authentication}

![UI螢幕的影像，您可以在其中使用OAuth 2和客戶端憑據身份驗證連接到Pega CDH目標](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填寫下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL 訪問令牌URL]**:您的OAuth 2訪問令牌URL [!DNL Pega Customer Decision Hub] 實例。
* **[!UICONTROL 客戶端ID]**:OAuth 2 [!DNL client ID] 你創造的 [!DNL Pega Customer Decision Hub] 實例。
* **[!UICONTROL 客戶端密碼]**:OAuth 2 [!DNL client secret] 你創造的 [!DNL Pega Customer Decision Hub] 實例。

### 填寫目標詳細資訊 {#destination-details}

在與 [!DNL Pega Customer Decision Hub]，提供目標的以下資訊：

![顯示Pega CDH目標詳細資訊的已完成欄位的UI螢幕影像](../../assets/catalog/personalization/pega/pega-connect-destination.png)

要配置目標的詳細資訊，請填寫必填欄位並選擇 **[!UICONTROL 下一個]**。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 主機名]**:配置檔案作為json資料導出到的Pega客戶決策中心主機名。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [激活受眾資料以流式處理配置檔案導出目標](../../ui/activate-streaming-profile-destinations.md) 有關激活此目標受眾段的說明。

### 目標屬性 {#attributes}

在 [[!UICONTROL 選擇屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。

### 映射示例：激活配置檔案更新 [!DNL Pega Customer Decision Hub]

下面是將配置檔案導出到時正確標識映射的示例 [!DNL Pega Customer Decision Hub]。

選擇源欄位：

* 選擇標識符(例如：CustomerID)作為唯一標識Adobe Experience Platform和 [!DNL Pega Customer Decision Hub]。
* 選擇需要在中導出和更新的XDM源配置檔案屬性更改 [!DNL Pega Customer Decision Hub]。

選擇目標欄位：

* 選擇 `CustomerID` 命名空間作為目標標識。
* 選擇需要映射到相應XDM源配置檔案屬性的目標配置檔案屬性名稱。

![標識映射](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 導出的資料/驗證資料導出 {#exported-data}

配置檔案的成功段成員身份更新將在Pega市場營銷段成員身份資料儲存中插入段標識符、名稱和狀態。 成員身份資料使用中的客戶配置檔案設計器與客戶關聯 [!DNL Pega Customer Decision Hub]，如下所示。
![UI螢幕的影像，您可以使用客戶配置檔案設計器將Adobe段成員資格資料與客戶關聯](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

段成員資格資料用於Pega Next-Best-Action Designer Engagement策略中，用於下一最佳動作決策，如下所示。
![UI螢幕的影像，您可以在Pega Next-Best-Action Designer的Engagement Policys中將段成員身份欄位添加為條件](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

客戶段成員資格資料欄位作為預測器添加到自適應模型中，如下所示。
![UI螢幕的影像，您可以使用Prediction Studio將段成員資格欄位添加為自適應模型中的預測器](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他資源 {#additional-resources}

請參閱 [設定OAuth 2.0客戶端註冊](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 在 [!DNL Pega Customer Decision Hub]。

請參閱 [為資料流建立即時運行](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 在 [!DNL Pega Customer Decision Hub]。

請參閱 [在客戶配置檔案設計器中管理客戶記錄](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86)。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
