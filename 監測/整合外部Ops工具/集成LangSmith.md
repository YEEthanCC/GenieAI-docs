# 什麼是LangSmith
## LangSmith 是一個用於建立生產級LLM 應用程式的平台，它用於開發、協作、測試、部署和監控LLM 應用程式。

LangSmith 官網介紹：[https://www.langchain.com/langsmith](https://www.langchain.com/langsmith)

## 如何配置LangSmith
本章節將指引你註冊LangSmith 並將其整合至Dify 平台內。

1. **註冊/登入**[LangSmith](https://www.langchain.com/langsmith)
2. **建立項目**

    在LangSmith 內建立項目，登入後在主頁點擊New Project建立一個自己的項目，項目將用於與Dify 內的應用關聯進行資料監測。

    ![在LangSmith內建立項目](/監測/整合外部Ops工具/images/在LangSmith內建立項目.png)

    創建完成之後在Projects 內可以查看該項目。

    ![在LangSmith內查看已建立項目](/監測/整合外部Ops工具/images/在LangSmith內查看已建立項目.png)

3. **建立專案憑證**

    建立專案憑證，在左側邊欄內找到專案設定Settings。

    ![項目設定](/監測/整合外部Ops工具/images/項目設定.png)

    點選**Create API Key**，建立一個專案憑證。
    
    ![建立一個項目API_Key](/監測/整合外部Ops工具/images/建立一個項目API_Key.png)

    選擇**Personal Access Token**，用於後續的API 身分校驗。
    
    ![建立一個API_Key](/監測/整合外部Ops工具/images/建立一個API_Key.png)

    將建立的API key 複製保存。

4. **將LangSmith 整合至Dify 平台**

    在Dify 應用程式內配置LangSmith。開啟需要監測的應用，在左側邊選單內開啟**監測**，點選頁面內的**設定**。

    ![配置LangSmith](/監測/整合外部Ops工具/images/配置LangSmith.png)

    點擊配置後，將在LangSmith 內建立的API Key和項目名稱貼上到配置內並儲存。

    