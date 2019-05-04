
# buttonrpc - modern rpc framework for C++
- ZeroMQ 作为网络层
- 使用c++14开发

## Features
- 轻量级，跨平台，简单易用
- 服务端可以绑定自由函数，类成员函数，std::function对象
- 服务端可以绑定参数是任意自定义类型的函数
- 客户端与服务端自动重连机制
- 客户端调用超时选项

## Example
server:

```c++
#include "buttonrpc.hpp"

int foo(int age, int mm){
	return age + mm;
}

int main()
{
	buttonrpc server;
	server.as_server(5555);

	server.bind("foo", foo);
	server.run();

	return 0;
}
```

client: 

```c++
#include <iostream>
#include "buttonrpc.hpp"

int main()
{
	buttonrpc client;
	client.as_client("127.0.0.1", 5555);
	int a = client.call<int>("foo", 2, 3).val();
	std::cout << "call foo result: " << a << std::endl;
	system("pause");
	return 0;
}

// output: call foo result: 5

```

## Dependences
- [ZeroMQ](http://zguide.zeromq.org/page:all)


## Building
- windows vs2015 或者更高版本,  linux 添加编译选项：-std=c++1z

## Usage

- 1： 更多例子在目录 example/ 下

