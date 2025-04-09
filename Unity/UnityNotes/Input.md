# Input

## 鼠标屏幕坐标：

屏幕坐标的原点位于左下角：

	<span data-type="text" style="background-color: var(--b3-font-background10);">Input.mouseposition鼠标的在屏幕坐标上的位置</span>

‍

## 1、获取鼠标输入：

参数为0、1、2：0是鼠标左键，1是鼠标右键，2是鼠标中键

### 检测鼠标按下：

	<span data-type="text" style="background-color: var(--b3-font-background10);">Input.GetMouseButtonDown(0)</span>;

### 检测鼠标弹起：

	Input.GetMouseButtonUp(0);

### 检测鼠标长按，按下或弹起：

	Input.GetMouseButton(0);

‍

```c#
        //鼠标按下相关检测 对于我们来说
        //比如： 1.可以做 发射子弹
        //      2.可以控制摄像机 转动

        //鼠标按下一瞬间 进入
        //0左键 1右键 2中键
        //只要按下的这一瞬间 进入一次
        if( Input.GetMouseButtonDown(0) )
        {
            print("鼠标左键按下了");
        }
       
        //鼠标抬起一瞬间 进入
        if( Input.GetMouseButtonUp(0) )
        {
            print("鼠标左键抬起了");
        }
        
        //鼠标长按按下抬起都会进入
        //就是 当按住按键不放时 会一直进入 这个判断
        if( Input.GetMouseButton(1))
        {
            print("右键按下");
        }
```

‍

## 2、检测键盘输入：

	<span data-type="text" style="background-color: var(--b3-font-background10);">使用 GetKeyDown、GetKeyUp、GetKey，参数使用KeyCode.X</span>, 示例如下：

```c#
        #region 知识点三 检测键盘输入
        //比如说 按一个键释放一个技能或者切换武器 等等的操作

        //键盘按下
        if( Input.GetKeyDown(KeyCode.W) )
        {
            print("W键按下");
        }

        //传入字符串的重载
        //这里传入的 字符串 不能是大写的 不然会报错
        //只能传入小写字符串
        if( Input.GetKeyDown("q") )
        {
            print("q按下");
        }
       
        //键盘抬起
        if( Input.GetKeyUp(KeyCode.W) )
        {
            print("W键抬起");
        }
        
        //键盘长按
        if( Input.GetKey(KeyCode.W) )
        {
            print("W键长按");
        }

```

‍

## 3、轴输入：WS

参数为字符串 ： Mouse X（检测鼠标水平移动）、 Mouse Y、 Vertical(检测键盘WS键）、 Horizontal(检测键盘AD键）

	GetAxis("Mouse X") 返回 float 从 -1 到 1，负代表左，正代表右，值多大代表鼠标移动越多。

<span data-type="text" style="background-color: var(--b3-font-background10);">	GetAxisRaw(&quot;XX&quot;) 只返回  -1 或 1</span>

```c#
        #region 知识点四 检测默认轴输入
        //我们学习鼠标 键盘输入 主要是用来
        //控制玩家 比如 旋转 位移等等
        //所以Unity提供了 更方便的方法 来帮助我们控制 对象的 位移和旋转

        //键盘AD按下时 返回 -1到1之间的变换
        //相当于 得到得这个值 就是我们的 左右方向 我们可以通过它来控制 对象左右移动 或者左右旋转
        float h = Input.GetAxis("Horizontal");
        //print(h);

        //键盘SW按下时 返回 -1到1之间的变换
        //得到得这个值 就是我们的 上下方向 我们可以通过它来控制 对象上下移动 或者上下旋转
        //print(Input.GetAxis("Vertical"));

        //鼠标横向移动时 -1 到 1 左 右
        //print(Input.GetAxis("Mouse X"));

        //鼠标竖向移动时  -1 到 1 下 上
        //print(Input.GetAxis("Mouse Y"));

        //我们默认的 GetAxis方法 是有渐变的 会总 -1~0~1之间 渐变 会出现小数

        //GetAxisRaw方法 和 GetAxis使用方式相同
        //只不过 它的返回值 只会是 -1 0 1 不会有中间值
        #endregion
```
