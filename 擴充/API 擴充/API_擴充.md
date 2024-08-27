# API 擴充

開發者可透過API 擴充模組能力，目前支援以下模組擴充：

- ```moderation```敏感內容審計

- ```external_data_tool```外部資料工具

在擴充模組能力之前，您需要準備一個API 和用於鑑權的API Key（也可由Dify 自動生成，可選）。

除了需要開發對應的模組能力，還需要遵守以下規範，以便Dify 可以正確地呼叫API。

![基於API擴充](/擴充/images/基於API擴充.png)

## API 規格
Dify 將會以以下規格呼叫您的介面：
```
POST {Your-API-Endpoint}
```

**標頭**

|**標頭**|**價值**|**描述**|
|:------|:-------|:-------|
|```Content-Type```|應用程式/json|請求內容為​​JSON 格式|
|```Authorization```|承載 {api_key}|API Key 以Token 令牌的方式傳輸，您需要解析該```api_key```並確認是否和提供的API Key 一致，以確保介面安全。|

**請求正文**

```
{
    "point":  string, //  扩展点，不同模块可能包含多个扩展点
    "params": {
        ...  // 各模块扩展点传入参数
    }
}
```

**API 傳回**

```
{
    ...  // API 返回的内容，不同扩展点返回见不同模块的规范设计
}
```

## 校驗
當Dify 設定API-based Extension 時，Dify 將會發送一個請求至API Endpoint，以檢驗API 的可用性。

當API Endpoint 接收到point=ping時，介面應傳回result=pong，如下：

**標頭**

```
Content-Type: application/json
Authorization: Bearer {api_key}
```

**請求正文**

```
{
    "point": "ping"
}
```

**API 期望傳回**

```
{
    "result": "pong"
}
```

## 範例

此處以外部資料工具為例，場景為根據地區取得外部天氣資訊作為上下文。

**API 範例**

```
POST https://fake-domain.com/api/dify/receive
```

**標頭**

```
Content-Type: application/json
Authorization: Bearer 123456
```

**請求正文**

```
{
    "point": "app.external_data_tool.query",
    "params": {
        "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
        "tool_variable": "weather_retrieve",
        "inputs": {
            "location": "London"
        },
        "query": "How's the weather today?"
    }
}
```

**API 傳回**

```
{
    "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
}
```

**程式碼範例**

程式碼基於Python FastAPI 框架。

1. 安裝依賴

    ```
    pip install fastapi[all] uvicorn
    ```

2. 依照介面規範編寫程式碼

    ```
    from fastapi import FastAPI, Body, HTTPException, Header
    from pydantic import BaseModel

    app = FastAPI()


    class InputData(BaseModel):
        point: str
        params: dict = {}


    @app.post("/api/dify/receive")
    async def dify_receive(data: InputData = Body(...), authorization: str = Header(None)):
        """
        Receive API query data from Dify.
        """
        expected_api_key = "123456"  # TODO Your API key of this API
        auth_scheme, _, api_key = authorization.partition(' ')

        if auth_scheme.lower() != "bearer" or api_key != expected_api_key:
            raise HTTPException(status_code=401, detail="Unauthorized")

        point = data.point

        # for debug
        print(f"point: {point}")

        if point == "ping":
            return {
                "result": "pong"
            }
        if point == "app.external_data_tool.query":
            return handle_app_external_data_tool_query(params=data.params)
        # elif point == "{point name}":
            # TODO other point implementation here

        raise HTTPException(status_code=400, detail="Not implemented")


    def handle_app_external_data_tool_query(params: dict):
        app_id = params.get("app_id")
        tool_variable = params.get("tool_variable")
        inputs = params.get("inputs")
        query = params.get("query")

        # for debug
        print(f"app_id: {app_id}")
        print(f"tool_variable: {tool_variable}")
        print(f"inputs: {inputs}")
        print(f"query: {query}")

        # TODO your external data tool query implementation here, 
        #  return must be a dict with key "result", and the value is the query result
        if inputs.get("location") == "London":
            return {
                "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind "
                        "Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
            }
        else:
            return {"result": "Unknown city"}
    ```

3. 啟動API 服務，預設連接埠為8000，API 完整位址為：http://127.0.0.1:8000/api/，配置的API Key 為123456。

    ```
    uvicorn main:app --reload --host 0.0.0.0
    ```

4. 在Dify 設定該API。

    ![基於API擴充](/擴充/images/基於API擴充.png)

5. 在App 中選擇該API 擴充功能。
