# 加密解密字典

## 类名

```
AddCoreValues
```

## 函数功能表

| 类名 | 参数 | 返回值 | 功能描述 |
| :--- | :--- | :--- | :--- |
| public AddCoreValues\(\) | null | null | 构造函数 |
| ~~public String getPassword\(\)~~ | ~~null~~ | ~~String~~ | ~~获取密码~~ |
| ~~public void setPassword\(String password\)~~ | ~~String~~ | ~~null~~ | ~~设置密码~~ |
| public void init\(\) | null | null | 设置加密字典 |
| public String getValue\(String key\) | String | String | 获取字典密码 |
| public void reInit\(\) | null | null | 设置解密字典 |
| public String getReValue\(String key\) | String | String | 获取字典解码 |

## 代码

```
package JavaBean.Tools.Password;

import java.util.Dictionary;
import java.util.HashMap;
import java.util.Hashtable;
import java.util.Map;

public class AddCoreValues {

    public AddCoreValues() {
        init();
        reInit();
    }

    private String password = null;

    private Map <String, String> values = null;

    private Map <String, String> reValues = null;

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public void init() {
        values = new HashMap<String, String>();
        String[] strings = {"平等", "公正", "文明", "和谐", "自由", "爱国", "敬业", "诚信", "法治", "富强", "社会主义核心价值观", "民主", "友善"};
        for (int i=0;i<=9;i++) {
            values.put(i+"", strings[i]);
            //System.out.println(i);
        }
        values.put("u", strings[10]);
        values.put("c", strings[11]);
        values.put("e", strings[12]);

        //System.out.println(values.get("2"));
    }

    public void reInit() {
        reValues = new HashMap<String, String>();

        String[] strings = {"平等", "公正", "文明", "和谐", "自由", "爱国", "敬业", "诚信", "法治", "富强", "社会主义核心价值观", "民主", "友善"};
        for (int i=0;i<=9;i++) {
            reValues.put(strings[i], i + "");
        }
        reValues.put(strings[10], "u");
        reValues.put(strings[11], "c");
        reValues.put(strings[12], "e");

    }

    public String getReValue(String key) {
        //System.out.println(key);
        String value = this.reValues.get(key);
        return value;
    }

    public String getValue(String key) {
        String value = this.values.get(key);
        return value;
    }

    public static void main(String[] args) {
        new AddCoreValues();
    }
}
```



