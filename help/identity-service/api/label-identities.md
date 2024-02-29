---
keywords: Experience Platform；首頁；熱門主題；標籤身分
solution: Experience Platform
title: 將欄位標示為身分
description: 包含個人識別資訊(PII)的欄位可標示為身分欄位。 身分欄位中提供的值會由Identity Service解譯為身分。 身分的名稱空間是在標示欄位時指定的。
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 將欄位標示為身分

包含個人識別資訊(PII)的欄位可標示為身分欄位。 身分欄位中提供的值會由解譯為身分 [!DNL Identity Service]. 身分的名稱空間是在標示欄位時指定的。

欄位必須符合下列條件，才能標示為身分：

- 只有字串型別欄位可用於身分
- 身分只能在記錄和時間序列資料中識別
- 只有PII欄位應該標示為身分。 選擇代表較通用資料的欄位可能會導致關係較不精確，並且可能導致從身分圖表存取相關身分時發生錯誤

如需有關如何使用Schema Registry API將欄位標示為身分的說明，請造訪 [描述項端點指南](../../xdm/api/descriptors.md#create).

## 後續步驟

繼續進行下一個教學課程： [列出叢集身分](./list-cluster-identites.md)
