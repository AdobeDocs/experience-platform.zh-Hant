---
title: 錯誤處理
description: 了解在Reactor API中如何處理錯誤。
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 錯誤處理

當呼叫Reactor API時發生問題時，可能會透過下列其中一種方式傳回錯誤：

* **立即錯誤**:執行會導致立即錯誤的要求時，API會傳回錯誤回應，其HTTP狀態會反映所發生的一般錯誤類型。
* **延遲錯誤**:執行API要求而導致延遲錯誤（例如非同步活動）時，API可能會在 `meta.status_details` 相關資源。

## 錯誤格式

錯誤回應旨在符合 [JSON:API錯誤規格](http://jsonapi.org/format/#errors)，並一般遵循下列結構：

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
| `id` | 此問題特定出現情況的唯一標識符。 |
| `status` | 適用於此問題的HTTP狀態代碼，以字串值表示。 |
| `code` | 應用程式專屬的錯誤碼，以字串值表示。 |
| `title` | 人類看得懂的簡短問題摘要 **不應變更** 從發生到發生，但本地化用途除外。 |
| `detail` | 此問題發生時人類看得懂的解釋。 贊 `title`，此欄位的值可以本地化。 |
| `source` | 包含對錯誤源的引用的對象，可選地包括以下任一成員：<ul><li>`pointer`:a [JSON指標(RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) 引用請求文檔中關聯實體的字串(如 `/data` 主要資料物件，或 `/data/attributes/title` )。</li></ul> |
| `meta` | 包含錯誤相關非標準中繼資料的物件。 |

{style="table-layout:auto"}

## 錯誤參考

下表列出API可傳回的不同錯誤。

| 錯誤標題 | 說明 |
| --- | --- |
| `authentication-failure` | 您的IMS存取權杖無效。 您可以重新登入以取得新的存取權杖。 或技術帳戶，產生新JWT並交換IMS存取權杖。 |
| `connection-refused` | 無法建立與伺服器的連接。 |
| `decrypt-bad-passphrase` | 無法使用提供的密碼來解密資料。 |
| `decrypt-failed` | 無法使用提供的私鑰解密資料。 請確定金鑰可在本機運作，且空格已修剪。 |
| `decrypt-no-data` | 若沒有私密金鑰，則無法解密資料。 請提供加密的私鑰。 |
| `delegate-descriptor-unresolved` | 擴展未提供此委派描述符的預期定義。 可能需要更新擴充功能。 |
| `deleted-resources` | 您嘗試新增至程式庫的資源已刪除。 |
| `environment-in-use` | 環境一次只能指派給一個程式庫。 選項1是選擇不同的環境。 選項2是將程式庫移至其他環境或刪除程式庫，借此釋放此環境。 |
| `environment-required` | 您必須先指派環境，才能建立組建。 |
| `extension-not-found` | 定義資料元素或規則元件的擴充功能不包含在程式庫中。 請確定所有必要的擴充功能均已新增至您的程式庫。 |
| `extension-package-path-error` | extension.json中定義的路徑的建構不正確。 |
| `extension-package-transform-definition-error` | 您已為對象屬性定義了無效的轉換。 每個對象屬性都可以定義一個轉換，它必須是檔案轉換或函式轉換。 |
| `extension-package-zip-error` | 解壓縮ExtensionPackage或壓縮檔案以進行分發時出錯。 |
| `host-in-use` | 如果一個或多個環境正在使用該主機，則不能刪除該主機。 |
| `host-required` | 指派給此程式庫的環境沒有有效的主機。 檢查指派給程式庫的環境。 然後為該環境分配有效的主機。 |
| `host-type-error` | 只有SFTP主機需要先驗證憑證才能使用，因此預先測試僅適用於該主機類型。 |
| `illegal-custom-code-transform` | 您不得使用customCode轉換。 請指定函式或檔案轉換。 |
| `ims-not-authorized` | 授權您的帳戶時出現未知錯誤。 請稍後再試。 |
| `ims-session-error` | 登入工作階段有問題。 請註銷並重新登錄。 |
| `internal-error` | 發生內部錯誤。 請稍候幾分鐘，然後重試。 如果問題仍然存在，請聯絡客戶服務。 |
| `invalid-data_element` | 無法將無效的資料元素添加到庫中。 |
| `invalid-embed_code` | 這不是有效的內嵌程式碼，或您正嘗試將其連結至開發或測試環境。 動態Tag Management(DTM)內嵌程式碼只能連結至生產環境。 |
| `invalid-extension` | 無法將無效的擴充功能新增至程式庫。 |
| `invalid-extension_package_id` | 您只能修改擴展包的某些對象屬性。 您嘗試修改其中一個不允許的。 |
| `invalid-new-owner-org-id` | 您嘗試指派的組織ID不是有效的組織ID。 |
| `invalid-org` | 您的作用中組織無法存取API。 檢查您使用的組織是否正確。 |
| `invalid-rule` | 無法將無效規則新增至程式庫。 |
| `invalid-settings-syntax` | 剖析設定JSON時遇到語法錯誤。 |
| `library-file-not-found` | 在zip套件內找不到extension.json中定義的必要檔案。 |
| `minification-error` | 由於代碼無效，無法編譯代碼。 |
| `multiple-revisions` | 程式庫中只能包含每個資源的一個修訂版本。 |
| `no-available-orgs` | 此使用者帳戶不屬於可存取標籤的產品設定檔。 使用Admin Console將此使用者新增至具有標籤權限的產品設定檔。 |
| `not-authorized` | 此使用者帳戶沒有執行此動作的必要權限。 |
| `not-found` | 找不到記錄。 驗證您嘗試擷取的物件ID。 |
| `not-unique` | 您嘗試使用的名稱已在使用中。 對於此資源，&#39;name&#39;屬性必須是唯一的。 |
| `public-release-not-authorized` | 擴充功能的公開發行由協調 `launch-ext-dev@adobe.com`. 請參閱 [發行擴充功能](../../extension-dev/submit/release.md) 以取得更多資訊。 |
| `read-only` | 此資源為只讀資源，無法修改。 |
| `session-timeout` | 用戶會話已過期。 請註銷並重新登錄。 |
| `sftp-authentication-failed` | SFTP連線驗證失敗。 |
| `sftp-connection-timeout` | SFTP連線已逾時。 |
| `sftp-exception` | 使用SFTP連線至伺服器時發生例外狀況。 |
| `sftp-status-exception` | 嘗試與伺服器通訊時遇到SFTP例外狀況。 |
| `socket-error` | 嘗試與伺服器通信時遇到套接字錯誤。 |
| `ssh-disconnect` | SSH會話已斷開。 |
| `timeout-error` | 與伺服器的連接超時。 |
| `unknown-error` | 發生意外錯誤。 您可以稍後再試，或給客戶服務打電話，說明發生時您在做什麼。 |
| `unsupported-custom-code-language` | 提供的自定義代碼語言不受支援。 |
| `upgraded-extension-required` | 安裝擴充功能升級後，您必須將其納入所有程式庫中，直到升級到生產環境為止。 唯一的例外是擴充功能尚未發佈。 |
| `upstream-build-required` | 您必須先成功建立上遊程式庫，才能建立此程式庫。 |

{style="table-layout:auto"}
