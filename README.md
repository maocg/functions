<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>调起轻应用</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
            margin-bottom: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>调起轻应用</h2>
        <input type="text" id="app-url" value="hap://game/com.syhd.zjcjy.nearme.gamecenter">
        <button onclick="checkAndLaunchApp()">调起轻应用</button>
    </div>

    <script>
        // 支持的轻应用 URL 前缀
        const SUPPORTED_PREFIX = "hap://";

        // 检测并调起轻应用
        function checkAndLaunchApp() {
            const input = document.getElementById('app-url');
            const url = input.value.trim();

            // 检测 URL 是否支持
            if (!url.startsWith(SUPPORTED_PREFIX)) {
                alert("不支持该轻应用 URL，请检查输入！");
                return;
            }

            // 调起轻应用
            launchApp(url);
        }

        // 调起轻应用
        function launchApp(url) {
            // 记录当前时间
            const startTime = Date.now();

            // 尝试调起轻应用
            window.location.href = url;

            // 设置定时器检测页面是否被隐藏
            setTimeout(() => {
                const endTime = Date.now();
                // 如果页面未被隐藏且时间差小于 2000ms，说明调起失败
                if (!document.hidden && endTime - startTime < 2000) {
                    alert("轻应用不存在或调起失败！");
                }
            }, 1000); // 1秒后检测
        }

        // 监听页面隐藏事件
        document.addEventListener("visibilitychange", () => {
            if (document.hidden) {
                console.log("页面被隐藏，轻应用调起成功！");
            }
        });
    </script>
</body>
</html>
