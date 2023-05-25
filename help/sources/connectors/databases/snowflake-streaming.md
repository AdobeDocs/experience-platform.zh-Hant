---
title: Snowflake串流來源聯結器概述
description: 瞭解如何建立來源連線和資料流，以將您的Snowflake執行個體的串流資料擷取到Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# [!DNL Snowflake] 串流來源

>[!IMPORTANT]
>
>* 此 [!DNL Snowflake] 串流來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。
>* 此 [!DNL Snowflake] 已購買Real-Time CDP Ultimate的客戶可在來源目錄中取得串流來源。


Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援來自的串流資料 [!DNL Snowflake] 資料庫。

## 瞭解 [!DNL Snowflake] 串流來源

此 [!DNL Snowflake] 串流來源的運作方式是定期執行SQL查詢來載入資料，並為結果集中的每一列建立輸出記錄。

透過使用 [!DNL Kafka Connect]，則 [!DNL Snowflake] 串流來源會追蹤其從每個表格接收到的最新記錄，以便它可以在下一個反複專案的正確位置開始。 來源使用此功能來篩選資料，並只從每個反複專案的表格中取得更新列。

## 先決條件

以下章節概述在您可從串流傳輸資料之前，必須完成的先決條件步驟。 [!DNL Snowflake] 要Experience Platform的資料庫：

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Snowflake]，您必須提供下列連線屬性：

| 認證 | 說明 |
| --- | --- |
| `account` | 與您的帳戶相關聯的完整帳戶名稱 [!DNL Snowflake] 帳戶。 完全合格 [!DNL Snowflake] 帳戶名稱包含您的帳戶名稱、地區和雲端平台。 例如 `cj12345.east-us-2.azure`。如需帳戶名稱的詳細資訊，請參閱此 [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | 此 [!DNL Snowflake] warehouse會管理應用程式的查詢執行程式。 每個 [!DNL Snowflake] warehouse彼此獨立，將資料帶到Platform時必須個別存取。 |
| `database` | 此 [!DNL Snowflake] 資料庫包含您要帶入Platform的資料。 |
| `username` | 的使用者名稱 [!DNL Snowflake] 帳戶。 |
| `password` | 的密碼 [!DNL Snowflake] 使用者帳戶。 |
| `role` | （選用）可以為使用者針對指定連線提供的自訂定義角色。 如果未提供，則此值預設為 `public`. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Snowflake] 是 `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

如需有關驗證的詳細資訊，請參閱此 [[!DNL Snowflake] 檔案](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### 設定角色設定 {#configure-role-settings}

您必須設定角色的許可權（即使指派了預設的公共角色），以允許來源連線存取相關 [!DNL Snowflake] 資料庫、綱要和表格。 不同的各種許可權 [!DNL Snowflake] 實體如下：

| [!DNL Snowflake] 實體 | 需要角色許可權 |
| --- | --- |
| 倉儲 | 操作，使用 |
| 資料庫 | 使用狀況 |
| 方案 | 使用狀況 |
| 表格 | 選取 |

>[!NOTE]
>
>必須在倉儲的進階設定組態中啟用自動恢復和自動暫停。

有關角色和許可權管理的詳細資訊，請參閱 [[!DNL Snowflake] API參考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## 限制和常見問題 {#limitations-and-frequently-asked-questions}

* 的資料輸送量 [!DNL Snowflake] 來源為每秒2000筆記錄。
* 訂價會依倉庫的有效時間與倉庫大小而有所不同。 對於 [!DNL Snowflake] 來源整合、最小尺寸、X小型倉儲已足夠。 建議啟用自動暫停，以便倉儲在不使用時能夠自行暫停。
* 此 [!DNL Snowflake] 來源每10秒輪詢資料庫新資料。
* 設定選項：
   * 您可以啟用 `backfill` 您的的布林值標幟 [!DNL Snowflake] 建立來源連線時的來源。
      * 如果回填設為true，則timestamp.initial的值會設為0。 這表示會擷取時間戳記欄超過0紀元時間的資料。
      * 如果回填設為false，則timestamp.initial的值會設為–1。 這表示會擷取時間戳記欄大於目前時間（來源開始擷取的時間）的資料。
   * 時間戳記欄的格式應該是： `TIMESTAMP_LTZ` 或 `TIMESTAMP_NTZ`. 如果時間戳記欄設為 `TIMESTAMP_NTZ`，則型別應以UTC時間儲存在資料庫中。

## 後續步驟

以下教學課程提供如何連線您的應用程式 [!DNL Snowflake] 要使用APIExperience Platform的串流來源：

* [從串流資料 [!DNL Snowflake] 要使用流程服務APIExperience Platform的資料庫](../../tutorials/api/create/databases/snowflake-streaming.md)

