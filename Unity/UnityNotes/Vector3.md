# Vector3

‍

一个三维变量的容器，一般用于表示（x,y,z)三维坐标

**this.transform.position 使用 Vector3 存储的，但position的x，y，z是不能单独改变的**

<span data-type="text" style="color: var(--b3-font-color8);">例如：this.transform.positon.x = 1 </span>**是非法的**<span data-type="text" style="color: var(--b3-font-color8);">；</span>

**正确的方法**： this.transform.position = new Vector3(1, this.transform.position.y,...);

**or:** 	Vector3 vec3 = this.transform.position;

	vec3.x = 1;

‍

**GameObject的位移**：通过 position + new Vector(..,...,...)可以实现位移；

**Vector3中的静态变量**：

	Vector3.forward (0,0,1) 表示向前，Z轴上为1；

	Vector3.backwad (0,0,-1);

	Vector3.left (-1,0,0) 向左，X轴上为-1；

	Vector3.right (1,0,0);

	Vector3.up;

	Vector3.down;

‍

**一般位移的方式：方向 * 速度 * 时间 ——**  <span data-type="text" style="background-color: var(--b3-font-background6);">即：Vector3.forward(方向） * 1(速度) * Time.deltatime(时间);</span>

示例：

	<span data-type="text" style="background-color: var(--b3-font-background10);">this.transform.Translate(Vector3.forward * 1 * Time.deltaTime);  </span>**注！默认第二个参数为 Space.Self 即物体本地坐标**

如果使用世界坐标应改为：

	<span data-type="text" style="background-color: var(--b3-font-background10);">this.transform.Translate(this.transform.forward * 1 * Time.deltaTime,Space.World)</span> 其中 **this.transform.forward** 表示本地坐标的方向。

也可以不使用方法：

	<span data-type="text" style="background-color: var(--b3-font-background10);">this.transform.position += this.transform.forward * 1 * Time.deltatime;</span>

‍

**GameObject的旋转**

<span data-type="text" style="background-color: var(--b3-font-background12);">使用 this.transform.Rotate() 进行自转； 使用 this.transform.RotateAround() 进行绕点旋转</span>；

**例如：**

	this.transform.Rotate(Vector3.up * 10 * Time.deltatime)；

	this.transform.RoateAround(Vector.zero, Vector3.up * 10 * Time.deltatime) 绕原点的Y轴进行旋转；

**注！this.transform.rotation 是个四元数 且一般使用 Quaternion.Euler()  来赋值 Euler表示欧拉角**

例如：

	this.transform.rotation = Quaternion.Euler(0, this.transform.rotation.eulerangle.y, 0); 只保留偏航角

欧拉角rpy;滚轮角（Roll）Z轴、俯仰角（Pitch）X轴、偏航角（yawing）Y轴，用 Vector3 存储。**注！不同坐标表示可能有其他解释，这里只是Unity的表示**

‍

**GameObject的缩放与看向**

缩放没有函数，看向用LookAt；

this.transform.LookAt(Transform t) 使用该的Z轴（默认）一直指向某对象。  
{: id="20250307000256-z91xfv8" style="background-color: var(--b3-font-background2); --b3-parent-background: var(--b3-font-background2);" updated="20250307001112"}

this.transform.lossyscale（相对世界坐标的大小）、 this.transform.localscale (相对父对象的大小)，同样用  Vector3存储.  
{: updated="20250307001112" id="20250307000432-tbtidmt" style="background-color: var(--b3-font-background2); --b3-parent-background: var(--b3-font-background2);"}

‍

‍

‍

## Vector3的数学运算：

Vector3.Dot（.....）：向量点乘，从空间上看，A·B 等于A向量在B向量上的投影，可用于判断向量之间的夹角是钝角还是锐角，<span data-type="text" style="color: var(--b3-font-color8);">换言之可以判断B点相对A点的前后</span>；

Vector3.Angle（.....）可以直接得出角度;

也可以：

```c#
        float pj = Vector3.Dot(this.transform.forward, (targetObj.transform.position - this.transform.position).normalized);
        float rad = Mathf.Acos(pj);
        float angle = rad * Mathf.Rad2Deg;
```

两单位向量点乘可以得到余弦值，反余弦后得到弧度，再转得到角度：

具体推导：

$$
\begin{align} \cos(\alpha) &= \overrightarrow{OA} \cdot \overrightarrow{OB} \, {\div} \,\left | OA \right |\\\cos(\alpha) &= \overrightarrow{e_{A}} \cdot \overrightarrow{e_{B}} \, {\div} \, \left | e_{A}\right | \\\cos(\alpha) &= \overrightarrow{e_{A}} \cdot \overrightarrow{e_{B}}\end{align}
$$

Vector3.Cross(......)叉乘，空间上得到两向量所在平面的法向量，<span data-type="text" style="color: var(--b3-font-color8);">并且A*</span>*B，法相量向上，B** <span data-type="text" style="color: var(--b3-font-color8);">A，法向量向下，由此可以判断B相对A的左右</span>

‍

‍
