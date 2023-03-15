---
keywords: Experience Platform；首頁；熱門主題；分段；分段符合；區段符合
solution: Experience Platform
title: 區段比對常見問題集
description: 區段比對是Adobe Experience Platform中的區段共用服務，可讓兩位或多位Platform使用者以安全、受控且符合隱私權的方式來交換區段資料。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] 常見問題集

本指南針對經常詢問關於Adobe Experience Platform區段比對的隱私權和法律問題提供解答。

## 在估計重疊期間共用哪些資料，以及Adobe如何確保安全地取得這些量度？

![overlap-report.png](./images/overlap-report.png)

不會跨沙箱移動任何客戶或區段資料，以取得這些重疊的估計量度。 任何指定沙箱中由客戶選取、預先雜湊的適用身分資料會新增至可能性資料結構，其中ID本身會以雜湊格式表示。

這是單向程式，表示原始預先雜湊識別碼不會公開，且無法反向設計。

這些資料結構具有獨特的屬性，使得工程能夠執行它們之間的聯合和交集操作，即使編碼的資訊被嚴重壓縮或雜湊。 這些操作允許 [!DNL Segment Match] 從兩個不同的沙箱中取得由ID組成的兩個資料結構的估計交集，而不需要比較實際值。 自 [!DNL Segment Match] ID只會使用資料結構，且不會為了估計目的而離開其各自的IMS組織設定檔儲存區。 這可讓Adobe滿足客戶的隱私和安全需求，同時提供指導資料協作協定的高度準確的估算工具。

## 指定哪些身分會接收共用區段ID的程式為何？

[!DNL Segment Match] 可讓客戶選擇設定要在服務中使用的命名空間。 如果客戶決定將摘要發佈至合作夥伴沙箱，此選項會套用至先前問題中說明的估計程式和資料傳輸程式。

在中性計算環境中執行兩個不同組織的加密身份之間的資料傳輸過程。 資料傳輸作業由Adobe擁有，且參與合作夥伴的組織無權訪問此環境，也無法訪問任何可能是資料傳輸作業結果的日誌。

只有區段成員資格會擷取至接收者IMS組織的重疊設定檔片段中，且不會將其他身分從傳送者IMS組織轉移至接收者IMS組織。 資料傳輸工作不會讀取純文字的個人識別資訊(PII)，因為 [!DNL Segment Match] 只允許在資料為PII時，於SHA256加密的命名空間（電子郵件/電話）上重疊。 結果永遠不會儲存在計算環境中。
