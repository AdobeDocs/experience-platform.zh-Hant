---
title: 錯誤處理
description: 瞭解在Repartor API中如何處理錯誤。
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 錯誤處理

當調用Reactor API時出現問題時，可能會以下列方式之一返回錯誤：

* **立即錯誤**:當執行導致立即錯誤的請求時，API將返回錯誤響應，HTTP狀態反映所發生的錯誤的一般類型。
* **延遲錯誤**:當執行導致延遲錯誤（如非同步活動）的API請求時，API可返回錯誤 `meta.status_details` 的下界。

## 錯誤格式

錯誤響應旨在符合 [JSON:API錯誤規範](http://jsonapi.org/format/#errors)並一般遵循以下結構：

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 問題特定發生情況的唯一標識符。 |
| `status` | 適用於此問題的HTTP狀態代碼，以字串值表示。 |
| `code` | 特定於應用程式的錯誤代碼，表示為字串值。 |
| `title` | 一個簡短的、人類可讀的關於 **不改變** 從發生到發生，但本地化除外。 |
| `detail` | 針對此問題發生的可人為閱讀的解釋。 像 `title`，此欄位的值可以本地化。 |
| `source` | 包含對錯誤源的引用的對象，可選地包括以下任何成員：<ul><li>`pointer`:a [JSON指針(RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) 引用請求文檔中關聯實體的字串(如 `/data` 主資料對象，或 `/data/attributes/title` )。</li></ul> |
| `meta` | 包含有關錯誤的非標準元資料的對象。 |

{style="table-layout:auto"}

## 錯誤引用

下表列出了API可返回的不同錯誤。

| 錯誤標題 | 說明 |
| --- | --- |
| `authentication-failure` | 您的IMS訪問令牌無效。 您可以通過重新登錄來獲取新的訪問令牌。 或者對於技術帳戶，生成新的JWT並交換IMS訪問令牌。 |
| `connection-refused` | 無法建立到伺服器的連接。 |
| `decrypt-bad-passphrase` | 無法使用提供的密碼來解密資料。 |
| `decrypt-failed` | 無法使用提供的私鑰解密資料。 確保密鑰在本地工作，並且空格已修剪。 |
| `decrypt-no-data` | 沒有私鑰，無法解密資料。 請提供加密的私鑰。 |
| `delegate-descriptor-unresolved` | 擴展未提供此委託描述符的預期定義。 可能需要更新擴展。 |
| `deleted-resources` | 您嘗試添加到庫的資源已被刪除。 |
| `environment-in-use` | 一次只能將環境分配給一個庫。 選項1是選擇不同的環境。 選項2是通過將庫移到其他環境或刪除庫來釋放此環境。 |
| `environment-required` | 在建立生成之前，必須為庫分配一個環境。 |
| `extension-not-found` | 定義資料元素或規則元件的擴展不包含在庫中。 確保已將所有必需的擴展添加到庫中。 |
| `extension-package-path-error` | extension.json中定義的路徑構造不正確。 |
| `extension-package-transform-definition-error` | 您為對象屬性定義了無效的轉換。 每個對象屬性都可以定義一個轉換，它必須是檔案轉換或函式轉換。 |
| `extension-package-zip-error` | 解壓縮ExtensionPackage或壓縮要分發的檔案時出錯。 |
| `host-in-use` | 如果一個或多個環境正在使用主機，則不能刪除該主機。 |
| `host-required` | 分配給此庫的環境沒有有效的主機。 檢查為庫分配的環境。 然後為該環境分配一個有效的主機。 |
| `host-type-error` | 只有SFTP主機需要先驗證憑據才能使用，因此預測僅可用於該主機類型。 |
| `illegal-custom-code-transform` | 不允許使用customCode轉換。 請指定函式或檔案轉換。 |
| `ims-not-authorized` | 授權帳戶時發生未知錯誤。 請稍後再試。 |
| `ims-session-error` | 登錄會話有問題。 請註銷並重新登錄。 |
| `internal-error` | 發生內部錯誤。 請稍候，然後重試。 如果問題仍然存在，請與「Client Care（客戶保護）」聯繫。 |
| `invalid-data_element` | 無法將無效的資料元素添加到庫。 |
| `invalid-embed_code` | 這不是有效的嵌入代碼，或者您正嘗試將其連結到開發或暫存環境。 動態Tag Management(DTM)嵌入代碼只能連結到生產環境。 |
| `invalid-extension` | 無法將無效的擴展添加到庫。 |
| `invalid-extension_package_id` | 您只能修改擴展包的某些對象屬性。 您試圖修改其中一個不允許的。 |
| `invalid-new-owner-org-id` | 您嘗試分配的組織ID不是有效的組織ID。 |
| `invalid-org` | 您的活動組織無權訪問API。 檢查您使用的組織是否正確。 |
| `invalid-rule` | 無法將無效規則添加到庫。 |
| `invalid-settings-syntax` | 分析設定JSON時遇到語法錯誤。 |
| `library-file-not-found` | 在zip包內找不到extension.json中定義的所需檔案。 |
| `minification-error` | 由於代碼無效，無法編譯代碼。 |
| `multiple-revisions` | 庫中只能包含每個資源的一個修訂版本。 |
| `no-available-orgs` | 此用戶帳戶不屬於具有標籤訪問權限的產品配置檔案。 使用Admin Console將此用戶添加到具有標籤權限的產品配置檔案中。 |
| `not-authorized` | 此用戶帳戶沒有執行此操作所需的權限。 |
| `not-found` | 找不到記錄。 驗證您嘗試檢索的對象的ID。 |
| `not-unique` | 您嘗試使用的名稱已在使用中。 對於此資源，「name」屬性必須唯一。 |
| `public-release-not-authorized` | 擴展的公開發佈由 `launch-ext-dev@adobe.com`。 查看上的文檔 [釋放擴展](../../extension-dev/submit/release.md) 的子菜單。 |
| `read-only` | 此資源為只讀，無法修改。 |
| `session-timeout` | 用戶會話已過期。 請註銷並重新登錄。 |
| `sftp-authentication-failed` | SFTP連接的身份驗證失敗。 |
| `sftp-connection-timeout` | SFTP連接超時。 |
| `sftp-exception` | 使用SFTP連接到伺服器時遇到異常。 |
| `sftp-status-exception` | 嘗試與伺服器通信時遇到SFTP異常。 |
| `socket-error` | 嘗試與伺服器通信時遇到套接字錯誤。 |
| `ssh-disconnect` | SSH會話已斷開。 |
| `timeout-error` | 與伺服器的連接超時。 |
| `unknown-error` | 發生錯誤。 您可以稍後再試，或給「客戶服務」打電話，解釋您在發生問題時正在執行的操作。 |
| `unsupported-custom-code-language` | 提供的自定義代碼語言不受支援。 |
| `upgraded-extension-required` | 安裝擴展升級後，必須將其包括在所有庫中，直到升級到生產。 唯一的例外是尚未發佈擴展。 |
| `upstream-build-required` | 在構建上游庫之前，需要成功構建上游庫。 |

{style="table-layout:auto"}
