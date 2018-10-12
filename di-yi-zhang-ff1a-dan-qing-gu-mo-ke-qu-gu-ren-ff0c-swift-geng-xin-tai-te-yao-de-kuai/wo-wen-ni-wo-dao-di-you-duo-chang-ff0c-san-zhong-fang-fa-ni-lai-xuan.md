# 求字符串的长度
## 代码
```
// 计算s字符串的长度
    func demo7() {
        let str : String = "abcdefg"
        
        //方法一
        //在画UTF-8编码中，每一个汉子都是3个字节
        print(str.lengthOfBytes(using: String.Encoding.utf8))
        
        //方法二
        print(str.count)
        
        // 方法三
        let strI = str as NSString
        print(strI.length)
    }
```