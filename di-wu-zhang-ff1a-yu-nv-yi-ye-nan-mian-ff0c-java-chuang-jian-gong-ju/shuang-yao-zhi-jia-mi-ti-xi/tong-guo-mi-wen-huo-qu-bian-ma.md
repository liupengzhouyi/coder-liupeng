# 通过密文获取编码，解码

## 类名

```
CreateValues
```

## 函数表

| 函数名 | 参数 | 返回值 | 功能描述 |
| :--- | :--- | :--- | :--- |
| public GetYourUnicode(String text）| String text | null | 构造函数 |
| public void init() | null | null | 初始化函数 |
| public String getMyUnicode() | null | null | 获取你的编码 |

## 代码

```
package JavaBean.Tools.Password;

public class GetYourUnicode {

    public GetYourUnicode(String text) {
        this.text = text;
        this.createAddCoreValues();
        this.setMyUnicode("");
        init();
    }

    public void init() {
        String[] hex = this.getText().split(",");
        String value = "";
        String obj = "";
        String fuqiang = new String("社会主义核心价值观");
        for (int i=0;i<hex.length;i++) {
            //System.out.println(hex[i]);
            obj = hex[i];
            if (obj.equals(fuqiang)) {
                value = this.addCoreValues.getReValue(obj);
                i++;
            } else {
                value = this.addCoreValues.getReValue(obj);
            }
            this.setMyUnicode(this.getMyUnicode() + value);
        }

    }


    public String getText() {
        return text;
    }

    public void setText(String text) {
        this.text = text;
    }

    public String getMyUnicode() {
        return myUnicode;
    }

    public void setMyUnicode(String myUnicode) {
        this.myUnicode = myUnicode;
    }

    public void createAddCoreValues() {
        this.addCoreValues = new AddCoreValues();
    }

    private AddCoreValues addCoreValues = null;

    private String text = null;

    private String myUnicode = null;

    public static void main(String[] args) {
        System.out.print(new GetYourUnicode("富强,公正,敬业,法治,和谐,法治,").getMyUnicode());
    }
}
```



