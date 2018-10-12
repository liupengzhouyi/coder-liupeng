# 新建一个APP
## 如图所示
## 代码添加按钮，按钮绑定事件
### 代码部分
```
class ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        //添加一个视图
        let v = UIView(frame: CGRect(x: 100, y: 100, width: 200, height: 200))
        //设置视图的背景
        v.backgroundColor = UIColor.red
        //控制器绑定视图
        self.view.addSubview(v)
        //新建一个按钮
        let btn = UIButton(type: UIButton.ButtonType.detailDisclosure)
        // 视图添加按钮
        v.addSubview(btn)
        //按钮绑定事件
        btn.addTarget(self, action: #selector(clickMe), for:UIControl.Event.touchUpInside)
    }

    //被按钮绑定的事件
    @objc func clickMe() ->() {
        print(#function)
        print("Hello,IOS")
    }
}
```
### 效果
![](/assets/屏幕快照 2018-10-09 上午11.25.44.png)















