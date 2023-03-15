---
keywords: Experience Platform；首頁；熱門主題；標籤身分
title: 在UI中將欄位標示為身分
description: 包含個人識別資訊(PII)的欄位可標示為身分欄位。 身分欄位中提供的值由身分識別服務解譯為身分識別。 身分識別的命名空間會指定為欄位標籤的一部分。
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 在UI中將欄位標示為身分

包含個人識別資訊(PII)的欄位可標示為身分欄位。 在身分欄位中提供的值，由 [!DNL Identity Service]. 身分識別的命名空間會指定為欄位標籤的一部分。

欄位必須符合下列條件，才能標示為身分：

* 只能將字串類型欄位用於標識
* 只在記錄和時間序列資料中識別身分
* 只有PII欄位應標示為身分。 選擇代表較通用資料的欄位，會導致關係較不精確，且從身分圖存取相關身分時可能會發生錯誤

如需如何在UI中標示身分欄位的指示，請參閱 [定義UI中的身分欄位](../../xdm/ui/fields/identity.md).

## 後續步驟

如需 [!DNL Identity Service]，請參閱 [[!DNL Identity Service] 概述](../home.md).
