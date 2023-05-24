---
keywords: Experience Platform；首頁；熱門主題；表；表；查詢服務；查詢服務；連接到查詢服務；
solution: Experience Platform
title: 將 Tableau 連接至查詢服務
description: 本文檔介紹將Tableau與Adobe Experience Platform查詢服務連接的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 連接 [!DNL Tableau] 查詢服務

本文檔提供了連接資訊 [!DNL Tableau] 與Adobe Experience Platform [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL Tableau] 並熟悉如何導航其介面。 有關 [!DNL Tableau] 在 [官 [!DNL Tableau] 文檔](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

有關如何 [使用Tableau連接到PostgreSQL伺服器](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 可從官方的Tableau網站獲得。 出現連接設定對話框後，在參數欄位中輸入您的平台憑據以與Adobe Experience Platform連接。 下面列出了所需的連接參數清單。

| 連接參數 | 說明 |
|---|---|
| **[!DNL Server]** | SFTP儲存位置的地址。 使用Experience Platform的值 **[!UICONTROL 主機]** 憑據。 |
| **[!DNL Port]:** | 埠 [!DNL Query Service]。 必須使用埠 **80** 或 **5432** 連接 [!DNL Query Service]。 |
| **[!DNL Database]** | 要訪問的資料庫。 使用Experience Platform的值 **[!UICONTROL 資料庫]** 憑據： `prod:all`。 |
| **[!DNL Authentication]:** | 您選擇的驗證用戶身份的方法。 建議您選擇 [!DNL Username and Password] 的子菜單。 |
| **[!DNL Username]** | 這是您的平台組織ID。 使用Experience Platform的值 **[!UICONTROL 用戶名]** 憑據。 ID的格式為 `ORG_ID@AdobeOrg`。 |
| **[!DNL Password]** | 此字母數字字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果要使用非過期憑據，此值是 `technicalAccountID` 和 `credential` 已下載到配置JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非過期憑據的配置JSON檔案是在初始化過程中一次下載，Adobe不保留副本。 |

有關查找用戶名、密碼和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。 要查找憑據，請登錄到 [!DNL Platform]，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

確保您已檢查 **[!UICONTROL 需要SSL]** 框，然後嘗試連接。 查看 [SSL模式文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套資料結構可以被平展，以提高其可用性並減少檢索、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 特徵](../essential-concepts/flatten-nested-data.md) 有關如何在連接到資料庫時激活此設定的說明。

填寫完所有憑據後，確認設定以繼續。 你現在已經和Adobe Experience Platform聯繫了。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Tableau] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀上的指南 [運行查詢](../best-practices/writing-queries.md)。
