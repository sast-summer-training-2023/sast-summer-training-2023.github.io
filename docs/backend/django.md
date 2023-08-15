# Django

:cheese_wedge: 前置知识：Web, Python

:mortar_board: 讲师：高焕昂 @c7w

:date: 日期：7 月 22 日星期六

---

Django: The web framework for perfectionists with deadlines. 

作为适合初学者入门前后端分离开发范式的开发框架，Django 可以让你在距离 DDL 还有几个小时的时候优雅地摆烂。在本节课程中你将了解到：

1. 前后端分离开发基础：基础知识、前后端对接交流的方式、前后端对接中的安全问题、在前后端分离的开发范式中后端的作用

2. Django 框架中路由、模型、视图、单元测试的相关介绍

:movie_camera: [课程回放](https://www.bilibili.com/video/BV1WV411L7mq)

:books: [作业](https://github.com/sast-summer-training-2023/sast2023-django)


## 课前准备

+ 安装测试工具 [PostMan](https://www.postman.com/) 
+ 在安装了 Python 并学会了使用包管理工具安装包后，使用如下命令安装 `django` 环境：
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple django
```


## 课程讲义

### 前后端分离开发基础

#### 知识回顾：Web 基础

Web 基础课程中对于前后端分离开发基础的介绍：

+ 对于绝大部分动态网页而言，“动态”的是具体的数据，网页的框架、呈现给用户的界面是“静态”的
+ 把“动态”数据填入“静态”模板这一过程其实可以放到客户端进行
+ “前端”指的就是用户界面，“后端”指的就是数据与业务逻辑，两者可以完全分离



#### “服务端渲染”与“客户端渲染”

在《程序设计训练》课程中，我们会接触“**服务端渲染**”的处理方式，即后端将网页在本地“**渲染**”（对网页模板进行占位符替换）后，将“渲染”好的网页直接发给用户。这样做服务器端需要解析 HTML 模板，对服务器资源的占用较大；同时前后端紧密耦合，不利于项目的高效开发。

取而代之地，“**客户端渲染**”的方式则是将上述开发过程一分为二：分为前端团队与后端团队两支队伍，前端团队专注于 UI 设计与实现，后端团队只需要提供相应的 API 接口负责具体展示的数据。在用户请求时，服务端先将一个带有逻辑功能（JS 代码）的网页模板发给用户，用户浏览器打开后通过逻辑代码的指示再去请求后端 API 具体要展现什么数据；在拿到后端接口返回的相应数据后，前端再通过自己的逻辑代码将内容“渲染”到浏览器中。

!!! 试一试
    试着对以下网站进行分析，它们是“客户端渲染”还是“服务端渲染”？
    
    + GitHub.com
    + Bilibili.com
    + 网络学堂 2018
    
    提示：一个比较简单的判断方式是在网页要展示的数据还在请求时，网页是显示占位符（如提示 Loading... 之后将数据替换在这个地方）还是完全空白。当然，更加合理的做法是打开网页“审查元素”后进入“网络”选项卡，试着理解每一次请求都在做什么。后端返回给浏览器的，是整个网页，还是仅含有网页中内容的数据包？



#### 后端的作用

在“客户端渲染”的语境下，后端可以理解成**与前端交互数据**，并**操作与管理数据库**的一段逻辑代码。接下来我们以一个视频网站为例进行讲解。

**与前端交互内容**包含两个方面：一方面是后端面对前端的查询请求（**GET** 方法）要返回相应的数据供前端渲染，比如用户点开网页后首页要进行视频推荐，用户可以查看自己的个人信息；另一方面是后端面对前端的修改请求（**POST** 方法、**PUT** 方法、**DELETE **方法，分别对应创建、修改、删除）要在**检查**后做出响应，比如用户可以上传视频、发表评论、修改个人信息、删除视频等等。做检查是很重要的一部分，因为前后端分离的开发范式中十分重要的一个思想是**后端不相信前端**，即后端接受到的任何请求除了是前端发来的之外，还有可能是攻击者发来的，因此必须对请求内容做出相应检查。

后端与前端的交互通过网络请求的格式进行，而最常用的数据规范便是 **JSON 格式**（JavaScript Object Notation）。JSON 将数据组织成键值对的形式，其值涵盖的类型包括：object, array, number, string, Boolean (true / false) 和 null。很多高级语言都支持 JSON 格式与自身自带的 HashMap 容器的高效转换，比如在 Python 中，`json` 库可以将 JSON 字符串与 dict 进行转换。

**操作与管理数据库**是由于我们需要将用户的数据高效地组织起来，以供后续查询与修改。这里的“数据库”是一个相对广泛的概念：对于简单的开发需求，**文件系统**也可以满足这个“数据库”的要求，用户的数据可以直接存储成文件的形式；但是，面对更大体量的数据，面对更快的查询与修改需求，各种各样的**数据库软件**是不可或缺的。不管采用哪种数据存储方式，都是以需求和用户为中心服务的。

**关系型数据库**是数据库的一种，一个数据库应用中可以创建若干个**数据库**，每个数据库又可以包含若干个**数据表**（可以类比 Excel 的工作簿、工作表进行理解）。每个数据表中，不同列代表不同的属性，每一行代表一条记录。事实上，我们可以将数据表与一个实体类联系起来。将每一列看做是这个实体类的一个具体的成员变量，每一行看成是这个类的一个实例。换句话说，我们可以将每张数据表看做是相同类的实体构成的集合。这种观点就是 **ORM 机制**（Object-relational mapping）出现的基础：我们可以用操作类和对象的代码来直接操作关系型数据库，而无需裸写 SQL 语句。当然，这样做会带来一定的性能损失，但极大地有利于程序员对代码本身的理解。



#### 后端的测试

软件开发与之前我们在课程中写代码最不同的一点就是要多做**软件测试**。在软件开发中，程序的正确性是至关重要的，于是需要专人（测试工程师）来撰写相应的测试代码，涉及到一般情况与尽可能多的 Corner Cases。一方面，这能帮助开发工程师有效开发，另一方面，在一个大型项目中可能会出现改动一部分代码导致另一部分代码的原有功能失效的情况，而通过固定的测试程序与测试用例则可以保证只有稳定的版本才会最终呈现给用户。

后端的单元测试往往有如下前提：

+ 测试工程师将开发工程师撰写的后端逻辑视为黑盒
+ 测试工程师可以直接模拟前端请求，读取与修改数据库中的内容
+ 测试工程师可以通过一系列断言验证程序的正确性

测试工程师就像是在设计 OJ 测例，断言后端系统在面对输入（用户请求）时，应该产生什么样的输出（对用户请求的响应、对数据库的修改）。若断言失败，则说明开发工程师提交的本次修改存在功能性问题，需要进行修复。

我们一般以测试覆盖率来定量地衡量后端测试的有效性与完整性，其中覆盖率的计算方式为测例覆盖到的代码行数与总代码行数之比。



#### 后端框架如何工作

一个成熟的后端框架往往具备以下解耦合的功能：

+ 路由：将前端请求的不同路径**映射**到不同的处理函数的方法
+ 模型：**与数据库进行交互**的方法，可以使用 ORM 机制撰写成面向对象风格
+ 视图：前端请求的**处理函数**，接受用户请求并返回响应
+ 单元测试：如何为测试工程师提供模拟请求、读写数据库、断言的操作

这里的“路由”、“模型”、“视图”都是 Django 中的概念，在其他的后端框架中它们不一定被如此称呼，但你总可以在学习其他后端框架时找到这些重要概念的影子。


### Django 速览


#### 文件树结构

在安装了 Django 库之后，我们可以使用 `django-admin startproject <项目名>` 来创建一个新项目。在新建**项目**后，我们进入项目文件夹，可以看到如下的文件树：

```
.
├── manage.py  # 使用命令行操作后端的主入口
└── <Project Name>
    ├── __init__.py  
    ├── settings.py  # 后端启动时应用的设置
    ├── urls.py  # 主路由入口
    ├── asgi.py  # 以 asgi 方式进行部署的配置文件
    └── wsgi.py  # 以 wsgi 方式进行部署的配置文件
```

项目部署的部分是小作业部署阶段（CI/CD 部分）的主要内容，这里我们不详细展开。

然后我们可以使用 `python3 manage.py startapp <应用名> ` 来新建一个**应用**。一个 Django 项目中可以同时存在多个应用，一个应用是具有完成某个独立功能作用的模块，这之后你应该看到：

```
.
├── app1  # 你创建的应用
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations  # 应用对数据库表及表属性的修改历史
│   │   └── __init__.py
│   ├── models.py  # 应用的“模型”定义
│   ├── tests.py  # 应用的“单元测试”定义
│   └── views.py  # 应用的“视图”定义
├── manage.py
└── <Project Name>
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

这时，你一般需要在 `<project>/settings.py` 中的 `INSTALLED_APPS` 字段中注册该应用。接下来，你应该能够理解下述目录结构：

```
.
├── DjangoHW  # 我们的项目名为 DjangoHW
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── README.md
├── board  # 我们新建了一个应用叫做 board
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   ├── 0001_initial.py
│   │   ├── 0002_remove_board_deleted_remove_user_deleted.py
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── db.sqlite3  # 本地数据库存储
├── manage.py
├── requirements.txt
└── utils  # 撰写的功能函数，可以放在应用中也可以放在根目录下，保证引用路径正确即可
    ├── utils_request.py
    ├── utils_require.py
    └── utils_time.py
```

!!! note 参考资料
	本节对应官方文档 “编写你的第一个 Django 应用，第 1 部分” 中“创建项目”、“用于开发的简易服务器”、“创建投票应用”节。



#### 路由（Routing）

首先，我们来解决后端收到请求时，后端会将请求交给哪个应用的哪个视图函数处理的问题。和这个功能有关的文件主要包括 `<项目名>/urls.py` 和 `<应用名>/urls.py`。

假如我们的后端部署在 `my-backend.com`，我们在访问 `my-backend.com/board/restart` 时，后端会首先在 `<项目名>/urls.py` 中以 `board/restart` 开始搜索。假设 `<项目名>/urls.py` 中配置为：

```python
from django.urls import path, include

urlpatterns = [
    path('board/', include("board.urls")),
]
```

我们会匹配掉字符串 `'board/'`，然后将剩下的请求 `restart` 交给 `board/urls.py` 处理，这也是这里 `include` 的作用，将请求转发给子应用的路由表处理。

然后，假设我们在 `board/urls.py` 中配置为：

```python
from django.urls import path, include
import board.views as views

urlpatterns = [
    path('restart', views.restart_board),
]
```

这时剩余请求 `restart` 匹配到第一条规则后，交由 `board/views.py` 中的 `restart_board` 函数进行处理，即后端会帮助我们调用这个函数，并把请求体（和请求有关的信息，包括请求方法、请求数据等等）作为参数传给这个函数。

此外还有更多和路由有关的功能，例如在路径中解析变量等，请阅读[官方文档](https://docs.djangoproject.com/zh-hans/4.1/topics/http/urls/)。

!!! question 思考题
	假如 `<project>/urls.py` 要把所有的请求都转发给 `api/urls.py`，`<project>/urls.py` 中 `path` 应如何填写？



#### 模型（Models）

!!! note 数据库使用的相关知识
	如果你对记录、主键、外键、索引、联合主键这些概念并不熟悉，你可以阅读 [这篇文档](https://zhuanlan.zhihu.com/p/64368422) 快速入门。在实际的开发过程中，这些元数据对于数据表的设计以及数据库使用起来的性能是至关重要的。

在 Django 中，模型用于数据库中数据表的结构设计以及数据表的元数据（如主键、外键、索引等）管理。我们使用 Django 提供的 ORM 机制来进行对数据表和数据表列属性的管理。具体来说，我们只需要在 `<app>/models.py` 中定义一个类继承 `django.db.models.Model` 即可，比如[官方文档](https://docs.djangoproject.com/zh-hans/4.1/intro/tutorial02/)中给出的定义：

```python
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField()

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

在你修改完应用的 `models.py` 之后，你应该使用如下命令去生成修改数据表结构与属性的语句：

```bash
python3 manage.py makemigrations <app_name>
```

注意请不要将 migrations 文件夹纳入到 .gitignore 文件中。进而，每次在服务端部署时，在其运行之前，请确保你的部署脚本会执行：

```bash
python3 manage.py migrate
```

将上条命令生成的修改表属性的语句应用到该部署所对应的数据库中。

由于我们只是进行本地测试，所以你可以在本地连续地输入这两条指令，本地的数据库会存储在 `db.sqlite3` 文件中。 

!!! question 思考题
	请查阅文档，主键、外键、联合主键、唯一性约束、索引这些元数据都应该如何创建？

!!! note 参考资料
	本节对应官方文档 “编写你的第一个 Django 应用，第 2 部分” 中“数据库配置”、“创建模型”、“激活模型”节。



#### 视图（Views）

我们接下来介绍视图函数。视图函数是后端逻辑的主入口，其接受经过路由之后的 [`HttpRequest`](https://docs.djangoproject.com/en/4.1/ref/request-response/#django.http.HttpRequest) 类型的请求作为参数，并返回一个 [`HttpResponse`](https://docs.djangoproject.com/zh-hans/4.1/ref/request-response/#django.http.HttpResponse) 类型的对象作为响应。你可以在上述链接中查找这两个类分别有哪些成员变量可以供你使用。

我们可以在 `<app>/views.py` 中定义一个应用所具有的视图函数。我们在这里举一个留言板应用“获取与创建留言”的视图函数作为例子：

```python
def message(request):  # 这里 request 是 HttpRequest 类型的对象
    # 功能函数，快速创建具有特定状态码的响应
    def gen_response(code: int, data: str):
        return JsonResponse({
            'code': code,
            'data': data
        }, status=code)  # JsonResponse 是 HttpResponse 的子类
        				 # 可以传入一个 dict 转换成 JSON 响应

    if request.method == 'GET':
        limit = request.GET.get('limit', default='100')
        offset = request.GET.get('offset', default='0')
        if not limit.isdigit():
            return gen_response(400, f'{limit} is not a number')
        if not offset.isdigit():
            return gen_response(400, f'{offset} is not a number')

        return gen_response(200, [
                {
                    'title': msg.title,
                    'content': msg.content,
                    'user': msg.user.name,
                    'timestamp': int(msg.pub_date.timestamp())
                }
                for msg in Message.objects.all()\
            				.order_by('-pub_date')\
            				[int(offset):int(offset)+int(limit)]
            ])

    elif request.method == 'POST':
        # 从 cookie 中获得 user 的名字，如果 user 不存在则新建一个
        # 如果 cookie 中没有 user 则使用 "Unknown" 作为默认用户名
        name = request.COOKIES['user']\
        		if 'user' in request.COOKIES else 'Unknown'
        user = User.objects.filter(name=name).first()
        if not user:
            user = User(name = name)
            try:
                user.full_clean()
                user.save()
            except ValidationError as e:
                return gen_response(400, 
                                    f"Validation Error of user: {e}")


        # 验证请求的数据格式是否符合 json 规范，如果不符合则返回 400
        try:
            data = json.loads(request.body.decode("utf-8"))
        except:
            return gen_response(400, 
                            "Exception occurred in request body parsing.")

        # 验证请求数据是否满足接口要求，若通过所有的验证，则将新的消息添加到数据库中
        # PS: {"title": "something", "content": "someting"} 
        # 这里 title 和 content 均有最大长度限制
        try:
            title = data['title']
            content = data['content']
            obj = Message(user=user, title=title, content=content)
            obj.full_clean()
            obj.save()
        except:
            return gen_response(400, 
                                "Requested data failed verification.")

        # 添加成功返回 code 201
        return gen_response(201, 
                            "Message received successfully")

    else:
        return gen_response(405, 
                            f'Method {request.method} not allowed')
```

这是个经典的视图函数，面对 GET 方法返回数据库中的相应信息，面对 POST / PUT / DELETE 方法在**做检查**之后去修改对应的数据库内容，然后返回一个 `JsonResponse` 对象说明操作的结果，以 HTTP 状态码来区分操作的状态。

!!! note 参考资料
	本节对应官方文档 “编写你的第一个 Django 应用，第 1 部分” 中“编写第一个视图”节，“编写你的第一个 Django 应用，第 3 部分”中“编写更多视图”、“写一个真正有用的视图”、“抛出 404 错误”节。



#### 单元测试（Unit Tests）

接下来我们介绍单元测试。在课程中我们学过，对模块进行测试，相比对模块拼接起来的系统直接测试所付出的代价要小得多。在真正的软件开发过程中，单元测试环节就是要对我们所开发的模块进行自动化的测试。在 Django 中，测试工程师会将开发工程师所编写的路由与视图视为黑盒，通过 `django.test.TestCase` 类与 `django.test.Client` 类来模拟前端与开发工程师所撰写的后端交互，并通过其提供的断言函数来断言响应所应该具有的属性或是数据库应被如何修改。以上述的留言板应用的视图函数为例，我们可以撰写如下测试：

```python
from django.test import TestCase, Client
from .models import Message, User  # Defined in models.py

class MessageModelTests(TestCase):
    def setUp(self):  # Preparation
        alice = User.objects.create(name="Alice")
        bob = User.objects.create(name="Bob")
        Message.objects.create(user=alice, 
                               title="Hi", 
                               content="Hello World!")
        Message.objects.create(user=bob, 
                               title="This is a title", 
                               content="This is my content")

        
    # 测试 POST 方法
    def test_add_new_message(self):
        # 模拟前端请求
        title, content = "Title", "Message"
        user = "student"
        payload = {
            'title': title,
            'content': content,
        }
        self.client.cookies['user'] = user

        response = self.client.post('/api/message', 
                                data=payload,
                                content_type="application/json")
        
        # 断言响应的属性
        self.assertJSONEqual(response.content, 
                             {
                                 'code': 201, 
                                 'data': "Message received successfully"}
                            )
        # 断言数据库的属性
        self.assertTrue(User.objects.filter(name=user).exists())
        self.assertTrue(Message.objects.filter(
            title=title, content=content).exists())
    
    
    # 测试 GET 方法
    def test_message_can_be_fetched(self):  
        offset, limit = 0, 100  
        response_data = [
                {
                    'title': msg.title,
                    'content': msg.content,
                    'user': msg.user.name,
                    'timestamp': int(msg.pub_date.timestamp())
                }
                for msg in Message.objects.all()\
            				.order_by('-pub_date')\
            				[int(offset):int(offset)+int(limit)]
            ]
        response = self.client.get("/api/message")
        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.json()['data'], response_data)
     
    
	# 测试 Corner Case（如不存在 Title 字段）
    def test_add_new_message_title_not_exists(self):
        content = "Message"
        user = "student"
        payload = {
            'content': content,
        }
        self.client.cookies['user'] = user

        response = self.client.post('/api/message', 
                                data=payload,
                                content_type="application/json")
        
        self.assertEqual(response.status_code, 400)
```

!!! note 参考资料
	本节对应官方文档 “编写你的第一个 Django 应用，第 5 部分” 中的所有节。


#### 模板（Template）

在 程序设计训练 Python 小学期中会用到，但因为是“服务端渲染”的范式，在这里不做详细介绍。

有需求的同学请查阅官方文档 :)


### 参考资料

- [《软件工程》课程小作业讲稿与文档](https://thuse-course.github.io/course-index/)
- [Django 官方文档](https://docs.djangoproject.com/en/4.2/)



## 课程作业

课程作业正在与前端 React 课程联合筹备中，预期将与 React 作业一同发布 :)

