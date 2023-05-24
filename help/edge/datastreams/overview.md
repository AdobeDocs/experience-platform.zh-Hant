---
title: 資料流概述
description: 連接您的客戶端 Experience Platform SDK 與 Adobe 產品和協力廠商目標的整合。
keywords: 配置；資料流；資料流；邊；資料流ID；環境設定；邊配置ID；標識；ID同步容器ID；沙盒；流入口；事件資料集；目標；客戶端代碼；屬性令牌；目標；Cookie目標；URL目標；分析設定塊報表ID；資料資料收集準備；資料準備；映射器；XDM映射器；邊緣上的映射器；
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 4%

---

# 資料流概述

資料流代表實作 Adobe Experience Platform Web 和 Mobile SDK 時的伺服器端設定。當 [configure命令](../fundamentals/configuring-the-sdk.md) 在SDK中，控制必須在客戶端上處理的內容(如 `edgeDomain`)，資料流處理SDK的所有其它配置。 當請求發送到Adobe Experience Platform邊緣網路時， `edgeConfigId` 用於引用資料流。 這樣，您就可以更新伺服器端配置，而無需在網站上進行代碼更改。

通過選擇 **[!UICONTROL 資料流]** 在Adobe Experience PlatformUI或資料收集UI中的左側導航中。

![UI中的資料流頁籤](../assets/datastreams/overview/datastreams-tab.png)

有關如何在UI中配置資料流的詳細資訊，請參見 [配置指南](./configure.md)。

## 處理資料流中的敏感資料 {#sensitive}

>[!IMPORTANT]
>
>本檔案內容不是法律意見，不是代替法律意見。 有關處理敏感資料的建議，請咨詢貴公司的法律部門。

公司資料管理策略和法規要求對如何收集、處理和使用敏感客戶資料提出了越來越多的限制。 這包括受保護健康資料(PHI)的收集、處理和使用，這些資料受健康保險便攜性和責任法案(HIPAA)等法規的約束。

資料流提供了三種方法來幫助您安全地處理敏感資料：

* [增強加密](#encryption)
* [資料治理](#governance)
* [稽核記錄](#audit-logs)

### 增強加密 {#encryption}

通過邊緣網路傳輸的所有資料都使用安全、加密的連接進行 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246)。 如果資料流將資料引入Experience Platform，則資料隨後在Experience Platform資料湖中靜止地加密。 查看上的文檔 [資料加密在Experience Platform](../../landing/governance-privacy-security/encryption.md) 的子菜單。

### 資料治理 {#governance}

資料流利用Experience Platform的內置資料管理功能，防止敏感資料被發送到非HIPAA就緒型服務。 通過在資料流架構中標籤包含敏感資料的特定欄位，您可以對哪些資料欄位可用於特定目的進行細粒度控制。

以下視頻簡要概述了如何在UI中為資料流配置和實施資料使用限制：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在Experience Platform中，您可以 [敏感資料使用標籤](../../data-governance/labels/reference.md#sensitive) 到包含您的組織認為敏感資料的架構和欄位。 例如， `RHD` 標籤用於表示受保護的健康資訊(PHI), `S1` 標籤表示地理位置資料。

>[!NOTE]
>
>有關如何在中應用資料使用標籤的詳細資訊 [!UICONTROL 架構] Experience PlatformUI或資料收集UI中的頁籤，請參見 [架構標籤教程](../../xdm/tutorials/labels.md)。

建立新資料流時，如果所選架構包含敏感資料使用標籤，則只能將資料流配置為將該資料發送到HIPAA就緒的目標。 目前，資料流支援的唯一HIPAA就緒目標是Adobe Experience Platform。 其他目標服務(包括Adobe Target、Adobe Analytics、Adobe Audience Manager、事件轉發和邊緣目標)被禁用，用於包含敏感資料使用標籤的資料流。

如果某個架構正在具有非HIPAA就緒服務的現有資料流中使用，則嘗試向該架構添加敏感資料使用標籤將導致策略違規消息並阻止該操作。 該消息指定觸發違規的資料流，並建議從資料流中刪除任何非HIPAA就緒服務以解決此問題。

### 稽核記錄

在Experience Platform中，可以以審核日誌的形式監視資料流活動。 審計日誌告訴 **誰** 執行 **什麼** 操作和 **何時**&#x200B;以及其他上下文資料，這些上下文資料可以幫助您解決與資料流相關的問題，以幫助您的業務遵守公司資料管理策略和法規要求。

每當用戶建立、更新或刪除資料流時，都會建立審計日誌來記錄操作。 當用戶建立、更新或刪除映射時，也會發生同樣的情況 [資料收集的資料準備](./data-prep.md)。 無論是資料流還是已更新的映射，生成的審核日誌都會在 [!UICONTROL 資料流] 資源類型。

請參閱 [審核日誌](../../landing/governance-privacy-security/audit-logs/overview.md) 有關如何從資料流和其他受支援服務解釋日誌的詳細資訊。

## 後續步驟

本指南概要介紹了資料流及其在資料收集和敏感資料處理中的應用。 有關如何設定新資料流的步驟，請參見 [資料流配置指南](./configure.md)。
