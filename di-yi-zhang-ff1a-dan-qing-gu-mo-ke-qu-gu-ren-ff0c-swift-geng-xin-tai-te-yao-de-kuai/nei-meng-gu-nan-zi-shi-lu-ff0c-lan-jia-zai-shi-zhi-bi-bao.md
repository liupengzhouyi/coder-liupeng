# 内蒙古男子实录，懒加载实质闭包

## 懒加载，又叫《延时加载》

## 作用：

### 1. 保证控件的延时加载

### 2. 避免开发过程中的理解包的问题

## 实例代码

* 自定义DemoLable


```
//
//  DemoLable.swift
//  懒加载
//
//  Created by 刘鹏 on 2018/10/15.
//  Copyright © 2018 刘鹏. All rights reserved.
//

import UIKit

class DemoLable: UILabel {

    //懒加载
    var dataList : [String]?
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        setupUI()
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        
        setupUI()
    }
    
    /*
    // Only override draw() if you perform custom drawing.
    // An empty implementation adversely affects performance during animation.
    override func draw(_ rect: CGRect) {
        // Drawing code
    }
    */

    private func setupUI() {
        print("设置界面")
    }
}

```
* UIViewController 代码


```
//
//  ViewController.swift
//  懒加载
//
//  Created by 刘鹏 on 2018/10/15.
//  Copyright © 2018 刘鹏. All rights reserved.
//

import UIKit

class ViewController: UIViewController {

    // 初始化并分配空间， 会提前创建
    // 移动端开发， ‘延时加载’
    // 懒加载
//    lazy var lable : DemoLable = DemoLable()
    //懒加载本质上是一个闭包
    /**
     {} 包装代码
     () 执行代码
    */
    lazy var lable = { () -> DemoLable in
        
        let l = DemoLable()
        
        //设置Lable 的属性
        
        return l
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        
        setupUI()
        
    }

    private func setupUI() {
        
        //添加到视图
        // ！解包，为了参与计算， addSubview 用 数组记录控件，数组中不允许插入
        // ？ 可选解包， 调用方法，如果 nil， 不调用方法， 但是不参与运算
        view.addSubview(lable)
        
        lable.text = "Hello"
        lable.sizeToFit()
        lable.center = view.center
        
    }

}


```








