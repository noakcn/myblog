---
title: 找出字符串中出现次数最多的字符
date: 2018-5-30 20:58:22
tags:
- java
categories:
- 面试
---

今天面试遇到一道题目，题目如下：
提供如下字符串`"ABBCCDE"`找出字符串中出现次数最多的字符，如果次数相同，显示首次出现的字符。

我开始构思的如下：
**本题很多人用HashMap<Character,Integer>实现计数，获取最高，但是本题要求如果次数相同，应该获取首次出现的支付，HashMap的无序存储显然不能满足要求**
```

public static char getFirstMax(char[] arr) {
        int[] count = new int[256];
        int max = 0;
        for (int i = 0; i < arr.length; i++) {
            count[arr[i]]++;
            if (max < count[arr[i]]) {
                max = i;
            }
        }
        return arr[max];

    }

```

后来经过面试官的提醒，如果字符串改为`"CABBCDE"`我这个方法就不准确了。思考了下，当时有点紧张没能在原来的基础上实现，就改用``LinkedHashMap<Character,Integer>来实现``，代码如下
```
 public static Character getFirstMaxV2(String str) {
        Character arr[] = new Character[str.length()];
        for(int i = 0;i<str.length();i++){
            arr[i] = str.charAt(i);
        }

        LinkedHashMap<Character, Integer> map = new LinkedHashMap<>();
        for (int i = 0; i < arr.length; i++) {
            if (map.get(arr[i]) == null) {
                map.put(arr[i], 1);
            } else {
                map.put(arr[i], map.get(arr[i]) + 1);
            }
        }
        int max = 0;
        Character maxChar = arr[0];
        for (Character key : map.keySet()) {
           if(map.get(key) > max){
               max = map.get(key);
               maxChar = key;
           }
        }

        return maxChar;

    }

```

回家后，我又想了下第一种实现的优化，代码如下
```

public static char getFirstMaxV3(char[] arr) {
        int maxCount = 0;
        char maxChar = arr[0];
        for (int i = 0; i < arr.length; i++) {
            int thisCount = 0;
            for (int j = 0; j < arr.length; j++) {
                if (arr[j] == arr[i]) {
                    thisCount++;
                }
            }
            if (maxCount < thisCount) {
                maxCount = thisCount;
                maxChar = arr[i];
            }

        }
        return maxChar;
    }
```

运行测试跑一下:
```

 public static void main(String[] args) {
        String str = "ABBCCDE";
        System.out.println(getFirstMax(str.toCharArray()));
        System.out.println(getFirstMaxV2(str));
        System.out.println(getFirstMaxV3(str.toCharArray()));


        System.out.println("-------------");
        str = "CABBCDE";
        System.out.println(getFirstMax(str.toCharArray()));
        System.out.println(getFirstMaxV2(str));
        System.out.println(getFirstMaxV3(str.toCharArray()));


        System.out.println("-------------");
        str = "EFGBCADABD";
        System.out.println(getFirstMax(str.toCharArray()));
        System.out.println(getFirstMaxV2(str));
        System.out.println(getFirstMaxV3(str.toCharArray()));

    }

```

输出
```
B
B
B
-------------
B
C
C
-------------
A
B
B

```

成功，第一版果然错误，后面的版本都成功返回期望值。