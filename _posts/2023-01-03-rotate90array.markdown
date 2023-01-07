---
title:  "Rotate90˚"
excerpt: ""

categories:
  - Algorithm
tags:
  - [Algorithm, Go]

toc: true
toc_sticky: true
 
date: 2023-01-03
last_modified_at: 2023-01-07
---

# rotate90

### 5x5 matrix  

| | | | | |
|---|---|---|---|---|
|00|01|02|03|04|
|10|11|12|13|14|
|20|21|22|23|24|
|30|31|32|33|34|
|40|41|42|43|44|

### rotate 90   

| | | | | |
|---|---|---|---|---|
|04|14|24|34|44|
|03|13|23|33|43|
|02|12|22|32|42|
|01|11|21|31|41|
|00|10|20|30|40|


```
package main
import "log"

func main() {
    log.Println(Rotate90(map[int]map[int]string{
         0 : { 0 : "00", 1 : "01", 2 : "02", 3 : "03", 4 : "04" }, 
         1 : { 0 : "10", 1 : "11", 2 : "12", 3 : "13", 4 : "14" }, 
         2 : { 0 : "20", 1 : "21", 2 : "22", 3 : "23", 4 : "24" }, 
         3 : { 0 : "30", 1 : "31", 2 : "32", 3 : "33", 4 : "34" },
         4 : { 0 : "40", 1 : "41", 2 : "42", 3 : "43", 4 : "44" }}))
}

func Rotate90(image map[int]map[int]string) map[int]map[int]string {
    targetNum:= len(image) - 1
    for i := 0; i < len(image) - 1;i++ {
        // change values
        for j := i; j < targetNum - i; j++ {
            temp := image[i][j]
            image[i][j] = image[j][targetNum-i]
            image[j][targetNum-i] = image[targetNum-i][targetNum-j]
            image[targetNum-i][targetNum-j] = image[targetNum-j][i]
            image[targetNum-j][i] = temp
        }
    }
    return image
}
```

```
result : map[
    0:map[0:04 1:14 2:24 3:34 4:44] 
    1:map[0:03 1:13 2:23 3:33 4:43] 
    2:map[0:02 1:12 2:22 3:32 4:42] 
    3:map[0:01 1:11 2:21 3:31 4:41] 
    4:map[0:00 1:10 2:20 3:30 4:40]]

```


execution time : **O(N<sup>2</sup>)**