# Prototype C: UDP Client and Server (UDP伺服器與客戶端雛形)
============================================================
Spec: 請寫出一個 TCP Client 與一個 TCP Server

1. Client行為
	1. 執行後，等待使用者輸入兩個IP，分別代表本機及Server
	2. 輸入完成後，假設此client維持一個移動中物體的座標(x, y)
		* 座標由(0, 0)到(100, 100)
		* 每隔2秒client便將x, y座標各加1，即由(x, y)更新為(x+1, y+1)
		* 當(x, y) == (100, 100)，將(x, y)更新為(0, 0)
		* 每隔0.2秒向UDP Server傳送UDP Message `X Y`以更新目前座標
2. Server行為
	1. 無窮迴圈，等待client送座標
	2. 當收到`X Y`座標訊息時，輸出`(X Y)`於螢幕上