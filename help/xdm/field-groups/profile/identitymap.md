---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；個別設定檔；欄位；結構描述；身分對應；身分對應；結構描述設計；對應；聯合結構描述；聯合
title: IdentityMap結構描述欄位群組
description: 瞭解XDM個別設定檔類別。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# [!UICONTROL IdentityMap]架構欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL IdentityMap]是[[!UICONTROL XDM ExperienceEvent]類別](../../classes/experienceevent.md)的標準結構描述欄位群組，以及[[!UICONTROL XDM個人設定檔]類別](../../classes/individual-profile.md)的相容欄位群組。 欄位群組提供單一對應欄位，其中包含一組由名稱空間輸入的使用者身分。

![ [!UICONTROL IdentityMap]結構描述欄位群組](../../images/field-groups/identitymap.png)的圖表

請參閱結構描述組合](../../schema/composition.md#identityMap)的[基本概念中的身分對應一節，以取得有關其使用案例的更多資訊，包括其優點和缺點。

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

如需欄位群組的詳細資訊，請參閱公用XDM存放庫中的[完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json)。
