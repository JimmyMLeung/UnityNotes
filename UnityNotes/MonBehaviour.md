# MonBehaviour

***MonoBehaviour的重要内容：***

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class New : MonoBehaviour
{
    public New2 othernew;
    // Start is called before the first frame update
    void Start()
    {
        //ouput the name of the GameObject
        //Debug.Log("Perform operation");
        //Debug.Log(this.gameObject.name);

        //output the position, rotation and scale of the GameObject
        /*        Debug.Log(this.transform.position);
                Debug.Log(this.transform.rotation);
                Debug.Log(this.transform.localScale);*/

        //get the New2 component from the GameObject
/*        New2 new2 = this.GetComponent<New2>();
        Debug.Log(new2.gameObject.name);
        new2 = this.GetComponent(typeof(New2)) as New2;
        Debug.Log(new2.gameObject.name);
        new2 = this.gameObject.GetComponent("New2") as New2;
        Debug.Log(new2.gameObject.name);*/

        //get the New2 component from the parent or children(默认包括自己本身)
        New2[] new2s = this.GetComponentsInChildren<New2>(true);
        Debug.Log("Children: " + new2s.Length);

        //true or false 用于控制是否搜索失活子对象
        //New2[] new3s = this.GetComponentsInChildren<New2>(false);
        //Debug.Log("Children: " + new2s.Length);

        New2[] new2s2 = this.GetComponentsInParent<New2>();
        Debug.Log("Parent: " + new2s2.Length);

        //get by list
        List<New2> new2s3 = new List<New2>();
        this.GetComponents<New2>(new2s3);
        Debug.Log("my" + new2s3.Count);


       for(int i = 1; i < new2s.Length; i++)
       {
           new2s[i].gameObject.SetActive(false);
       }

/*        for (int i = 1; i < new2s.Length; i++)
        {
            new2s[i].enabled = false;
        }*/



    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

***通过变量关联挂载A脚本的对象，可以在其他脚本中使A脚本失活：***

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class B : MonoBehaviour
{
    public A a;

    // Start is called before the first frame update
    void Start()
    {
        A t = a.GetComponent<A>();
        if(t != null )
            t.enabled = false;

    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

***两脚本挂载在一个对象中，可以使另一脚本失活***

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class A : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        B b = this.GetComponent<B>();
        if (b != null)
        {
            b.enabled = false;
        }
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```
