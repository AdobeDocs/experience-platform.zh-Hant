---
title: CMK警示解決方式參考
description: 識別、疑難排解及解決Adobe Experience Platform中客戶自控金鑰(CMK)設定錯誤所觸發的常見警報。 使用本指南來遵循清楚的逐步指示，並還原安全的金鑰存取。
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# CMK警示解決方式參考

使用本指南來疑難排解及解決Adobe Experience Platform中客戶自控金鑰(CMK)設定錯誤所觸發的警報。 它可協助系統管理員與實作專家找出原因並套用解決方案，以恢復安全存取。

## 警示類別 {#categories}

以下小節概述Adobe Experience Platform中客戶自控金鑰(CMK)問題可能觸發的警報型別：

- [金鑰存取已停用](#key-access-disabled)
- [金鑰存取失敗](#key-access-failure)
- [警示通知](#alert-notification)

## 金鑰存取已停用 {#key-access-disabled}

此警報表示Adobe Experience Platform無法存取已設定的CMK，因為金鑰已停用或因其設定而無法存取。 在這種情況下，系統會將狀況視為有意移除關鍵存取權。

### 發生時間

當Azure Key Vault中的加密金鑰處於停用狀態、遭到刪除或設定錯誤，導致無法在平台作業期間進行存取時，就會觸發此警報。

### 可能的原因

發生此警示的常見原因如下：

- 金鑰已手動停用。
- 主要操作(wrapKey/unwrapKey)已移除。
- 金鑰啟用日期設定在未來。
- 金鑰到期日是過去時間。
- 已刪除金鑰。
- 已移除或變更「多租使用者應用程式」許可權。
- 已刪除多租使用者應用程式。
- 已變更MultiTenant App屬性。
- 金鑰儲存庫已刪除或無法再存取。

### 解決方法

+++如果金鑰已停用

1. 導覽至包含CMK的[Azure金鑰儲存庫](https://portal.azure.com/)。
2. 選取與Adobe Experience Platform相關聯的金鑰。
3. 確認金鑰的狀態已設定為&#x200B;**已啟用**。
4. 如果金鑰已停用，請使用Azure入口網站或CLI命令`az keyvault key enable`啟用它。

>[!NOTE]
>
>為您的Azure環境自訂此命令。

+++

+++如果重要作業已變更

1. 重新新增`wrapKey`和`unwrapKey`許可權至金鑰。

>[!NOTE]
>
>金鑰的所有設定（包括啟用和到期日）都必須有效，金鑰才能正常運作。

+++

+++若啟用或到期日設定錯誤

1. 將啟用日期設為過去或現在。
2. 將到期日設為未來的日期。

+++

+++如果索引鍵已刪除

1. 請確定Azure Key Vault中已啟用軟刪除。
2. 在Azure入口網站或CLI中導覽至「管理已刪除的金鑰」。
3. 從可變刪除專案清單中選取已刪除的金鑰。
4. 按一下&#x200B;**復原**&#x200B;以還原金鑰。

+++

+++如果移除或變更MultiTenant應用程式許可權

1. 還原多租使用者應用程式的正確許可權。
2. 確定已授與下列許可權： `Key Vault Crypto Service Encryption User`

+++

+++若多租使用者應用程式已刪除

這是重大變更。 您必須聯絡Adobe以還原或重新產生MultiTenant應用程式。

+++

+++若多租使用者應用程式設定已變更

1. 還原與多租使用者應用程式關聯之屬性的變更。

+++

+++如果金鑰儲存庫已刪除

1. 確認Azure中已啟用軟刪除。
2. 瀏覽至入口網站或CLI中的「管理已刪除的儲存庫」。
3. 在保留期間（7-90天）內復原已刪除的儲存庫。
4. 如果已停用清除保護，您仍可復原儲存庫。

>[!NOTE]
>
>如果未正確設定軟刪除或清除保護，金鑰或儲存庫可能無法復原。

+++

## 金鑰存取失敗 {#key-access-failure}

此警報表示Adobe Experience Platform無法存取CMK，因為網路層級或設定型拒絕存取。

>[!IMPORTANT]
>
>這被視為可復原的錯誤。 在此案例中，資料在SLA下&#x200B;**未**&#x200B;清除。

### 發生時間

此警報通常會在金鑰儲存庫防火牆未設定為允許Adobe CMK存取或身分型存取失敗時觸發。

### 可能的原因

- 金鑰儲存庫防火牆正在封鎖Adobe的靜態IP (`20.88.123.53`)
- 金鑰已不存在於預期的位置
- 缺少Adobe多租使用者應用程式的許可權
- 金鑰儲存庫已刪除或設定錯誤
- 多租使用者應用程式的物件ID已變更

### 解決方法

+++如果金鑰儲存庫或金鑰已不存在

1. 確認金鑰儲存庫和加密金鑰仍然存在。
2. 如果金鑰已刪除，請依照「金鑰存取已停用」下的軟刪除復原步驟操作。

+++

+++如果MultiTenant應用程式許可權遺失或變更

1. 確認Adobe MultiTenant應用程式具有下列許可權：
   - 索引鍵上的`get`、`wrapKey`和`unwrapKey`。
2. 檢查多租使用者應用程式的物件識別碼是否正確。 如果已變更，則重新套用許可權。

+++

+++如果防火牆封鎖Adobe

1. 檢閱Azure Key Vault中的防火牆規則。
2. 請確定它們允許從Adobe的靜態IP存取： `20.88.123.53`。

>[!NOTE]
>
>即使擁有正確的許可權，封鎖的IP也會阻止金鑰存取。

+++

## 警示通知 {#alert-notification}

此警報可作為CMK設定或不符合已知失敗型別的存取異常的一般通知。

>[!NOTE]
>
>此警報可能反映內部錯誤、新的設定錯誤或意外狀況。

### 發生時間

當Adobe CMK在金鑰存取或監視期間偵測到未知、不支援或新問題時，此警報便會出現。

### 可能的原因

- 無法預期的防火牆/網路狀況
- 預先定義的警示型別未涵蓋的金鑰或儲存庫變更
- 內部Adobe網路中斷
- Adobe先前未發生設定錯誤

### 解決方法

+++如果原因不明或不明確

1. 檢閱警示訊息以瞭解任何內容詳細資訊。
2. 檢查防火牆、儲存庫和金鑰設定，以取得最近的變更。
3. 如果找不到明確的原因，請聯絡Adobe支援以取得指引。
4. 監視日誌和系統行為以識別模式。

+++

## 後續步驟

若要瞭解如何觸發警示以及如何設定[!DNL Azure] CMK的IP允許清單，請參閱[設定Azure CMK的警示和IP允許清單](./azure/alerts-and-ip-access.md)指南。
