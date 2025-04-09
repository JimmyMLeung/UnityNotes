# GameObject的成员方法

```c#
        GameObject obj3 = new GameObject();
        //create empty gameobject with name
        GameObject obj4 = new GameObject("obj4");
        //create gameobject with component
        GameObject obj5 = new GameObject("obj5", typeof(A));

        //添加组件
        B ogjb = obj5.AddComponent<B>();
        A ogja = obj5.AddComponent(typeof(A)) as A;


        //compare tag
        if (obj5.CompareTag("Player"))
        {
            Debug.Log("obj5 is Player");
        }

        //set Active or deactive
        obj5.SetActive(false);
        obj5.SetActive(true);
		
		//重载没卵用
        //send message  调用函数名为Test的函数
        this.gameObject.SendMessage("Test");
        this.gameObject.SendMessage("Test2", 100);
        //向下包括自己发送消息
        //this.gameObject.BroadcastMessage("Test");
        //向上包括自己发送消息
        //this.gameObject.SendMessageUpwards("Test");
```
