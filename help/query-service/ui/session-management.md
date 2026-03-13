---
title: 在Adobe Experience Platform中管理查詢服務工作階段
description: 瞭解管理員如何檢視、監控和結束使用中的查詢服務工作階段，以釋放閒置容量和維護可靠的資料Distiller工作流程。
keywords: Experience Platform；查詢服務；工作階段；工作階段管理；資料Distiller；管理員
solution: Experience Platform
badgeLimitedAvailability: label="有限可用性" type="Informative"
exl-id: f986177a-9a46-4fc6-927e-98b6b7dc8cfe
source-git-commit: 2117b7ad0f507b5a35595d702cb8a70e2e09f39d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# 管理查詢服務工作階段

>[!AVAILABILITY]
>
>查詢服務的工作階段管理目前使用受限，僅供擁有&#x200B;**資料Distiller**&#x200B;權益的組織使用。 若要要求存取權，請聯絡您的Adobe客戶團隊。

使用本指南從Adobe Experience Platform使用者介面管理作用中的查詢服務工作階段。 工作階段管理可協助管理員監視沙箱間的同時查詢編輯器工作階段，並在使用者保持工作階段開啟時釋放容量。

## 工作階段管理所需的許可權 {#permissions}

>[!IMPORTANT]
>
>此功能適用於管理員。 執行查詢的一般使用者無法管理工作階段。

若要檢視和結束工作階段，您必須屬於具有Data Distiller存取權的組織，且已指派&#x200B;**[!UICONTROL Manage Query Session]**&#x200B;許可權。 沒有必要許可權的使用者可以存取查詢服務，但無法檢視或管理作用中工作階段。

## 檢視作用中工作階段 {#view-active-sessions}

管理員可以查看組織中各個沙箱中所有活動的查詢服務會話。 在Experience Platform中，在左側導航中選擇&#x200B;**[!UICONTROL Queries]**&#x200B;以開啟查詢服務工作區，然後選擇&#x200B;**[!UICONTROL Admin]**&#x200B;頁籤以訪問會話管理。

![選中「管理」頁籤的「查詢服務」工作區。 將顯示「會話管理」表，並列出組織中多個沙箱中的活動會話和非活動會話。](../images/ui/session-management/session-management-admin-tab.png)

作業階段管理表格會即時自動更新，並列出目前耗用指定給您組織之「查詢服務」並行作業階段產能的所有作業階段。 每一列代表在查詢編輯器中開啟的單一工作階段。

## 工作階段狀態和閒置時間 {#session-status}

階段作業表格提供的資訊可協助您決定是否可安全地結束階段作業。

| 欄 | 說明 |
| --- | --- |
| 使用者 ID | 擁有工作階段之使用者的Adobe ID |
| 使用者名稱 | 與Adobe ID相關聯的名稱 |
| 沙箱 | 表示執行工作階段的沙箱 |
| 工作階段狀態 | 顯示工作階段為&#x200B;**[!UICONTROL Active]**&#x200B;或&#x200B;**[!UICONTROL Inactive]** |
| 閒置時間 | 顯示開啟工作階段而沒有互動的時間 |
| 剩餘工作階段時間 | 表示在自動到期之前，工作階段可以保持開啟的時間長度 |

### 工作階段狀態

**[!UICONTROL Inactive]**&#x200B;表示用戶未主動運行查詢；這些會話可以結束。 **[!UICONTROL Active]**&#x200B;表示查詢當前正在運行；在查詢執行完成之前，**[!UICONTROL End session]**&#x200B;控制項不可用。

### 空閒時間和剩餘會話時間

空閒時間顯示會話在沒有用戶交互的情況下已開啟多長時間。 剩餘工作階段時間表示在系統自動關閉工作階段之前，工作階段可以保持開啟的時間長度。 工作階段會在允許的最長持續時間（閒置兩個小時）後自動過期。 此持續時間由系統定義，無法設定。

## 結束閒置工作階段 {#end-idle-sessions}

您可以結束閒置工作階段，以釋出其他使用者的同時工作階段容量。 當使用者不再主動工作時，請考慮以高閒置時間結束工作階段。

從工作階段管理表格中，選取&#x200B;**[!UICONTROL End session]**&#x200B;以選擇要結束的非作用中工作階段。

![工作階段管理資料表顯示非使用中工作階段，並反白標示結束工作階段。](../images/ui/session-management/end-session.png)

確認對話方塊會出現，以防止意外終止。 在對話方塊中選取&#x200B;**[!UICONTROL End session]**&#x200B;以確認動作。

![結束工作階段確認對話方塊顯示警告訊息，並反白顯示結束工作階段。](../images/ui/session-management/end-session-confirmation-dialog.png)

工作階段結束後，工作階段會從表格中移除，容量會立即可用，並記錄動作以進行稽核。

>[!NOTE]
>
>無法結束狀態為&#x200B;**[!UICONTROL Active]**&#x200B;的會話。 此保護措施可避免中斷進行中的工作負載。

## 終止後的工作階段行為 {#session-behavior-after-termination}

管理員結束工作階段時，受影響使用者的程式碼會保留在編輯器中而不會遺失工作。 如果用戶嘗試在終止後運行查詢，則系統會檢測結束的會話，自動重新建立連接，並保持查詢編輯器內容不變。

此行為確保用戶不會丟失在編輯器中編寫的工作，並且一旦建立新會話，就可以繼續。

## 會話管理的審核日誌 {#audit-logs}

系統記錄會話管理操作以提供可見性和可問責性。 稽核記錄會記錄工作階段ID、工作階段結束的使用者、執行動作的管理員，以及動作的時間。

使用稽核記錄檢閱工作階段終止歷程記錄並調查非預期的中斷情形。

如需有關檢視稽核記錄的詳細資訊，請參閱[查詢服務稽核記錄指南](../data-governance/audit-log-guide.md)。

## 後續步驟 {#next-steps}

請考慮下列資源，以擴充您對查詢服務和資料Distiller的使用：

* [瞭解使用者如何在查詢編輯器使用手冊中建立和執行查詢](user-guide.md)
* [使用排程查詢監視檔案監視排程工作負載](monitor-queries.md)
