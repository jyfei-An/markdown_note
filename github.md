# Taskflow

创建平行或者异步任务流

## github网址

https://github.com/taskflow/taskflow

## 参考文档

https://taskflow.github.io/taskflow/index.html

# spdlog

# 循环日志文件

```c++
//将github上的spdlog库下载，include头文件包含到该项目中
#include "spdlog/spdlog.h"
#include "spdlog/sinks/stdout_color_sinks.h"
#include "spdlog/sinks/basic_file_sink.h"
#include "spdlog/sinks/rotating_file_sink.h"
#include "spdlog/async.h"

void rotating_example() {
	// Create a file rotating logger with 5mb size max and 3 rotated files
	auto max_size = 1048576 * 5;
	auto max_files = 5;

	auto rotating_file_sink = std::make_shared<spdlog::sinks::rotating_file_sink_mt>("logs/rotating1.txt", max_size, max_files);
    //多个日志器共享sink
	auto logger = std::make_shared<spdlog::logger>("some_logger_name", rotating_file_sink);
	auto logger1 = std::make_shared<spdlog::logger>("some_logger_name1", rotating_file_sink);
	auto logger2 = std::make_shared<spdlog::logger>("some_logger_name2", rotating_file_sink);
	//注册日志器
	spdlog::register_logger(logger2);
	
	std::string test1 = u8"test";
	while (1) {
		// 注册后，其它代码可以根据名称获得日志器
		auto loggertest = spdlog::get("some_logger_name2");
		if (!loggertest)
		{
			std::cout << 1 << std::endl;
		}
		logger->info(test1);
		logger1->info(test1);
		logger2->info(test1);
	}

}

int main()
{
	rotating_example();
    std::cout << "Hello World!\n";
}
```



#  ./configure

## 添加FPIC选项

https://stackoverflow.com/questions/629961/how-can-i-set-ccshared-fpic-while-executing-configure

```
./configure --enable-shared
```

## 设置安装目录

```
./configure --prefix=/localdir/
```

# googletest

## Basic Assertions

进行基本的真/假条件测试。

| Fatal assertion            | Nonfatal assertion         | Verifies             |
| -------------------------- | -------------------------- | -------------------- |
| `ASSERT_TRUE(condition);`  | `EXPECT_TRUE(condition);`  | `condition` is true  |
| `ASSERT_FALSE(condition);` | `EXPECT_FALSE(condition);` | `condition` is false |

# RapidXml

```
原项目github网址：https://github.com/dwd/rapidxml
```

```
测试代码github项目网址：git@github.com:Mr-jiayunfei/githubtest.git
```

```
用户手册：http://rapidxml.sourceforge.net/manual.html#classrapidxml_1_1memory__pool_95c49fcb056e9103ec906a59e3e01d76_195c49fcb056e9103ec906a59e3e01d76
```



## XML文件编码声明

```
xml_node<> *decl_node = writedoc.allocate_node(node_declaration);
decl_node->append_attribute(writedoc.allocate_attribute(u8"version", u8"1.0"));
decl_node->append_attribute(writedoc.allocate_attribute(u8"encoding", u8"UTF-8"));
writedoc.append_node(decl_node);
```

## 情况1(只有node)：

```
<person>
		<Name>yunfei</Name>
		<birthday>2019-12-11 19:37:58.854</birthday>
</person>
```

### 读：

```
xml_node<char>* personnode= doc.first_node(u8"person");
if (!personnode) {
return false;
}
xml_node<char>* Namenode= personnode->first_node(u8"Name");
if (!Namenode) {
return false;
}
std::string authorname;
auto value = Namenode->value();
if (value) {
if (strlen(value) != 0) {
authorname = value;
}
}
```

### 写：

```
xml_node<> *Namenode= doc.allocate_node(node_element, u8"Name");
Namenode->append_node(doc.allocate_node(node_data, "","yunfei"));
personnode->append_node(author_node);
```



## 情况2（有attribute）

```
<person id="01" gender="man">
		<Name>yunfei</Name>
		<birthday>2019-12-11 19:37:58.854</birthday>
</person>
```

### 读：

```
xml_node<char>* personnode= doc.first_node(u8"person");
if (!personnode) {
return false;
}
xml_attribute<> *att = personnode->first_attribute(u8"id");
if (att) {
auto id = att->value();
std::cout << "id:" << id << std::endl;
}
```

### 写：

```
xml_node<> *personnode= doc.allocate_node(node_element, u8"person");
personnode->append_attribute(doc.allocate_attribute(u8"id","01"));
personnode->append_attribute(doc.allocate_attribute(u8"gender","man"));
```



## 1 使用条件

从github上下载源码，将文件目录包含在自己项目目录中，在源码文件中包含下面语句

```C++
#include <rapidxml.hpp>
#include <rapidxml_print.hpp>
#include <rapidxml_utils.hpp>

using namespace rapidxml;
```

