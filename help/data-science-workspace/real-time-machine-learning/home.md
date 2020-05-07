---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 即時機器學習概觀
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# 即時機器學習概觀

>[!IMPORTANT]
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

Adobe Experience Platform的即時機器學習架構可讓您使用機器學習，在適當的通道中，在適當的時間，以次秒的時間範圍，在適當的時間向適當的使用者提供適當的體驗。

## 優點

即時機器學習功能可大幅提升數位體驗內容對使用者的相關性。 透過在Experience Edge上運用即時參考和持續學習，您就能做到這一點。

在Hub和Edge上結合流暢的運算，可大幅降低傳統上推動高度個人化體驗（既相關又回應快速）的延遲。 因此，即時機器學習為同步決策提供極低的延遲。 例如，轉換個人化網頁內容，或呈現優惠或折扣，以減少客戶流失並提高網路商店的轉化率。

## 即時機器學習架構

下圖提供即時機器學習架構的概觀。

![簡化總覽](../images/rtml/simple-overview.png)

## 即時機器學習工作流程(Alpha)

以下工作流程概述建立和使用即時機器學習模型的典型步驟和結果。

### 資料擷取與準備

透過Adobe Experience Platform上的Experience Data Model(XDM)，資料會被擷取並轉換。 此資料用於模型訓練。 若要進一步瞭解XDM，請造訪 [XDM概觀](../../xdm/home.md)。

### 製作

從頭開始製作即時機器學習模型，或以預先訓練好的序號化ONNX模型在Adobe Experience Platform Jupyter Notebooks中引入，以建立即時機器學習模型。

### 部署

將您的模型部署至Experience Edge，以使用預測API端點在服務收藏館中建立即時機器學習服務。

### 推理

使用Prediction REST API端點，即時產生機器學習見解。

### 傳送

然後，行銷人員可以定義區段和規則，將即時機器學習分數對應至使用Adobe Target的體驗。 這可讓品牌網站的訪客即時顯示相同或下一頁的超個人化體驗（100毫秒以下）。

## 開發計畫

即時機器學習目前處於Alpha階段。 下表列出預期在未來測試版迭代中發行的某些功能和更新。

<table>
    <th></th>
    <th>Alpha（5月）</th>
    <th>測試版</th>
    <tr>
        <td>
            <strong>功能</strong>
        </td>
        <td>
            <li>Data Science Workspace透過筆記型電腦啟動程式整合，提供您自己的模型與作者。</li>
            <li>製作營運商的入門者集。</li>
            <li>部署至中心</li>
            <li>Scikit學習型號。</li>
        </td>
        <td>
            <li>Data Science Workspace服務收藏館UI整合。</li>
            <li>利用推理結果自動豐富即時客戶個人檔案。</li>
            <li>深入學習模型。</li>
            <li>擴充的編寫運算元集，包括自訂運算元。</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>可用性</strong>
        </td>
        <td>
            北美
        </td>
        <td>
            <li>北美</li>
            <li>歐洲和中東(EMEA)</li>
            <li>亞太地區</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>製作</strong>
        </td>
        <td>
            <li>Python支援</li>
            <li>即時機器學習SDK</li>
            <li>Python編寫節點： Pacrotics、ScikitLearn、ONXNode、Split、ModelUpload、OneHotEncoder。</li>
        </td>
        <td>
            <li>索力流支援。</li>
            <li>其他Python製作節點： 即時客戶資料閱讀器、即時客戶資料撰寫器、Numpy Arrays、XDM2Frame、Frame2XDM。 </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>計分執行時間</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## 後續步驟

您可依照快速入 [門指南](./getting-started.md) 。 本指南會逐步引導您設定建立即時機器學習模型的所有必要先決條件。

