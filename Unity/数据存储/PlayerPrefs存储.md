# PlayerPrefs存储

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
using System.Text;
using System.Threading.Tasks;
using UnityEngine;


class PlayerPrefMgr
{
    private static PlayerPrefMgr _instance;

    public static PlayerPrefMgr Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new PlayerPrefMgr();
            }
            return _instance;
        }
    }

    private PlayerPrefMgr()
    {
    }

    public static PlayerPrefMgr GetInstance()
    {
        return Instance;
    }

    public object LoadData(string keyname,Type type)
    {
        object value = Activator.CreateInstance(type);

        FieldInfo[] fields = type.GetFields();
        for (int i = 0; i < fields.Length; i++)
        {
            string loadkeyname = keyname + "_" + type.Name +
                "_" + fields[i].FieldType.Name + "_" + fields[i].Name;
            fields[i].SetValue(value, LoadValue(loadkeyname, fields[i].FieldType));
        }
        return null;
    }

    private object LoadValue(string keyname, Type type)
    {
        if (type == typeof(int))
        {
            return PlayerPrefs.GetInt(keyname, 0);
        }
        else if (type == typeof(float))
        {
            return PlayerPrefs.GetFloat(keyname, 0.0f);
        }
        else if (type == typeof(string))
        {
            return PlayerPrefs.GetString(keyname, "");
        }
        else if (type == typeof(bool))
        {
            return PlayerPrefs.GetInt(keyname, 0) == 1;
        }
        else if (type == typeof(double))
        {
            return PlayerPrefs.GetFloat(keyname, 0.0f);
        }
        else if (typeof(IList).IsAssignableFrom(type))
        {
            int count = PlayerPrefs.GetInt(keyname, 0);
            if (count > 0)
            {
                IList obj = Activator.CreateInstance(type) as IList;
                for(int i = 0; i < count; i++)
                {
                    obj.Add(LoadValue(keyname + "_" + i, type.GetGenericArguments()[0]));
                }
            }
        }
        else if (typeof(IDictionary).IsAssignableFrom(type))
        {
            int count = PlayerPrefs.GetInt(keyname, 0);
            if (count > 0)
            {
                IDictionary obj = Activator.CreateInstance(type) as IDictionary;
                for (int i = 0; i < count; i++)
                {
                    obj.Add(LoadValue(keyname + "_" + "key_" + i, type.GetGenericArguments()[0]), 
                        LoadValue(keyname + "_" + "value_" + i, type.GetGenericArguments()[1]));
                }
            }
        }
        else
        {
            return LoadData(keyname, type);
        }


        return null;
    }

    public void SaveData(string keyname, object data)
    {
        Type type = data.GetType();

        FieldInfo[] fields = type.GetFields();
        for (int i = 0; i < fields.Length; i++)
        {
            string savekeyname = keyname + "_" + type.Name +
                "_" + fields[i].FieldType.Name + "_" + fields[i].Name;
            SaveValue(savekeyname, fields[i].GetValue(data));
        }
    }

    private void SaveValue(string keyname, object value)
    {
        Type type = value.GetType();
        if (type == typeof(int))
        {
            PlayerPrefs.SetInt(keyname, (int)value);
        }
        else if (type == typeof(float))
        {
            PlayerPrefs.SetFloat(keyname, (float)value);
        }
        else if (type == typeof(string))
        {
            PlayerPrefs.SetString(keyname, (string)value);
        }
        else if (type == typeof(bool))
        {
            PlayerPrefs.SetInt(keyname, (bool)value ? 1 : 0);
        }
        else if (type == typeof(double))
        {
            PlayerPrefs.SetFloat(keyname, (float)value);
        }
        else if (typeof(IList).IsAssignableFrom(type))
        {
            int index = 0;
            IList list = (IList)value;
            PlayerPrefMgr.Instance.SaveValue(keyname, list.Count);
            foreach (object obj in list) 
            {
                PlayerPrefMgr.Instance.SaveValue(keyname + "_" + index, obj);
                index++;
            }
        }
        else if(typeof(IDictionary).IsAssignableFrom(type))
        {
            IDictionary dict = (IDictionary)value;
            PlayerPrefMgr.Instance.SaveValue(keyname, dict.Count);
            int index = 0;
            foreach (object key in dict.Keys)
            {
                PlayerPrefMgr.Instance.SaveValue(keyname + "_" + "key_" + index, key);
                PlayerPrefMgr.Instance.SaveValue(keyname + "_" + "value_" + index, dict[key]);
                index++;
            }
        }
        else
        {
            PlayerPrefMgr.Instance.SaveData(keyname, value);
        }
    }
}
```
