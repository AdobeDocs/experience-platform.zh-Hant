---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
hide: true
hidefromtoc: true
source-git-commit: c716bac1db556fe7a47462e38ee64d7b46bbefcc
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 44%

---


# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年6月18日**

Adobe Experience Platform中的新功能及現有功能更新：

- [存取控制](#access-control)
- [進階資料生命週期管理](#advanced-data-lifecycle-management)
- [儀表板](#dashboards)
- [資料控管](#data-governance)
- [目標](#destinations)
- [聯合客群構成](#fac)
- [Privacy Service](#privacy-service)
- [沙箱](#sandboxes)
- [來源](#sources)

## 存取控制 {#access-control}

Experience Platform運用[Adobe Admin Console](https://adminconsole.adobe.com)產品設定檔來連結具有許可權和沙箱的使用者。 許可權可控制各種Experience Platform功能的存取權，包括資料模型製作、設定檔管理和沙箱管理。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匯出儀表板資料許可權 | 儀表板中的&#x200B;**[!UICONTROL 下載CSV]**&#x200B;和&#x200B;**[!UICONTROL 以電子郵件傳送]**&#x200B;選項現在需要&#x200B;**[!UICONTROL 匯出儀表板資料]**&#x200B;許可權。 此許可權可確保只有授權的使用者才能匯出清單化insight資料，支援更嚴格的控管和資料存取控制原則。 |

如需詳細資訊，請參閱[存取控制總覽](../access-control/home.md)。

## 進階資料生命週期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供一套資料檢疫功能，可讓您以程式化方式刪除消費者記錄與資料集，以管理儲存的資料。利用使用者介面中的資料生命週期工作區，或透過呼叫資料檢疫 API，您可以有效地管理資料儲存區。利用這些功能可確保資訊如預期般使用、在不正確的資料需要修正時更新資訊，以及在組織原則認為必要時刪除資訊。

**新文件**

| 新文件 | 說明 |
| --- | --- |
| 記錄刪除一般可用性 | 您現在可以使用UI或API根據身分欄位刪除個別記錄。 此功能允許從單一資料集或所有資料集中進行刪除，有助於減少儲存、強制執行治理並改善資料衛生。 數量限制與權利要求適用。 |

如需詳細資訊，請閱讀[進階資料生命週期管理概觀](../hygiene/home.md)。

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板，檢視每日快照期間擷取之組織資料的重要解析。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 以電子郵件匯出選項傳送 | 您現在可以從Query Pro模式儀表板匯出最多10,000筆記錄，方法是從&#x200B;**[!UICONTROL 檢視更多]**&#x200B;選單中選取&#x200B;**[!UICONTROL 以電子郵件傳送]**。 此選項會將下載連結安全地傳送至與Adobe相關的電子郵件，以供進行較大規模的匯出。 |

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先閱讀[儀表板概觀](../dashboards/home.md)。

## 資料治理 {#data-governance}

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在 [!DNL Experience Platform] 的不同階層都扮演重要的角色，包括編目、資料譜系、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| --- | --- |
| Azure CMK警報和IP允許清單設定 | 您現在可以在Azure Key Vault中將Adobe的靜態IP位址加入允許清單，以確保在啟用網路限制時能夠繼續存取。 這有助於防止因金鑰存取受限而中斷Platform服務。 |
| CMK組態警示和解決方案 | Experience Platform現在會在Adobe服務無法存取您的Azure Key Vault （例如，由於已移除IP允許清單專案或停用的金鑰）時觸發警報。 新的指南可協助您瞭解每個警示並採取更正動作。 |

如需詳細資訊，請閱讀[資料治理概觀](../data-governance/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目的地**

| 目標 | 說明 |
| --- | --- |
| 阿爾及利亞使用者區段 | 「演演算法使用者區段」目的地可讓行銷專業人員從首頁跨網站提供一致的個人化內容以供搜尋。 從多個資料來源建立豐富的受眾，並在各種管道中共用受眾，以改進目標定位策略和行銷活動個人化。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| LinkedIn帳戶到期資訊 | LinkedIn目的地的帳戶到期資訊現在可直接在[!UICONTROL 瀏覽]與[!UICONTROL 帳戶]檢視中取得。 之前，此資訊僅可在檔案中取得。 此增強功能可讓您更清楚瞭解LinkedIn驗證狀態和憑證管理。 |
| Google Customer Match + DV360一般可用性與增強功能 | Google Customer Match + DV360目的地現在可供所有Experience Platform使用者使用。 檔案現在包含Adobe與Google廣告帳戶之間帳戶連結的詳細指引。 |
| Data Landing Zone (DLZ)目的地加密支援 | 新增資料登陸區域目的地的加密支援。 您現在可以附加RSA格式的公開金鑰，以新增加密至匯出的檔案。 |
| 適用於企業目的地的受眾層級監控 | 對象層級監視現在可用於以下企業目的地： [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)、[[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md)、[[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 聯合客群構成 {#fac}

聯合客群構成可讓企業構成資料，以善加應用於各種使用案例中。有了這種新方法，Adobe Real-Time Customer Data Platform 和/或 Adobe Journey Optimizer 的使用者就可以直接聯合現有資料倉儲中的資料集，透過單一系統建立並擴充 Adobe Experience Platform 的客群及屬性。

| 新功能 | 說明 |
| ----------- | ----------- |
| HIPAA 整備程度 | 同盟對象構成現在符合HIPAA標準。 如需同盟對象構成的隱私權與安全措施的詳細資訊，請閱讀[同盟對象構成概觀中的隱私權與安全性](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security)。 如需有關Experience Platform產品一般HIPAA相容性的詳細資訊，請閱讀[HIPAA和Adobe產品和服務總覽](https://www.adobe.com/trust/compliance/hipaa-ready.html)。 |

如需詳細資訊，請閱讀[聯合客群構成文件](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/home)。

## [!DNL Privacy Service] {#privacy}

有多項法律及組織法規授予使用者權利，讓使用者有權透過請求，從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和使用者介面，協助您管理這些來自客戶的資料請求。透過 [!DNL Privacy Service]，您可以提交請求來存取和刪除 Adobe Experience Cloud 應用程式中的私人或個人客戶資料，進而促進法律和組織隱私法規的自動化合規。

**新功能**

| 功能 | 說明 |
|--- | ---|
| 支援田納西州和明尼蘇達州隱私權法 | Privacy Service現在支援田納西資訊保護法(`tipa_tn_usa`)和明尼蘇達消費者資料隱私法(`mcdpa_mn_usa`)。 您可以依照這些新的州級法規，處理存取和刪除要求。 如需詳細資訊，請參閱[法規總覽](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview)。 |

參閱 [Privacy Service 概觀](../privacy-service/home.md)可了解更多有關該服務的資訊。

## 沙箱 {#sandboxes}

Adobe Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 物件設定更新移轉 | 您現在可以在初始復寫後，跨沙箱移轉反複物件組態更新。 此增強功能支援開發工作流程，其中設定需要更新並在不同環境傳播，而無需重新建立整個沙箱設定。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../sandboxes/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援[!DNL Azure Synapse Analytics]的新驗證型別 | 除了現有的連線字串驗證之外，[!DNL Azure Synapse Analytics]現在也將支援服務主要驗證。 |

**重要驗證更新**

| 更新 | 說明 |
| --- | --- |
| [!DNL Salesforce]基本驗證淘汰 | Salesforce CRM和Salesforce Service Cloud的基本驗證將於2026年1月前淘汰。 客戶必須移轉至OAuth 2.0驗證以維持連線。 此變更會同時影響來源聯結器，並確保增強安全性並符合Salesforce的驗證標準。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。
