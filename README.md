# 洪水演算法(Flood Fill)
## 洪水演算法介紹
```
用於確定連接到多維數組中給定節點的區域。它用於繪畫程序的“存儲桶”填充工具中，以不同的顏色填充連接的相似顏色的區域，並用於諸如Go和Minesweeper之類的遊戲中，以確定要清除的部分。
填充算法採用三個參數：起始節點，目標顏色和替換顏色。該算法查找通過目標顏色的路徑連接到起始節點的陣列中的所有節點，並將其更改為替換顏色。可以使用多種方法來構造泛洪填充算法，但是大多數方法都顯式或隱式地使用隊列或堆棧數據結構。
根據是否考慮節點在連接的角接觸，我們有兩種變化：分別為八向和四向。
```
#### 遞歸式實現
```
填充（節點，目標顏色，替換顏色）：
 1.如果目標顏色等於替換顏色，則返回
 2.否則，如果節點的顏色不等於target-color，則返回
 3.否則將節點的顏色設置為replace-color
 4.執行Flood-fill（填充，在node的南部，target-color，replace-color的南部）
    執行泛洪填充（在node北部，target-color，replace-color的北部）
    執行Flood-fill（向node的西邊一步，target-color，replace-color）
    執行泛洪填充（向node的東側一步，target-color，replace-color）
 5.返回
```
#### 程式
```
檢查是否可以從轉到像素（x，y）。確認當前像素。如果像素，該函數返回false，顏色不同或不是有效像素
```
```
public static boolean isSafe(char[][] M, int m, int n,
                                 int x, int y, char target)
    {
        return x >= 0 && x < m && y >= 0 && y < n && M[x][y] == target;
    }
```
```
洪水演算法使用到BFS
```
```
 public static void floodfill(char[][] M, int x, int y, char replacement)
    {
        int m = M.length;
        int n = M[0].length;

        Queue<Pair> q = new ArrayDeque<>();
        q.add(new Pair(x, y));
  
        char target = M[x][y];
 
        while (!q.isEmpty())
        {
            Pair node = q.poll();
            x = node.x;
            y = node.y;
            M[x][y] = replacement;
 
            for (int k = 0; k < row.length; k++)
            {
                if (isSafe(M, m, n, x + row[k], y + col[k], target))
                {
                    q.add(new Pair(x + row[k], y + col[k]));
                }
            }
        }
``` 
```
顯示不同顏色的屏幕部分的矩陣
```
```  
 public static void main(String[] args)
    {
        char[][] M = {
                "YYYGGGGGGG".toCharArray(),
                "YYYYYYGXXX".toCharArray(),
                "GGGGGGGXXX".toCharArray(),
                "WWWWWGGGGX".toCharArray(),
                "WRRRRRGXXX".toCharArray(),
                "WWWRRGGXXX".toCharArray(),
                "WBWRRRRRRX".toCharArray(),
                "WBBBBRRXXX".toCharArray(),
                "WBBXBBBBXX".toCharArray(),
                "WBBXXXXXXX".toCharArray()
        };
 
        int x = 3, y = 9;    // target color = "X"
 
        char replacement = 'C';
        floodfill(M, x, y, replacement);
        for (var row: M) {
            System.out.println(Arrays.toString(row));
        }
    }
```  
#### 輸出結果
```  
[Y, Y, Y, G, G, G, G, G, G, G]
[Y, Y, Y, Y, Y, Y, G, C, C, C]
[G, G, G, G, G, G, G, C, C, C]
[W, W, W, W, W, G, G, G, G, C]
[W, R, R, R, R, R, G, C, C, C]
[W, W, W, R, R, G, G, C, C, C]
[W, B, W, R, R, R, R, R, R, C]
[W, B, B, B, B, R, R, C, C, C]
[W, B, B, C, B, B, B, B, C, C]
[W, B, B, C, C, C, C, C, C, C]
```  
#### 時間複雜度分析
``` 
此算法中m和n陣列作為輸入，此時間複雜度為O(mn)
``` 

