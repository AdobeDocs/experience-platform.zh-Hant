---
title: 在Adobe Experience Platform中管理查詢服務工作階段
description: 瞭解管理員如何檢視、監控和結束使用中的查詢服務工作階段，以釋放閒置容量和維護可靠的資料Distiller工作流程。
keywords: Experience Platform；查詢服務；工作階段；工作階段管理；資料Distiller；管理員
solution: Experience Platform
source-git-commit: 1d2a8ef649c4454da7cf0949192b8b1eb3696e5a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# 管理查詢服務工作階段

使用本指南從Adobe Experience Platform使用者介面管理作用中的查詢服務工作階段。 工作階段管理可協助管理員監視沙箱間的同時查詢編輯器工作階段，並在使用者保持工作階段開啟時釋放容量。

## 工作階段管理所需的許可權 {#permissions}

>[!AVAILABILITY]
>
>工作階段管理僅適用於擁有資料Distiller許可權的組織。

>[!IMPORTANT]
>
>此功能適用於管理員。 執行查詢的一般使用者無法管理工作階段。

若要檢視和結束工作階段，您必須屬於具有Data Distiller存取權的組織，且已指派&#x200B;**[!UICONTROL Manage Query Session]**&#x200B;許可權。 沒有必要許可權的使用者可以存取查詢服務，但無法檢視或管理作用中工作階段。

## 檢視作用中工作階段 {#view-active-sessions}

管理員可以檢視貴組織中不同沙箱的所有使用中查詢服務工作階段。 在Experience Platform中，選取左側導覽中的&#x200B;**[!UICONTROL Queries]**&#x200B;以開啟查詢服務工作區，然後選取&#x200B;**[!UICONTROL Admin]**&#x200B;索引標籤以存取工作階段管理。

![已選取[管理員]索引標籤的查詢服務工作區。 會顯示「工作階段管理」表格，並列出您組織中多個沙箱中的作用中和非作用中工作階段。](../images/ui/session-management/session-management-admin-tab.png)

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

**[!UICONTROL Inactive]**&#x200B;表示使用者未主動執行查詢；這些工作階段可以結束。 **[!UICONTROL Active]**&#x200B;表示查詢目前正在執行；**[!UICONTROL End session]**&#x200B;控制項在查詢執行完成前無法使用。

### 閒置時間和剩餘工作階段時間

閒置時間顯示工作階段開啟而未與使用者互動的時間。 剩餘工作階段時間表示在系統自動關閉工作階段之前，工作階段可以保持開啟的時間長度。 工作階段會在允許的最長持續時間（閒置兩個小時）後自動過期。 此持續時間由系統定義，無法設定。

## 結束閒置工作階段 {#end-idle-sessions}

您可以結束閒置工作階段，以釋出其他使用者的同時工作階段容量。 當使用者不再主動工作時，請考慮以高閒置時間結束工作階段。

從工作階段管理表格中，選取&#x200B;**[!UICONTROL End session]**&#x200B;以選擇要結束的非作用中工作階段。

![工作階段管理資料表顯示非使用中工作階段，並反白標示結束工作階段。](../images/ui/session-management/end-session.png)

確認對話方塊會出現，以防止意外終止。 在對話方塊中選取&#x200B;**[!UICONTROL End session]**&#x200B;以確認動作。

![結束工作階段確認對話方塊顯示警告訊息，並反白顯示結束工作階段。](../images/ui/session-management/end-session-confirmation-dialog.png)

工作階段結束後，工作階段會從表格中移除，容量會立即可用，並記錄動作以進行稽核。

>[!NOTE]
>
>無法結束狀態為&#x200B;**[!UICONTROL Active]**&#x200B;的工作階段。 此保護措施可避免中斷進行中的工作負載。

## 終止後的工作階段行為 {#session-behavior-after-termination}

管理員結束工作階段時，受影響使用者的程式碼會保留在編輯器中而不會遺失工作。 如果使用者在終止後嘗試執行查詢，系統會偵測到結束的工作階段、自動重新建立連線，並保持「查詢編輯器」內容不變。

此行為可確保使用者不會遺失在編輯器中撰寫的工作，並在建立新工作階段後繼續進行。

## 工作階段管理的稽核記錄 {#audit-logs}

系統會記錄工作階段管理動作，以提供可見度和責任感。 稽核記錄會記錄工作階段ID、工作階段結束的使用者、執行動作的管理員，以及動作的時間。

使用稽核記錄檢閱工作階段終止歷程記錄並調查非預期的中斷情形。

如需有關檢視稽核記錄的詳細資訊，請參閱[查詢服務稽核記錄指南](../data-governance/audit-log-guide.md)。

## 後續步驟 {#next-steps}

請考慮下列資源，以擴充您對查詢服務和資料Distiller的使用：

* [瞭解使用者如何在查詢編輯器使用手冊中建立和執行查詢](user-guide.md)
* [使用排程查詢監視檔案監視排程工作負載](monitor-queries.md)

