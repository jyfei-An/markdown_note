# 打印日志

```
Debug.Log("helloworld");
```



# 设置物体初试位置

```
transform.position = new Vector3(0,0,0);
```



# 控制物体移动

```
transform.position += new Vector3(0.1f, 0, 0);
```



# 控制物体旋转

```
transform.Rotate(new Vector3(0, Time.deltaTime*100, 0 ));
```

# 控制物体变大

```
transform.localScale += new Vector3(0.01f, 0.01f, 0.01f);
```

