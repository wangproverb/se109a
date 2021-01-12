```

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Queue;
 
class Pair {
    int x, y;
 
    public Pair(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
 
class Main
{
    // Below arrays details all 8 possible movements
    private static final int[] row = { -1, -1, -1, 0, 0, 1, 1, 1 };
    private static final int[] col = { -1, 0, 1, -1, 1, -1, 0, 1 };
 
    // check if it is possible to go to pixel (x, y) from
    // current pixel. The function returns false if the pixel
    // has different color or it is not a valid pixel
    public static boolean isSafe(char[][] M, int m, int n,
                                 int x, int y, char target)
    {
        return x >= 0 && x < m && y >= 0 && y < n && M[x][y] == target;
    }
 
    // Flood fill using BFS
    public static void floodfill(char[][] M, int x, int y, char replacement)
    {
        int m = M.length;
        int n = M[0].length;
 
        // create a queue and enqueue starting pixel
        Queue<Pair> q = new ArrayDeque<>();
        q.add(new Pair(x, y));
 
        // get target color
        char target = M[x][y];
 
        // loop till queue is empty
        while (!q.isEmpty())
        {
            // pop front node from queue and process it
            Pair node = q.poll();
 
            // (x, y) represents current pixel
            x = node.x;
            y = node.y;
 
            // replace current pixel color with that of replacement
            M[x][y] = replacement;
 
            // process all 8 adjacent pixels of current pixel and
            // enqueue each valid pixel
            for (int k = 0; k < row.length; k++)
            {
                // if adjacent pixel at position (x + row[k], y + col[k]) is
                // a valid pixel and have same color as that of current pixel
                if (isSafe(M, m, n, x + row[k], y + col[k], target))
                {
                    // enqueue adjacent pixel
                    q.add(new Pair(x + row[k], y + col[k]));
                }
            }
        }
    }
 
    public static void main(String[] args)
    {
        // matrix showing portion of the screen having different colors
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
 
        // start node
        int x = 3, y = 9;    // target color = "X"
 
        // replacement color
        char replacement = 'C';
 
        // replace target color with replacement color
        floodfill(M, x, y, replacement);
 
        // print the colors after replacement
        for (var row: M) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```
