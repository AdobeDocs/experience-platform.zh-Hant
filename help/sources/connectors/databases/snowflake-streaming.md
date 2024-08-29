---
title: Snowflake串流Source聯結器概述
description: 瞭解如何建立來源連線和資料流，以將您的Snowflake執行個體中的串流資料擷取到Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: e8ab39ce085a95eac898f65667706b71bdadd350
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# [!DNL Snowflake]串流來源

>[!IMPORTANT]
>
>* [!DNL Snowflake]串流來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。
>* 已購買Real-time Customer Data Platform Ultimate的使用者可在API中使用[!DNL Snowflake]串流來源。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從[!DNL Snowflake]資料庫串流資料。

## 瞭解[!DNL Snowflake]串流來源

[!DNL Snowflake]串流來源的運作方式是定期執行SQL查詢來載入資料，並為結果集中的每一列建立輸出記錄。

藉由使用[!DNL Kafka Connect]，[!DNL Snowflake]串流來源會追蹤它從每個資料表收到的最新記錄，以便它可以在下一個反複專案的正確位置開始。 來源使用此功能來篩選資料，並只從每個疊代的表格中取得更新的列。

## 先決條件

以下章節概述從[!DNL Snowflake]資料庫將資料串流到Experience Platform之前要完成的先決條件步驟：

### 更新您的IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources)頁面。

以下檔案提供如何使用API或使用者介面將[!DNL Amazon Redshift]連線到Platform的資訊：

### 收集必要的認證

若要讓[!DNL Flow Service]與[!DNL Snowflake]連線，您必須提供下列連線屬性：

| 認證 | 說明 |
| --- | --- |
| `account` | [!DNL Snowflake]帳戶的完整帳戶識別碼（帳戶名稱或帳戶定位器）已附加尾碼`snowflakecomputing.com`。 帳戶識別碼可以是不同的格式： <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com （例如`acme-abc12345.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}.snowflakecomputing.com （例如`acme12345.ap-southeast-1.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}。{CLOUD}.snowflakecomputing.com （例如`acme12345.east-us-2.azure.snowflakecomputing.com`）</li></ul> 如需詳細資訊，請閱讀[[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料傳送至Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]資料庫包含您要帶入Platform的資料。 |
| `username` | [!DNL Snowflake]帳戶的使用者名稱。 |
| `password` | [!DNL Snowflake]使用者帳戶的密碼。 |
| `role` | （選用）可以為使用者針對指定連線提供的自訂定義角色。 如果未提供，此值會預設為`public`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Snowflake]的連線規格識別碼為`51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

{style="table-layout:auto"}

### 設定角色設定 {#configure-role-settings}

您必須設定角色的許可權（即使已指派預設公用角色），以允許來源連線存取相關[!DNL Snowflake]資料庫、結構描述和表格。 不同[!DNL Snowflake]個實體的各種許可權如下：

| [!DNL Snowflake]實體 | 需要角色許可權 |
| --- | --- |
| 倉儲 | 操作，使用 |
| 資料庫 | 使用狀況 |
| 綱要 | 使用狀況 |
| 表格 | 選取 |

>[!NOTE]
>
>您必須在倉儲的進階設定組態中啟用自動恢復和自動暫停。

如需角色與許可權管理的詳細資訊，請參閱[[!DNL Snowflake] API參考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>)。

## 限制和常見問答 {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake]來源的資料輸送量為每秒2000筆記錄。
* 訂價會因倉儲的有效時間長短及倉儲大小而有所不同。 對於[!DNL Snowflake]來源整合，最小大小x小型倉儲就足夠了。 建議啟用自動暫停，以便倉儲在不使用時能夠自行暫停。
* [!DNL Snowflake]來源每10秒輪詢資料庫是否有新資料。
* 設定選項：
   * 建立來源連線時，您可以為[!DNL Snowflake]來源啟用`backfill`布林值標幟。
      * 如果回填設為true，則timestamp.initial的值會設為0。 這表示會擷取時間戳記欄超過0紀元時間的資料。
      * 如果回填設為false，則timestamp.initial的值會設為–1。 這表示會擷取時間戳記欄大於目前時間（來源開始擷取的時間）的資料。
   * 時間戳記資料行的格式應該是： `TIMESTAMP_LTZ`或`TIMESTAMP_NTZ`。 如果時間戳記資料行設為`TIMESTAMP_NTZ`，則儲存值的對應時區應透過`timezoneValue`引數傳遞。 如果未提供，此值將預設為UTC。
      * `TIMESTAMP_TZ`不能用於時間戳記資料行或對應中。

## 後續步驟

下列教學課程提供如何使用API將您的[!DNL Snowflake]串流來源連線至Experience Platform的步驟：

* [使用Flow Service API從 [!DNL Snowflake] 資料庫串流資料以Experience Platform](../../tutorials/api/create/databases/snowflake-streaming.md)
* [從 [!DNL Snowflake] 資料庫串流資料，以使用Experience Platform使用者介面中的來源工作區進行Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
