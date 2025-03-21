# Random

## Unity.Random:

int randomNum = Random.Range(0,100)   <span data-type="text" style="color: var(--b3-font-color11);">//左包含，右不包含</span>

float randomFNum = Random.Range(0.0f,100.0f) <span data-type="text" style="color: var(--b3-font-color11);">//左包含，右包含</span>

## System.Random:

System.Random r = new System.Random();

int num = r.Next(10,100);

```c#
        #region 知识点一 随机数
        //Unity中的随机数
        //Unity当中 的Random类 此Random(Unity)非彼Random（C#）
        //使用随机数 int重载 规则是 左包含 右不包含
        //0~99之间的数
        int randomNum = Random.Range(0, 100);
        print(randomNum);
        //float重载 规则是 左右都包含
        float randomNumF = Random.Range(1.1f, 99.9f);

        //C#中的随机数
        //System.Random r = new System.Random();
        //r.Next(0, 100);
        #endregion
    }
```
