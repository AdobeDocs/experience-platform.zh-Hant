---
keywords: Experience Platform；首頁；熱門主題；疑難解答；訪問控制
solution: Experience Platform
title: 訪問控制故障排除指南
description: 本文檔提供有關Adobe Experience Platform訪問控制的常見問題的答案。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 訪問控制故障排除指南

本文檔提供有關Adobe Experience Platform訪問控制的常見問題的答案。 有關與其他相關的問題和故障排除 [!DNL Platform] 服務，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 提供基於角色的訪問控制，將用戶與權限和沙箱連結起來。  查看 [訪問控制概述](home.md) 的子菜單。

## 在哪裡可以找到我的當前訪問權限？

如果您是組織的系統管理員、產品管理員或產品配置檔案管理員，則可以查看您分配的產品配置檔案及其在Adobe Admin Console內提供的權限。 查看 [訪問控制使用手冊](./ui/overview.md) 有關如何導航的說明 [!DNL Admin Console] 查看產品配置檔案的權限。

如果您不是管理員，您仍然可以通過向 `/acl/effective-policies` 訪問控制API中的終結點。 請參閱中的「查看有效策略」部分 [訪問控制開發者指南](./api/effective-policies.md) 的子菜單。

## 中的某些功能 [!DNL Platform] UI不可用。 如何通過權限控制對這些功能的訪問？

如果您沒有特定的訪問權限 [!DNL Platform] 將在 [!DNL Experience Platform] UI。 例如，為了查看&quot;[!UICONTROL 配置檔案]「 」頁籤，必須具有「 」[!UICONTROL 查看配置檔案]&quot;或&quot;[!UICONTROL 管理配置檔案]&quot;權限。 如果您需要其他權限，請與管理員聯繫 [!DNL Experience Platform] 功能。

## 權限分組方式，以及哪個組包含我要使用的權限？

權限按 [!DNL Platform] 應用於(例如 [!DNL Data Management] 和 [!DNL Profile Management])。 有關可用權限及其所屬組的完整清單，請參見 [權限部分](home.md#permissions) 訪問控制概述中。

查看 [訪問控制概述](home.md) 的子菜單。

## 從AdobeIO遷移到業務ID後，權限會如何？

訪問控制使用用戶ID（分配給用戶的內部唯一ID）授予權限。 當組織從Adobe ID遷移到業務ID時，其用戶設定的所有權限都將丟失，因為用戶ID更改，訪問控制將使用新生成的用戶ID。 如果您的組織已遷移到業務ID，請與Adobe代表聯繫，將您的用戶ID從Adobe ID遷移到業務ID。
