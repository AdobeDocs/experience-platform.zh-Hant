---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供從Sources工作區檢視現有資料流的步驟。
solution: Experience Platform
title: 監視資料流
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 791ad61f2f28da03ef3e5cb5efdd89154e9b1a0b
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---


# 在UI中監視目標的資料流

目標可讓您將Adobe Experience Platform中的資料啟動給無數外部合作夥伴。 本教學課程提供如何使用Experience Platform使用者介面監控目的地資料流的指示。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [目標](../../destinations/home.md):目標是與常用應用程式預先建立的整合，可讓跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例的平台資料順暢啟動。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 監視資料流

在「平 **[!UICONTROL 台]** 」UI的「目標」工作區中，導覽至「瀏覽 **** 」標籤並選取您要檢視的目標名稱。

![](../assets/ui/monitor-destinations/select-destination.png)

將顯示現有資料流清單。 本頁列出了可查看的資料流，包括有關其目標、用戶名、資料流數和狀態的資訊。

如需狀態的詳細資訊，請參閱下表：

| 狀態 | 說明 |
| ------ | ----------- |
| 啟用 | 狀 `Enabled` 態表示資料流處於活動狀態，並正在根據提供的時間表接收資料。 |
| 停用 | 狀 `Disabled` 態表示資料流處於非活動狀態且未吸收任何資料。 |
| 正在處理 | 狀 `Processing` 態表示資料流尚未激活。 建立新資料流後，通常會立即出現此狀態。 |
| 錯誤 | 狀態 `Error` 表示資料流的激活過程已中斷。 |

## [!UICONTROL 資料流運行]

「數 [!UICONTROL 據流運行] 」頁籤提供資料流運行到批處理目標的度量資料。 會顯示個別執行及其特定度量的清單，以及下列描述檔記錄總計：

- **[!UICONTROL 已激活配置檔案記錄]**:為啟動而建立或更新的描述檔記錄總計。
- **[!UICONTROL 已略過描述檔記錄]**: 根據描述檔退出或遺失屬性，跳過以進行啟動的描述檔記錄總計。

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>根據目標資料流的調度頻率生成資料流運行。 會針對套用至區段的每個合併原則執行個別的資料流。

要查看特定資料流運行的詳細資訊，請從清單中選擇運行的開始時間。 資料流運行的詳細資訊頁包含其他資訊，如處理的資料大小和錯誤診斷詳細資訊中發生的所有錯誤的清單。

![](../assets/ui/monitor-destinations/dataflow.png)