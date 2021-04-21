---
keywords: Experience Platform；首頁；熱門主題；故障排除；訪問控制
solution: Experience Platform
title: 存取控制疑難排解指南
topic-legacy: troubleshooting guide
description: 本檔案提供有關Adobe Experience Platform地區存取控制常見問題的解答。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 存取控制疑難排解指南

本檔案提供有關Adobe Experience Platform地區存取控制常見問題的解答。 有關其他[!DNL Platform]服務的問題和故障排除，請參閱[Experience Platform故障排除指南](../landing/troubleshooting.md)。

[!DNL Experience Platform] 運用 [Adobe管理控](http://adminconsole.adobe.com) 制台中的產品設定檔，提供角色存取控制，將使用者與權限和沙盒連結。有關詳細資訊，請參閱[訪問控制概述](home.md)。

## 我可以在哪裡找到目前的存取權限？

如果您是IMS組織的系統管理員、產品管理員或產品描述檔管理員，則可以檢視指派的產品描述檔及其在Adobe Admin Console內提供的權限。 請參閱[存取控制使用指南](./ui/overview.md)以取得如何導覽[!DNL Admin Console]以檢視產品設定檔權限的指示。

如果您不是管理員，您仍可以透過傳送要求至存取控制API中的`/acl/effective-policies`端點，來檢視目前的存取權限。 如需詳細資訊，請參閱[存取控制開發人員指南](./api/effective-policies.md)中的「檢視有效政策」一節。

## [!DNL Platform] UI中的某些功能不可用。 這些功能的存取權如何由權限控制？

如果您沒有特定[!DNL Platform]功能的存取權限，該功能在[!DNL Experience Platform] UI中會隱藏或變灰。 例如，若要檢視&quot;[!UICONTROL Profiles]&quot;標籤，您必須擁有&quot;[!UICONTROL View Profiles]&quot;或&quot;[!UICONTROL Manage Profiles]&quot;權限。 如果您需要[!DNL Experience Platform]功能的額外權限，請連絡您的管理員。

## 權限分組方式，以及哪個群組包含我要使用的權限？

權限依其套用的[!DNL Platform]功能（例如[!DNL Data Management]和[!DNL Profile Management]）分組和分類。 如需可用權限及其所屬群組的完整清單，請參閱存取控制概觀中的[權限區段](home.md#permissions)。

有關提供基於角色的訪問控制的詳細資訊，請參見[訪問控制概述](home.md)。
