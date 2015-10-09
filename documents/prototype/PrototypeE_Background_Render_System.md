# Prototype E: Background Render System (背景成像系統)
============================================================
Spec: 請寫一個程式
	* 按照目前座標(X, Y)改變背景的程式
	* 背景大小為 5000 pixel x 2000 pixel
	* 此(X, Y)可受鍵盤上下左右鍵控制

細部規格如下
1. 直接取5000 pixel x 2000 pixel的圖片來使用是不可行，耗費太多記憶體
2. 可以使用 100 pixel x 100 pixel 的基本場景圖檔(basic block)重複貼圖
3. 請製作五種以上的basic block。以100x100為例，則5000x2000的地圖可以一個50x20的2D-array表示
	* 參考程式碼: class BasicBlock
	```
	enum blockType {
		GRASS, FOREST, WATER, ROCK, GRASS_WITH_WATER
	}
	class BasicBlock {
		blockType type;
		... //other attribute
	}
	```
	* 參考程式碼: BasicBlock[][] scene
	```
	BasicBlock[][] scene = new BasicBlock[20][50];
	for(y=0; y<20; y++) {
		for(x=0; x<50; x++) {
			scene[y][x] = new BasicBlock();
		}
	}
4. 場景可先用自訂組合，或隨機產生，將5種basic block填入場景中
5. 初始座標為(2500, 1000)
6. 可見視窗(view window)大小為500x300
7. 請設計出一套彈性的計算，可根據現在座標與視窗大小，計算出相對於scene的位置，然後以現在座標為中心，把周圍要顯示的basic block畫在view window上
8. 當使用者按右鍵時，表示螢幕中心的主角向右移動，定每次移動距離為25，則新座標為(X+25, Y)。當作標變動時，呼叫update()重新繪製背景。同理，請完成上下左右移動。
9. 請注意使用`drawImage()`時，座標可為負，也就是你可以將basic block畫到view window外，然後再讓view window幫你做剪裁