## 2 读取XML文件

	bool ReadXML(const std::string& xml_full_name) 
	{
	bool rv = false;
	
	try 
	{
		rapidxml::file<> content(xml_full_name.c_str());
	
		xml_document<> doc;
		doc.parse<0>(content.data());
	
		xml_node<char>* catelognode = doc.first_node(u8"catalog");
		if (!catelognode) {
			return false;
		}
	
		for (auto it = catelognode->first_node("book"); it; it = it->next_sibling()) 
		{
			std::string bookid;
			xml_attribute<> *att = it->first_attribute(u8"id");
			if (att) {
				bookid = att->value();
				std::cout << "bookid:" << bookid << std::endl;
			}
	
			xml_node<char>* authornode = it->first_node(u8"author");
			if (!authornode) {
				return false;
			}
			std::string authorname;
			auto value = authornode->value();
			if (value) {
				if (strlen(value) != 0) {
					authorname = value;
					std::cout << "authorname:" << authorname << std::endl;
				}
			}
	
			xml_node<char>* titlenode = it->first_node(u8"title");
			if (!titlenode) {
				return false;
			}
			std::string titlename;
			value = titlenode->value();
			if (value) {
				if (strlen(value) != 0) {
					titlename = value;
					std::cout << "titlename:" << titlename << std::endl;
				}
			}
	
			xml_node<char>* genrenode = it->first_node(u8"genre");
			if (!genrenode) {
				return false;
			}
			std::string genrename;
			value = genrenode->value();
			if (value) {
				if (strlen(value) != 0) {
					genrename = value;
					std::cout << "genrename:" << genrename << std::endl;
				}
			}
			
		}
	}
	catch (const parse_error& e) {
		std::string error_info = u8"解析XML出错，";
		error_info += e.what();
		return false;
	}
	catch (const std::exception& e) {
		std::string error_info = u8"解析XML出错，";
		error_info += e.what();
		return false;
	}
	catch (...) {
		return false;
	}
	
	return true;
	}
## 3 写入XML文件

	bool WriteXML(const std::string& xml_full_name) {
	xml_document<char> doc;
	
	///声明
	xml_node<> *decl_node = doc.allocate_node(node_declaration);
	decl_node->append_attribute(doc.allocate_attribute(u8"version", u8"1.0"));
	decl_node->append_attribute(doc.allocate_attribute(u8"encoding", u8"UTF-8"));
	doc.append_node(decl_node);
	
	xml_node<> *catalog_node = doc.allocate_node(node_element,
		u8"catalog");
	doc.append_node(catalog_node);
	
	for (int i=0;i<3;++i)
	{
		xml_node<> *book_node = doc.allocate_node(node_element, u8"book ");
		book_node->append_attribute(doc.allocate_attribute(u8"id","boolid"));
	
		xml_node<> *author_node = doc.allocate_node(node_element, u8"author ");
		author_node->append_node(doc.allocate_node(node_data, "","authorname"));
		book_node->append_node(author_node);
	
		xml_node<> *title_node = doc.allocate_node(node_element, u8"title ");
		title_node->append_node(doc.allocate_node(node_data, "", "titlename"));
		book_node->append_node(title_node);
	
		xml_node<> *genre_node = doc.allocate_node(node_element, u8"genre ");
		genre_node->append_node(doc.allocate_node(node_data, "", "genrename"));
		book_node->append_node(genre_node);
	
		catalog_node->append_node(book_node);
	}
	
	std::ofstream out(xml_full_name);
	out << doc;
	out.close();
	
	doc.clear();
	
	return true;
	}
## 4 修改XML文件（注意parse模板参数）


	bool ModifyNodeValue(const std::string& xml_full_name, const std::string& node_name, const std::string& node_value) {
	rapidxml::file<> content(xml_full_name.c_str());
	
	xml_document<> doc;
	doc.parse<rapidxml::parse_no_data_nodes>(content.data());
	
	xml_node<>* catelog_node = doc.first_node(u8"catalog");
	if (!catelog_node) {
		return false;
	}
	xml_node<>* book_node = catelog_node->first_node(u8"book");
	if (!book_node) {
		return false;
	}
	xml_node<>* author_node = book_node->first_node(u8"author");
	if (!author_node) {
		return false;
	}
	
	const std::string author_name = node_value;
	const char * text = doc.allocate_string(author_name.c_str(), strlen(author_name.c_str()));
	author_node->value(text);
	
	std::string data;
	rapidxml::print(std::back_inserter(data), doc);
	
	std::ofstream out(xml_full_name);
	out << data;
	out.close();
	}

## 5 复制节点

```
xml_node<Ch>* clone_node(const xml_node< Ch > *source, xml_node< Ch > *result=0);
xml_node<char>* clonenode = readdoc.clone_node(node1);
```



## 6 插入节点

```
void insert_node(xml_node< Ch > *where, xml_node< Ch > *child);
```



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

 

# youtube-dl

```
github网址:https://github.com/ytdl-org/youtube-dl
```

1 首先需要安装python，默认安装即可

2 使用管理员身份打开cmd窗口（不使用管理员身份打开后续安装会报错）

3 使用如下命令进行安装youtube-dl

```
pip install --upgrade youtube-dl
```

4 安装完成后，使用该工具下载youtube视频

```
example：
youtube-dl  https://www.youtube.com/watch?v=zERp1IJ0R4U&t=2787s
```

注：默认下载安装为最优视频格式，没有特殊要求的直接在后面加上url即可下载



