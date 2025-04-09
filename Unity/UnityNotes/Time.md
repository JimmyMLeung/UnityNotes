# Time

主要内容：

Time.timescale游戏速度;

Time.deltatime游戏帧间隔时间（受游戏速度影响） = Time.unscaledDeltatime * Time.timescale;

```c#
public class MyTime : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        //游戏暂停
        Time.timeScale = 0;
        //游戏正常
        Time.timeScale = 1;
        //游戏二倍速
        Time.timeScale = 2;

    }

    // Update is called once per frame
    void Update()
    {
        //Time.deltaTime是每帧的时间间隔
        print(Time.deltaTime);

        //Time.fixedDeltaTime是物理帧的时间间隔
        print(Time.fixedDeltaTime);

        //Time.fixedTime是不受timescale影响的时间间隔
        print(Time.unscaledDeltaTime);

        //游戏从开始到现在的帧数
        print(Time.frameCount);

        //游戏从开始到现在的时间
        print(Time.time);
    }
}

```
