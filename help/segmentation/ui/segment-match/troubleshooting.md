---
keywords: Experience Platform；首頁；熱門主題；分段；分段；段匹配；段匹配
solution: Experience Platform
title: 段匹配常見問題
description: 段匹配是Adobe Experience Platform的段共用服務，允許兩個或兩個以上平台用戶以安全、受管理和隱私友好的方式交換段資料。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# [!DNL Segment Match] 常見問題

本指南提供有關Adobe Experience Platform段匹配的隱私和法律問題的答案。

## 在估計重疊期間共用哪些資料，Adobe如何確保安全獲取這些度量？

![重疊報表.png](./images/overlap-report.png)

不會跨沙箱移動客戶或段資料以獲得這些重疊估計度量。 將任何給定沙箱中客戶選擇的預先散列的適用身份添加到概率資料結構中，其中ID本身以散列格式表示。

這是一個單向過程，這意味著原始預散列標識符不會被公開，並且無法進行反向工程。

這些資料結構具有獨特的屬性，使工程能夠執行它們之間的聯合和交集操作，即使編碼的資訊被嚴重壓縮或散列。 這些操作允許 [!DNL Segment Match] 從兩個不同的沙箱中獲取由ID組成的兩個資料結構的估計交點，而無需比較實際值。 自 [!DNL Segment Match] 僅使用資料結構，ID永遠不會離開各自組織的配置檔案儲存以便進行估計。 這允許Adobe滿足客戶的隱私和安全要求，同時提供高度準確的評估工具來指導資料協作協定。

## 指定哪些標識接收共用段ID後，會採取什麼過程？

[!DNL Segment Match] 為客戶提供了一個選項，以配置在服務中使用的命名空間。 如果客戶決定將訂閱源發佈到合作夥伴沙箱，則此選擇將應用於上一個問題中描述的估計過程和資料傳輸過程。

在兩個不同組織的加密身份之間的資料傳輸過程在中性計算環境中執行。 資料傳輸作業由Adobe所有，並且參與夥伴關係的組織無權訪問此環境，也無權訪問任何可能由資料傳輸作業產生的日誌。

只將段成員身份接收到接收組織重疊的Profile片段，並且不將附加身份從發送組織轉移到接收組織。 資料傳輸作業不會讀取純文字檔案個人識別資訊(PII)，因為 [!DNL Segment Match] 只允許在資料為PII時在SHA256加密命名空間（電子郵件/電話）上重疊。 結果從不儲存在計算環境中。
