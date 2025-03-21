# GameObject的成员变量

```c#
        // Get the GameObject's active state
        bool isactive = this.gameObject.activeSelf;
        // Get the GameObject's tag
        string tag = this.gameObject.tag;
        // Get the GameObject's layer
        int layer = this.gameObject.layer;
        // Get the GameObject's name
        string name = this.gameObject.name;
        //改名
        this.gameObject.name = "newName";
        //是否静态
        bool isStatic = this.gameObject.isStatic;
        // Get the GameObject's parent
        Transform parent = this.gameObject.transform.parent;
        // Get the GameObject's children
        Transform[] children = this.gameObject.GetComponentsInChildren<Transform>();
        // Get the GameObject's transform
        Transform transform = this.gameObject.transform;
        // Get the GameObject's components
        Component[] components = this.gameObject.GetComponents<Component>();
        // 得到渲染层
        var b = this.gameObject.sceneCullingMask;
```

‍
