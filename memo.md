- WebRTC 功能我想预览一下，怎么操作？
- websocket 以后要换成接口的形式，由portal定时请求
- 日常portal运行过程中需要需要上报的，通过HTTP接口
工作流下发 通过定时去请求HTTP接口
- 修改websocket url 输入框。默认地址为服务器地址
- 修改websocket url 只输入IP，协议和端口以及path都是固定的

{"method":"app","params":{"package":"com.kuaishou.nebula"}}
{"method":"events/device/ui","params":{"resourceId":"android:id/button2","actionId":16}}
{"method":"tap","params":{"x":944,"y":499}}
{"method":"app/stop","params":{"package":"com.kuaishou.nebula"}}

```
{"method":"tap","params":{"x":300,"y":800}}
{"method":"swipe","params":{"startX":300,"startY":1200,"endX":300,"endY":400,"duration":300}}
{"method":"global","params":{"action":1}}
{"method":"app","params":{"package":"", "activity":[optional]string, "stopBeforeLaunch":[optional]bool=false}}
{"method":"app/stop","params":{"package":""}}
{"method":"input","params":{"base64_text":"","clear":[optional]bool=true}}
{"method":"clear"}
{"method":"screenshot","params":{"hideOverlay":true}}
{"method":"packages","params":{}}
{"method":"state","params":{"filter":true}}
{"method":"version","params":{}}
{"method":"time","params":{}}
{"method":"events/device/ui","params":{}}
```

```
2. 所有支持的 method 及参数（按 ActionDispatcher.dispatch 代码顺序）
1. tap
参数：x (Int, 默认0), y (Int, 默认0)
2. swipe
参数：startX, startY, endX, endY (Int, 默认0), duration (Int, 默认300)
3. global
参数：action (Int, 默认0)
4. app
参数：
package (String, 必填，或用 packageName)
activity (String, 可选)
stopBeforeLaunch (Boolean, 可选，默认false)
5. app/stop
参数：package (String, 必填，或用 packageName)
6. keyboard/input 或 input
参数：base64_text (String, 默认""), clear (Boolean, 默认true)
7. keyboard/clear 或 clear
参数：无
8. keyboard/key 或 key
参数：key_code (Int, 默认0)
9. overlay_offset 或 overlay/offset
参数：offset (Int, 默认0)
10. overlay/set-visible
参数：visible (Boolean, 默认false)
11. overlay/visible 或 overlay/is-visible
参数：无
12. socket_port
参数：port (Int, 默认0)
13. screenshot
参数：hideOverlay (Boolean, 默认true)
14. packages
参数：无
15. state
参数：filter (Boolean, 默认false)
16. version
参数：无
17. time
参数：无
18. files/list
参数：path (String, 默认"")
19. files/download
参数：path (String, 默认"")
20. files/upload
参数：
path (String, 必填)
data (String, base64, 必填)
21. files/delete
参数：path (String, 默认"")
22. files/fetch
参数：url (String, 默认"")
参数：path (String, 默认"")
23. files/push
参数：url (String, 默认"")
参数：path (String, 默认"")
24. triggers/catalog
参数：无
25. triggers/status
参数：无
26. triggers/rules/list
参数：无
27. triggers/rules/get
参数：ruleId (String, 必填)
28. triggers/rules/save
参数：rule (JSONObject, 必填)
29. triggers/rules/delete
参数：ruleId (String, 必填)
30. triggers/rules/setEnabled
参数：ruleId (String, 必填)
参数：enabled (Boolean, 必填)
31. triggers/rules/test
参数：ruleId (String, 必填)
32. triggers/runs/list
参数：limit (Int, 默认50)
33. triggers/runs/delete
参数：runId (String, 必填)
34. triggers/runs/clear
参数：无
35. screen/keepAwake/set
参数：enabled (Boolean, 必填)
36. screen/keepAwake/status
参数：无
37. install
参数：
urls (Array of String, 必填)
hideOverlay (Boolean, 默认false)
38. stream/start
参数：任意（透传给 apiHandler.startStream(params)）
39. stream/stop
参数：sessionId (String, 必填)
40. webrtc/answer
参数：sdp (String, 必填)
参数：sessionId (String, 必填)
41. webrtc/offer
参数：sdp (String, 必填)
参数：sessionId (String, 必填)
42. webrtc/ice
参数：candidate (String, 必填)
参数：sdpMid (String, 可选)
参数：sdpMLineIndex (Int, 可选)
参数：sessionId (String, 必填)
43. webrtc/rtcConfiguration
参数：任意（透传）
44. webrtc/requestFrame
参数：sessionId (String, 必填)
45. webrtc/keepAlive
参数：sessionId (String, 必填)
46. webrtc/connect
参数：sessionId (String, 必填)
参数：其他参数透传
 
3. 其它说明
所有 method 都支持 /action/xxx、action.xxx、xxx 三种写法。
参数类型和必填项严格见上，缺少必填参数会返回错误。
还有部分 method 只允许特定 origin（如 stream/*、webrtc/* 只允许反向 WebSocket）。
```

