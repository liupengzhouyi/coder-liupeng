# 私钥与unicode的编码

## 类名

```
CreateValues
```

## 函数表

| 函数名 | 参数 | 返回值 | 功能描述 |
| :--- | :--- | :--- | :--- |
| public CreateValues\(String password, String code\) | String password, String code | null | 构造函数 |
| public void createUserCode\(\) | null | null | 创建用户 |
| public void createCoreValues\(\) | null | null | 创建新的编码 |
| public void setPassword\(String password\) | String password | null | 设置密码 |
| public AddCoreValues getAddCoreValues\(\) | null | AddCoreValues | 获取加密工具 |
| public void setAddCoreValues\(AddCoreValues addCoreValues\) | AddCoreValues addCoreValues | null | 设置加密工具 |
| public String getCode\(\) | null | String | 获取编码 |
| public void setCode\(String code\) | String code | null | 设置编码 |
| public String getCoreValues\(\) | null | String | 获取带密码的编码 |
| public void setCoreValues\(String coreValues\) | String coreValues | null | 设置带密码的编码 |

## 代码

```
package JavaBean.Tools.Password;

public class CreateValues {

    public CreateValues(String password, String code) {
        this.setPassword(password);
        this.setCode(code);
        this.coreValues = coreValues;
        this.createUserCode();
    }

    public void createUserCode() {
        // password : 私钥：151136161191
        // code : 我的unicode：u6838u5c102ec99e3u4c101ec102e7u503c99eu89c99e2
        String[] hex = code.split("u");
        char[] arrays = this.getPassword().toCharArray();
        int temp = 0;
        this.setCoreValues("");
        for (int i=1;i<hex.length;i++) {
            //System.out.println(hex[i]);
            hex[i] = "u" + arrays[temp] + hex[i];
            temp = temp + 1;
            if (temp == 12) {
                temp = 0;
            }
            this.setCoreValues(this.getCoreValues() + hex[i]);
        }
    }

    public void createCoreValues() {
        this.addCoreValues = new AddCoreValues();
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public AddCoreValues getAddCoreValues() {
        return addCoreValues;
    }

    public void setAddCoreValues(AddCoreValues addCoreValues) {
        this.addCoreValues = addCoreValues;
    }

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public String getCoreValues() {
        return coreValues;
    }

    public void setCoreValues(String coreValues) {
        this.coreValues = coreValues;
    }

    private String password = null;

    private AddCoreValues addCoreValues = null;

    private String code = null;

    private String coreValues = null;

    public static void main(String[] args) {

        System.out.print(new CreateValues("151136161191", "u6838u5c102ec99e3u4c101ec102e7u503c99eu89c99e2").getCoreValues());
    }
}
```



