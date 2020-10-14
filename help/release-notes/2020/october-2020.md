---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 43ceda3d95511c3972fd0588f472c6c412dd95bf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 6%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 10 月 14 日**

- [資料準備](#data-prep)
- [即時客戶個人檔案](#profile)
- [來源](#sources)

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| `is_set` 函數 | 此函 `is_set` 數允許您檢查源資料中是否存在屬性。 `is_set` 可與組合使用， `is_empty` 以檢查屬性的存在和屬性中值的存在。 |
| `get_values` 函數 | 此函 `get_values` 數可讓您從輸入映射取得任何指定鍵的值。 |

如需詳細資訊，請閱讀資料準 [備概觀](../../data-prep/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過 [!DNL Real-time Customer Profile]此功能，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 描述檔預覽API新增功能 | 描述檔預覽API(`/previewsamplestatus`)現在包含在IMS組織中檢視描述檔片段總數的劃分，以及在身分名稱空間中檢視描述檔片段的分佈。 |
| 聯合架構視圖更新 | 在Experience Platform UI中，使用者可以更輕鬆地找到有關所有結構描述和資料集的資訊，以及表面金鑰屬性，例如身分和關係欄位。 這些更新可改善疑難排解和驗證描述檔已正確設定、身分識別已正確銜接，以及資料已成功擷取的能力。 |

有關使用資 [!DNL Real-time Customer Profile]料的更多資訊，包括教學課程和最佳實務，請 [!DNL Profile] 閱讀即時客 [戶資料概觀](../../profile/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 分層映射 | 您可以在資料擷取程式期間預覽階層式來源檔案，例如JSON或Parce。 |
| SFTP的SSH驗證支援 | 您可以使用RSA/DSA Open SSH密鑰將SFTP [!DNL Platform] 帳戶連接到。 如需詳細 [資訊，請參閱](../../sources/connectors/cloud-storage/ftp-sftp.md) SFTP概觀。 |
| UX改進 | 您可以在資料擷取程式 [!DNL Profile] 期間啟用資料集。 如需詳細 [資訊，請參閱雲端儲存資料流工作流程](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 教學課程。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。