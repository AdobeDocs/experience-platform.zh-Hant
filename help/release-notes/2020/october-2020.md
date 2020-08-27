---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 6%

---


# Adobe Experience Platform 發行說明

**發行日期：2020年10月**

Adobe Experience Platform的新功能：

- [[!DNL訪問控制]](#access-control)
- [[!DNL沙盒]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 運用 [Adobe Admin Console](https://adminconsole.adobe.com) 產品設定檔，將使用者與權限和沙盒連結。 權限控制對各種平台功能的存取，包括資料模型、描述檔管理和沙盒管理。

**主要功能**

| 功能 | 說明 |
|--- | ---|
| 權限 | 在中， [!DNL Admin Console]產品配置檔案中的選 [!DNL Platform] 項卡允許您自定義附加到該 [!DNL Platform] 配置檔案的用戶可以使用哪些功能。 可用權限類別包括： [!UICONTROL 資料建模], [!UICONTROL 資料管理], [!UICONTROL 管理]，概要資訊監控， 資料管理，沙箱管理，沙箱目標，源標識。 |
| 存取沙盒 | 產品 [!UICONTROL _設定檔中的_] 「權限」 [!DNL Platform] 標籤可授予使用者特定沙盒的存取權。 如需詳細資訊，請參 [閱下方](#sandboxes) 「沙盒」一節。 |

如需詳細資訊，請參閱存 [取控制概觀](../../access-control/home.md)。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在讓全球數位體驗應用程式更加豐富。 公司通常並行執行多種數位體驗應用程式，並需要滿足這些應用程式的開發、測試和部署需求，同時確保運作符合規範。 為了滿足此需求，提供 [!DNL Experience Platform] 沙盒，將單一執行個體分割為 [!DNL Platform] 個別的虛擬環境，以協助開發和發展數位體驗應用程式。

**主要功能**

| 功能 | 說明 |
|--- | ---|
| 製作沙盒 | [!DNL Experience Platform] 提供單一生產沙盒，無法刪除或重設。 |
| 非生產沙盒 | 您可針對單一執行個體建立多個非生產沙盒，讓 [!DNL Platform] 您測試功能、執行實驗並建立自訂組態，而不會影響您的生產沙盒。 |
| 沙盒切換器 | 在使用 [!DNL Experience Platform] 者介面中，畫面左上角的沙盒切換器可讓您透過下拉式選單，在可用沙盒之間切換。 |
| `x-sandbox-name` 標題 | 所有對 [!DNL Experience Platform] API的呼叫現在必須包含新 `x-sandbox-name` 標題，其值會參 `name` 考執行作業的沙盒屬性。 |

如需詳細資訊，請參閱 [沙盒總覽](../../sandboxes/home.md)。