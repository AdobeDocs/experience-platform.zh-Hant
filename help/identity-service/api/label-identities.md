---
keywords: Experience Platform；首頁；熱門主題；標籤身分
solution: Experience Platform
title: 將欄位標示為身分
description: 包含個人識別資訊(PII)的欄位可標示為身分欄位。 身分欄位中提供的值由身分識別服務解譯為身分識別。 身分識別的命名空間會指定為欄位標籤的一部分。
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 將欄位標示為身分

包含個人識別資訊(PII)的欄位可標示為身分欄位。 在身分欄位中提供的值，由 [!DNL Identity Service]. 身分識別的命名空間會指定為欄位標籤的一部分。

欄位必須符合下列條件，才能標示為身分：

- 只能將字串類型欄位用於標識
- 只在記錄和時間序列資料中識別身分
- 只有PII欄位應標示為身分。 選擇代表較通用資料的欄位，會導致關係較不精確，且從身分圖存取相關身分時可能會發生錯誤

有關如何使用Schema Registry API將欄位標示為身分的說明，請造訪 [descriptors endpoint worke](../../xdm/api/descriptors.md#create).

## 後續步驟

繼續下一個教學課程，前往 [清單群集標識](./list-cluster-identites.md)
