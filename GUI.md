# GUI

## 自定义皮肤

GUI.color <span data-type="text" style="color: var(--b3-font-color11);">//设置全局颜色；</span>

GUI.backgroundColor <span data-type="text" style="color: var(--b3-font-color11);">//单独显示区域改变背景颜色；</span>

GUI.contentColor <span data-type="text" style="color: var(--b3-font-color11);">//改变文本颜色；</span>

GUI.skin = skin <span data-type="text" style="color: var(--b3-font-color11);">//类似 GUI.Style 但这是全局的</span>

‍

## 自动布局

GUILayout.Button、GUILayout.Label等，用 GUILayout 代替 GUI 使用控件可以使其自动布局；

GUILayout.BeginVertial() and GUILayout.EndVVertical() // 垂直自动布局

GUILayout.BeginHorisiontal() and GUILayout.EndHorsiontal() // 水平自动布局

GUI.BeginArea(new Rect()) and GUI.EndArea(); //控制自动布局的开始位置；

‍

### 自动布局的参数：

GUILayout.Wiidth(???)；//固定宽高

GUILayout.Height(???);

GUILayoutMaxWidth(..); //最大最小

GUILayoutMinHeight();

GUILayout.ExpandWidth(true) //允许跟随前面的宽度

GUILayout.ExpandHeight(false) //默认false;

‍

## 弹窗：

GUI.Winodow(); //普通窗口

GUI.ModalDow()； //模态窗口，窗口弹出时，其它控件失效；

GUI.Window() + GUI.Dragwindow() //可拖动窗口；

弹窗需要一个 int参数、无返回值的委托参数，一般搭配下列方法：

```cpp
private void DrawTexture(int id){}
```

‍

## 图片：

参数；

1、Rect pos //图片的位置与大小

2、Texture image //图片

3、bool alpha blending //是否混合绘制

4、ScaleMode mode //缩放模式：

	StretchToFill(全部填充）,ScaleAndCrop（缩放并裁剪）,ScaleToFit（缩放并自适应）；

5、float WH 宽高比；

<span data-type="text" style="color: var(--b3-font-color10);">GUI.DrawTexture();</span>

```c#
GUI.DrawTexture(imageRect, background, mode, alpha, WH);
```

## 滑轮显示：

参数：

* scrollRect //滑动窗口的大小；
* scrollPosition//当前滑窗的位置，会实时返回；
* scrollViewRect//显示区域的实际大小，当宽度大于滑窗，会出现水平滑动条，高度同理；

```c#
        scrollPosition = GUI.BeginScrollView(scrollRect, scrollPosition, scrollViewRect);
        for(int i = 0; i < strs.Length; i++)
        {
            GUI.Label(new Rect(0, i * 50, 100, 20), strs[i]);
        }
        GUI.EndScrollView();
```

‍

## 多选框：

isXXX = GUI.Toggle（Rect rect，bool isXXX， string name）

只有两种状态，isXXX 为 true 时 为 OnNormal； isXXX 为 false 时 为 Normal；

每次调用都会返回状态值；

示例：

```c#
        isMusicOn = GUI.Toggle(new Rect(320, 100, 200, 20), isMusicOn, "Music", setting_style);
        isBackgroundMusicOn = GUI.Toggle(new Rect(320, 120, 200, 20), isBackgroundMusicOn, "Background Music", setting_style);
```

‍

## 单选框：

	基于 GUI.Toggle 实现；

一般用法：

```c#
private int nowIndex = 1;
...	
	if(GUI.Toggle(..., nowIndex == 1, ...){
		nowIndex = 1;
	}
	else if(GUI.Toggle(..., nowIndex == 2, ...){
		nowIndex = 2;
	}
	else if(GUI.Toggle(..., nowIndex == 3, ...){
		nowIndex = 3;
	}
...
```

‍

## 滑动条：

	<span data-type="text" style="color: var(--b3-font-color11);">int nowValue = GUI.Slider(Rect pos, int nowValue, int minValue, int maxValue);</span>

## 文本输入：

普通输入：

	<span data-type="text" style="color: var(--b3-font-color11);">string text = GUI.TextField(Rect pos,string text,GUIStyle style);</span>

密码输入: 输入会自动显示城 ‘*’；

	<span data-type="text" style="color: var(--b3-font-color11);">string password = GUI.PasswordField(Recr pos,string password, '*' ,GUiStyle style);</span>

‍

## 工具栏：

```c#
\\工具栏
toolIndex = GUI.Toolbar(toolRect, toolIndex, toolInfos);
\\网格
toolIIndex = GUI.SelectionGrid(toolIRect, toolIIndex, toolIInfos, toolCount);
```

‍

‍
