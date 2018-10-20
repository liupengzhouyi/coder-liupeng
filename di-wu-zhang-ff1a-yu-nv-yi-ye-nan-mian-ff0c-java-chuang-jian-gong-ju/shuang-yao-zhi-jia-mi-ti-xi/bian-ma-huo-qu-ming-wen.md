## 类名

```
CreateValues
```

## 函数表

| 函数名 | 参数 | 返回值 | 功能介绍 |
| :--- | :--- | :--- | :--- |
| public String decodeUnicode\(String unicode\) | String unicode | String | unicode转明文 |

## 代码

```
public String decodeUnicode(String unicode) {
        StringBuffer sb = new StringBuffer();

        String[] hex = unicode.split("\\\\u");

        for (int i = 1; i < hex.length; i++) {
            //System.out.println(hex[i]);
            int data = Integer.parseInt(hex[i], 16);
            sb.append((char) data);
        }
        return sb.toString();
    }

```



