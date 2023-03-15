---
title: 加密值
description: 了解如何在使用Reactor API時加密敏感值。
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 加密值

在Adobe Experience Platform中使用標籤時，某些工作流程需要提供敏感值（例如，透過主機將程式庫傳送至環境時提供私密金鑰）。 這些憑據的敏感性要求安全傳輸和儲存。

本檔案說明如何使用 [GnuPG加密](https://www.gnupg.org/gph/en/manual/x110.html) （也稱為GPG），因此只有標籤系統可以讀取。

## 獲取公共GPG密鑰和校驗和

之後 [下載](https://gnupg.org/download/) 安裝最新版GPG時，您必須取得標籤生產環境的公開GPG金鑰：

* [GPG金鑰](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [校驗和](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## 將金鑰匯入鑰匙圈

將金鑰儲存至電腦後，下一步就是將金鑰新增至GPG金鑰鏈。

**語法**

```shell
gpg --import {KEY_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{KEY_NAME}` | 公鑰檔案的名稱。 |

{style="table-layout:auto"}

**範例**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## 加密值

將金鑰新增至金鑰鏈後，您可以使用 `--encrypt` 標籤。 以下指令碼演示此命令的工作方式：

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

此命令可依下列方式劃分：

* 輸入被提供給 `gpg` 命令。
* `--armor` 會建立ASCII裝甲輸出，而非二進位。 這可簡化透過JSON傳輸值。
* `--encrypt` 指示GPG加密資料。
* `-r` 設定資料的收件者。 只有接收者（與公鑰對應的私密金鑰的持有者）才能解密資料。 通過檢查所需密鑰的輸出，可以找到所需密鑰的接收者名稱 `gpg --list-keys`.

以上命令使用的公鑰 `Tags Data Encryption <launch@adobe.com>` 要加密值， `Example value`，以ASCII裝甲格式。

命令的輸出如下所示：

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

此輸出只能由具有與 `Tags Data Encryption <launch@adobe.com>` 公開金鑰。

此輸出是將資料傳送至Reactor API時，應在中提供的值。 系統儲存這個加密的輸出，並根據需要臨時解密。 例如，系統解密足夠長的主機憑據以啟動到伺服器的連接，然後立即刪除解密值的所有跡線。

>[!NOTE]
>
>裝甲、加密值的格式非常重要。 確保在請求中提供的值中正確逸出行返回。
