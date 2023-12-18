---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；個別設定檔；欄位；綱要；綱要；身分對應；身分對應；綱要設計；對應；聯合綱要；聯合
title: IdentityMap結構描述欄位群組
description: 瞭解XDM個別設定檔類別。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# [!UICONTROL 身分對應] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 身分對應] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供單一對應欄位，其中包含一組由名稱空間輸入的使用者身分。

![的圖表 [!UICONTROL 身分對應] 結構描述欄位群組](../../images/field-groups/identitymap.png)

請參閱以下連結中有關身分對應的章節： [結構描述組合的基本面](../../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊，包括其優點和缺點。

**範例**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

如需欄位群組的詳細資訊，請參閱 [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) 在公用XDM存放庫中。
