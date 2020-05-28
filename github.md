

googletest



### Basic Assertions

进行基本的真/假条件测试。

| Fatal assertion            | Nonfatal assertion         | Verifies             |
| -------------------------- | -------------------------- | -------------------- |
| `ASSERT_TRUE(condition);`  | `EXPECT_TRUE(condition);`  | `condition` is true  |
| `ASSERT_FALSE(condition);` | `EXPECT_FALSE(condition);` | `condition` is false |



# nlohmann/json

```
github网址：https://github.com/nlohmann/json
```

```
博客网址：https://www.cnblogs.com/LuckCoder/p/11875918.html
```

1 从github上下载json源代码，链接如下：https://github.com/nlohmann/json.git

2 利用json在线解析网址测试json配置文件格式是否正确，链接如下：https://www.json.cn/

3 将下载下来的json项目的include头文件包含在自己的项目中的包含目录（VS）

4 在使用json的cpp文件开始加上下面两条语句（必须完成第三步，否则会编译出错）

```
#include <nlohmann/json.hpp>
using json = nlohmann::json;
```

##  读取json文件代码如下：

```
std::map<std::string, std::map<std::string, std::string>> ReadJsonFile(
const std::string &filepath) {
  std::map<std::string, std::map<std::string, std::string>> json_config;
  std::ifstream file(filepath);
  if (!file.is_open()) {
    file.clear();
    return json_config;
  }
  file.seekg(0, std::ios::end);
  int file_size = file.tellg();
  file.seekg(0, std::ios::beg);

  char *buf = new char[file_size + 1];
  memset(buf, 0, file_size + 1);
  file.read(buf, file_size);
  std::string con(buf);
  delete[]buf;
  file.close();

  try {
    json json_content;
    json_content = json::parse(con);
    json_config =
      json_content.get<std::map<std::string, std::map<std::string, std::string>>>();
  } catch (...) {
    return json_config;
  }

  return json_config;
}
```

 

## 写入json文件代码如下：

```
bool WriteJsonFile(const std::string& file_path,
                   std::map<std::string,  std::map<std::string, std::string>> &json_config) {
  std::ofstream file(file_path,
                     std::ios::trunc | std::ios::out | std::ios::in);

  if (!file.is_open()) {
    return false;
  }

  json js;
  for (auto p : json_config) {
    std::string objectname = p.first;
    std::map<std::string, std::string> object_config = p.second;
    json jsobject;
    for (auto k : object_config) {
      jsobject[k.first] = k.second;
    }
    js[objectname] = jsobject;
  }

  file << js;
  return true;
}
```

5 测试代码如下：

```
void TestReadJson() {
  std::map<std::string, std::map<std::string, std::string>> json_config =
        ReadJsonFile("config.json");
  if (json_config.empty()) {
    return ;
  }
  for (auto p : json_config) {
    std::cout << p.first << std::endl;
    for (auto k : p.second) {
      std::cout << "(" << k.first << "," << k.second << ")" << std::endl;
    }
  }
}

void TestWriteJson() {
  std::map<std::string, std::map<std::string, std::string>> json_config;
  json_config["username"] = { { "username1","admin" },{ "username2","administrator" } };
  json_config["udpconfig"] = { { "ipaddress","127.0.0.1" },{ "port","1234" } };
  WriteJsonFile("config.json", json_config);
}
```

 

注：要使上述代码可以直接运行，还需包含下面三个头文件

```
#include <iostream>
#include <fstream>
#include <map>
```

 