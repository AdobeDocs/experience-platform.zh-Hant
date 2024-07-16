---
title: 加密值
description: 瞭解在使用Reactor API時如何加密敏感值。
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---

# 加密值

使用Adobe Experience Platform中的標籤時，某些工作流程需要提供敏感值（例如，透過主機將程式庫傳送至環境時提供私密金鑰）。 這些認證的敏感性質是必要的
安全的傳輸和儲存。

本檔案說明如何使用[GnuPG加密](https://www.gnupg.org/gph/en/manual/x110.html) （也稱為GPG）來加密敏感值，以便只有標籤系統才能讀取它們。

## 取得公開GPG金鑰和總和檢查碼

在[下載](https://gnupg.org/download/)並安裝最新版GPG之後，您必須取得標籤生產環境的公用GPG金鑰：

* [GPG金鑰](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [總和檢查碼](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## 將金鑰匯入您的鑰匙圈

將金鑰儲存至電腦後，下一步就是將其新增至您的GPG金鑰鏈。

**語法**

```shell
gpg --import {KEY_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{KEY_NAME}` | 公開金鑰檔案的名稱。 |

{style="table-layout:auto"}

**範例**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## 加密值

將金鑰新增至鑰匙圈後，您可以使用`--encrypt`旗標開始加密值。 下列指令碼示範這個命令的運作方式：

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

此指令可依下列方式劃分：

* 輸入已提供給`gpg`命令。
* `--armor`會建立ASCII-carphaned輸出，而非二進位。 這可簡化透過JSON傳輸值的流程。
* `--encrypt`指示GPG加密資料。
* `-r`設定資料的收件者。 只有收件者（與公開金鑰對應的私密金鑰持有者）可以解密資料。 檢查`gpg --list-keys`的輸出即可找到所需金鑰的收件者名稱。

上述命令使用`Tags Data Encryption <launch@adobe.com>`的公開金鑰以ASCII裝甲格式加密值`Example value`。

指令的輸出將類似於以下內容：

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

此輸出只能由擁有私密金鑰的系統解密，
對應至`Tags Data Encryption <launch@adobe.com>`公開金鑰。

此輸出是在將資料傳送至Reactor API時，應在中提供的值。 系統會儲存此加密輸出，並視需要暫時解密。 例如，系統會解密足夠長的主機證明資料，以起始與伺服器的連線，然後立即移除解密值的所有追蹤。

>[!NOTE]
>
>裝甲加密值格式很重要。 確保請求中提供的值已正確逸出行傳回。
