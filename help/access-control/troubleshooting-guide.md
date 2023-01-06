---
keywords: Experience Platform；首頁；熱門主題；疑難排解；存取控制
solution: Experience Platform
title: 存取控制疑難排解指南
description: 本檔案提供關於Adobe Experience Platform存取控制常見問題的解答。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 存取控制疑難排解指南

本檔案提供關於Adobe Experience Platform存取控制常見問題的解答。 以了解與其他 [!DNL Platform] 服務，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

[!DNL Experience Platform] 會利用 [Adobe Admin Console](https://adminconsole.adobe.com) 提供角色型存取控制，將使用者連結至權限和沙箱。  請參閱 [存取控制概觀](home.md) 以取得更多資訊。

## 在哪裡可以找到我目前的存取權限？

如果您是IMS組織的系統管理員、產品管理員或產品設定檔管理員，可以檢視指派的產品設定檔及其在Adobe Admin Console內提供的權限。 請參閱 [存取控制使用手冊](./ui/overview.md) 導航說明 [!DNL Admin Console] 檢視產品設定檔的權限。

如果您不是管理員，您仍可以透過傳送要求至 `/acl/effective-policies` 端點。 請參閱 [存取控制開發人員指南](./api/effective-policies.md) 以取得更多資訊。

## 中的部分功能 [!DNL Platform] 無法使用UI。 權限如何控制對這些功能的存取？

如果您沒有特定的 [!DNL Platform] 特徵，該特徵將在 [!DNL Experience Platform] UI。 例如，為了檢視「[!UICONTROL 設定檔]「 」標籤中，您必須有「[!UICONTROL 檢視設定檔]&quot;或&quot;[!UICONTROL 管理設定檔]&quot;權限。 若您需要 [!DNL Experience Platform] 功能。

## 權限分組方式，以及哪個群組包含我要使用的權限？

權限會依 [!DNL Platform] 功能(例如 [!DNL Data Management] 和 [!DNL Profile Management])。 如需可用權限及其所屬群組的完整清單，請參閱 [權限區段](home.md#permissions) （在存取控制概述中）。

請參閱 [存取控制概觀](home.md) 有關提供基於角色的訪問控制的詳細資訊。

## 從AdobeIO移轉至業務ID後，權限會發生什麼事？

存取控制使用使用者ID（指派給使用者的內部唯一ID）來授予權限。 當組織從Adobe ID移轉至業務ID時，其使用者所設定的所有權限都會遺失，因為使用者ID變更且存取控制將使用新產生的使用者ID。 如果貴組織已移轉至Business ID，請連絡您的Adobe代表，將您的使用者ID從Adobe ID移轉至Business ID。
