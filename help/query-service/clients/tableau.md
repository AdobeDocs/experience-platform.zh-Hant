---
keywords: Experience Platform；首頁；熱門主題；tableau;Tableau；查詢服務；查詢服務；連線至查詢服務；
solution: Experience Platform
title: 將 Tableau 連接至查詢服務
description: 本檔案會逐步說明將Tableau與Adobe Experience Platform Query Service連線的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] 查詢服務

本文檔提供連接的資訊 [!DNL Tableau] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Tableau] 並熟悉如何導覽其介面。 有關 [!DNL Tableau] 可在 [官方 [!DNL Tableau] 檔案](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

如何 [連接到具有Tableau的PostgreSQL伺服器](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 可從官方的Tableau網站取得。 連線設定的對話方塊出現後，請在參數欄位中輸入您的Platform憑證，以便與Adobe Experience Platform連線。 下面列出了所需的連接參數清單。

| 連線參數 | 說明 |
|---|---|
| **[!DNL Server]** | SFTP儲存位置的位址。 使用Experience Platform的值 **[!UICONTROL 主機]** 憑據。 |
| **[!DNL Port]:** | 的埠 [!DNL Query Service]. 必須使用埠 **80** 或 **5432** 連線 [!DNL Query Service]. |
| **[!DNL Database]** | 要訪問的資料庫。 使用Experience Platform的值 **[!UICONTROL 資料庫]** 憑據： `prod:all`. |
| **[!DNL Authentication]:** | 您選擇的驗證用戶身份的方法。 建議您選取 [!DNL Username and Password] 從下拉式功能表的可用選項。 |
| **[!DNL Username]** | 這是您的平台組織ID。 使用Experience Platform的值 **[!UICONTROL 使用者名稱]** 憑據。 ID將採用 `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果您想使用非到期憑證，此值是 `technicalAccountID` 和 `credential` 下載到設定JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非到期憑證的設定JSON檔案是初始化期間的一次性下載，Adobe不會保留副本。 |

有關查找用戶名、密碼和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找憑證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

請確定您已核取 **[!UICONTROL 需要SSL]** 框，然後嘗試連接。 請參閱 [SSL模式檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以改善其可用性，並減少擷取、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 功能](../essential-concepts/flatten-nested-data.md) 有關在連接到資料庫時如何激活此設定的說明。

填入所有憑證後，請確認您的設定以繼續。 您現在已與Adobe Experience Platform連線。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Tableau] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢](../best-practices/writing-queries.md).
