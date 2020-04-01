---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 存取控制疑難排解指南
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# 存取控制疑難排解指南

本檔案提供有關Adobe Experience Platform中存取控制常見問題的解答。 有關其他平台服務的問題和疑難排解，請參閱「 [Experience Platform疑難排解指南」](../landing/troubleshooting.md)。

Experience Platform運用 [Adobe Admin Console中的產品設定檔](http://adminconsole.adobe.com) ，提供以角色為基礎的存 **取控制**，將使用者與權限和沙盒連結。  如需詳細 [資訊，請參閱存取控制概觀](home.md) 。

## 我可以在哪裡找到目前的存取權限？

如果您是IMS組織的系統管理員、產品管理員或產品描述檔管理員，您可以在Adobe Admin Console中檢視您指派的產品描述檔及其提供的權限。 如需如 [](./ui/overview.md) 何導覽「管理控制台」以檢視產品設定檔權限的指示，請參閱存取控制使用指南。

如果您不是管理員，您仍可以透過傳送要求至「存取控制API」中的端點，來檢 `/acl/effective-policies` 視目前的存取權限。 如需詳細資訊，請參閱存取控制開發人 [員指南中的](./api/effective-policies.md) 「檢視有效政策」一節。

## 平台UI中有些功能不提供。 這些功能的存取權如何由權限控制？

如果您沒有特定平台功能的存取權限，該功能在Experience Platform UI中會隱藏或變灰。 例如，若要檢視「描述檔」標籤，您必須擁有「檢視描述檔」或「管理描述檔」權限。 如果您需要額外的Experience Platform功能權限，請連絡您的管理員。

## 權限分組方式，以及哪個群組包含我要使用的權限？

權限會依其套用的平台功能（例如資料管理和描述檔管理）進行分組和分類。 如需可用權限及其所屬群組的完整清單，請參閱存取控 [制概述中的](home.md#permissions) 「權限」區段。

有關提供 [基於角色的訪問控制的詳細資訊](home.md) ，請參閱訪問控制概述。