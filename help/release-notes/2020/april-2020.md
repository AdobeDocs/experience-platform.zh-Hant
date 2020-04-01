---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Adobe Experience Platform 發行說明

## 發行日期: 2020 年 4 月 8 日

## 存取控制

Experience Platform運用 [Adobe Admin Console產品設定檔](https://adminconsole.adobe.com) ，將使用者與權限和沙盒連結在一起。 權限控制對各種平台功能的存取，包括資料模型、描述檔管理和沙盒管理。

### 主要功能

| 功能 | 說明 |
|--- | ---|
| 權限 | 在「管理控制台」中，「平台 __ 」產品設定檔中的「權限」標籤可讓您自訂附加至該設定檔的使用者可使用哪些平台功能。 可用權限類別包括：資料模型、資料管理、描述檔管理、身分識別、資料監控、沙盒管理、目標、來源。 |
| 存取沙盒 | 「平 _台_ 」產品設定檔中的「權限」標籤可授予使用者特定沙盒的存取權。 如需詳細資訊，請參 [閱下方](#sandboxes) 「沙盒」一節。 |

如需詳細資訊，請參閱存 [取控制概觀](../../access-control/home.md)。

## 沙盒

Experience Platform旨在讓全球數位體驗應用程式更加豐富。 公司通常並行執行多種數位體驗應用程式，並需要滿足這些應用程式的開發、測試和部署需求，同時確保運作符合規範。 為瞭解決此需求，Experience Platform提供沙盒，可將單一平台實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 主要功能

| 功能 | 說明 |
|--- | ---|
| 製作沙盒 | Experience Platform提供單一生產沙盒，無法刪除或重設。 |
| 非生產沙盒 | 您可針對單一平台實例建立多個非生產沙盒，讓您測試功能、執行實驗並建立自訂組態，而不會影響您的生產沙盒。 |
| 沙盒切換器 | 在Experience Platform使用者介面中，位於畫面左上角的沙盒切換器可讓您透過下拉式選單在可用沙盒之間切換。 |
| `x-sandbox-name` 標題 | 所有對Experience Platform API的呼叫現在必須包 `x-sandbox-name` 含新的標頭，其值會參 `name` 考執行該作業的沙盒屬性。 |

如需詳細資訊，請參閱 [沙盒總覽](../../sandboxes/home.md)。