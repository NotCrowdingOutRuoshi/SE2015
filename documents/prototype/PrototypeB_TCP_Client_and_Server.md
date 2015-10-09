# Prototype B: TCP Client and Server (TCP伺服器與客戶端雛形)
============================================================
Spec: 請寫出一個 TCP Client 與多執行緒的 TCP Server

1. 實作一個concurrent server，必須能同時接收2個connections
2. 當接到一個connection時，在螢幕上印出該connection的來源，並保持connection連通
3. 當2個connection連接完成時，Server行為如下。請假設有3個寶物 A, B, C由Server所控管
	1. 當Client想撿取該寶物時，透過TCP傳送一個message `GET A`給Server。
		* Server接收此訊息後，若決定寶物A由該client獲得，則回傳訊息 `YES A`給該clinet
		* 若A寶物不歸該clinet所有，則回傳 `NO A`
	2. 若client想釋放A寶物，則送出訊息 `RELEASE A` 給Server，Server收到後將寶物A設為無人所有
	3. Server每3秒印出寶物所有權訊息，例如A為1所有、B無主、C為2所有，則訊息如下
		> A YES 1
		> B NO  0
		> C YES 2
4. Client行為
	1. 請寫一個無窮迴圈，使client每隔一秒鐘便按順序A, B, C去撿取寶物。若該寶物已有主則跳過。
	2. 在寶物獲取後，設定一計時器，獲取寶物滿五秒後將該寶物釋放。
	3. Client每3秒印出寶物所有權訊息，例如A, C為此client所有，且A還能擁有4秒鐘、C還能擁有1秒鐘，則訊息如下
		> A YES 4
		> B NO  0
		> C YES 1