# GameObject的静态方法

**创建几何体对象**

```c#
        //创建几何体对象
        GameObject cube = GameObject.CreatePrimitive(PrimitiveType.Cube);
        //设置对象的名字
        cube.name = "Cube";
        //设置对象的位置
        cube.transform.position = new Vector3(0, 0, 0);
        //设置对象的旋转
        cube.transform.rotation = Quaternion.Euler(0, 0, 0);
        //设置对象的缩放
        cube.transform.localScale = new Vector3(1, 1, 1);

		//创建一个空对象
        GameObject empty = new GameObject("Empty");
        //设置对象的父对象
        cube.transform.parent = empty.transform;
```

**GameObject搜索对象的方法**

***注！无法搜索失活对象；单个对象搜索时，如果场景中存在多个相同对象时无法得到确定的对象***

```c#
        //根据对象名查找对象
        GameObject cube1 = GameObject.Find("Cube");
        Debug.Log(cube1?.name);

        //设置对象的标签
        cube.tag = "Player";

        //根据标签查找对象
        GameObject[] cubes = GameObject.FindGameObjectsWithTag("Player");
        foreach (var item in cubes)
        {
            Debug.Log(item.name);
        }

        //根据路径查找对象
        GameObject cube2 = GameObject.Find("/Empty/Cube");
        Debug.Log(cube2?.name);

        //继承自Object的方法
        //查找脚本对象，返回一个带该脚本的脚本对象
        MyGameObject myGameObject = GameObject.FindObjectOfType<MyGameObject>();
        Debug.Log(myGameObject?.gameObject.name);

		//对象克隆
        GameObject obj = GameObject.Instantiate(cube2);
        GameObject obj2 = GameObject.Instantiate(obj);
```

得到对象的方式目前有两种：

1、通过上面的API查找

2、创建公有变量，并在外部关

‍

**对象销毁**

***注！对象销毁一般发生在下一帧***

```c#
		//一般对象销毁发生在下一帧
        //销毁对象
        GameObject.Destroy(obj);
        //延迟销毁对象
        GameObject.Destroy(obj, 5);

        //立即销毁对象
        //GameObject.DestroyImmediate(obj2);

        //场景切换时不销毁对象
        GameObject.DontDestroyOnLoad(obj2);
```

‍

‍

‍
