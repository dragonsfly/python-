# python-面试题


Python面试题目
一、Python
1. python的多进程与多线程的运行机制是什么？有什么区别？分别在什么情况下用？
2. Python的装饰器的原理是什么，在什么情况会用到装饰器。请手写Python装饰器代码
3. 如何提高Python的运行效率，请说出不少于2种提高运行效率的方法。
4. 介绍下“消费者”和“生产者”模型。


二、HTTP/HTTPS，TCP/IP协议
1. 关于HTTP/HTTPS的区别，分别应该在什么场合下。
2. HTTPS有什么优点和缺点
3. HTTPS是如何实现安全传输数据的。
4. HTTPS安全证书是怎么来的，如何申请，国内和国外有哪些第三方机构提供安全证书认证。
5. get和post请求有什么区别，分别应该在什么场合下。
6. TCP三次握手、四次挥手，请说出每次发送的状态码。
7. HTTP请求会有哪些信息发送到后台服务器。
8.tcp和udp
  TCP/UDP对比:https://blog.csdn.net/air_hjj/article/details/70791852 
TCP的优点：可靠，稳定 三次握手,确认机制、重传机制、拥塞控制机制
	 缺点: 慢，效率低，占用系统资源高，易被攻击
	 应用:HTTP、HTTPS、FTP等传输文件的协议，POP、SMTP等邮件传输的协议 
UDP的优点:快
	 缺点:不可靠，不稳定
	 应用: 当对网络通讯质量要求不高的时候，要求网络通讯速度能尽量的快, QQ语音,QQ视频,TFTP
udp 网络程序-发送数据
	1. 创建客户端套接字(socket)
	2. 发送/接收数据
	3. 关闭套接字


三、数据库
0. MySQL的常用引擎有哪些？有什么区别？
1. redis是什么类型数据库，可以存哪些数据结构的数据。
2. redis有多少个库？
3. redis、MongoDB有什么区别，分别应用在什么情况下。
4. MongoDB是以什么数据结构存入的。
5. 如何优化MySql数据库


四、scrapy和scrapy-redis
1. 描述下scrapy框架运行的机制？
答：从start_urls里获取第一批url并发送请求，请求由引擎交给调度器入请求队列，获取完毕后，调度器将请求队列里的请求交给下载器去获取请求对应的响应资源，并将响应交给自己编写的解析方法做提取处理：1. 如果提取出需要的数据，则交给管道文件处理；2. 如果提取出url，则继续执行之前的步骤（发送url请求，并由引擎将请求交给调度器入队列...)，直到请求队列里没有请求，程序结束。


2. scrapy和scrapy-redis有什么区别？为什么选择redis数据库？
答：
1) scrapy是一个Python爬虫框架，爬取效率极高，具有高度定制性，但是不支持分布式。而scrapy-redis一套基于redis数据库、运行在scrapy框架之上的组件，可以让scrapy支持分布式策略，Slaver端共享Master端redis数据库里的item队列、请求队列和请求指纹集合。
2) 为什么选择redis数据库，因为redis支持主从同步，而且数据都是缓存在内存中的，所以基于redis的分布式爬虫，对请求和数据的高频读取效率非常高。


3. 反爬虫的机制有哪些？
答：
1) User—Agent
2) 代理ip
3) 访问频率限制
4) 验证码处理
5) Cookie
6) 动态HTML数据加载


4. 实现模拟登录的方式有哪些？
答：
1) 使用一个具有登录状态的cookie，结合请求报头一起发送，可以直接发送get请求，访问登录后才能访问的页面。
2) 先发送登录界面的get请求，在登录页面HTML里获取登录需要的数据（如果需要的话），然后结合账户密码，再发送post请求，即可登录成功。然后根据获取的cookie信息，继续访问之后的页面。


5. get和post请求有什么区别？分别应该在什么场合下。
答：
1) get请求用于直接获取指定url的响应数据，和服务器没有交互信息。
2) post请求在获取响应数据前，会先发送form表单，服务器会根据form表单来返回响应数据。


6. Selenium、PhantomJS是什么？可以为爬虫做哪些事情？
答：
1) Selenium是一种自动测试化工具，可以导入使用指定的浏览器，在发送请求获取响应后，响应数据则会在指定的浏览器里执行完毕。而PhantomJS是一种无界面浏览器，相比传统的Chrome或Firefox浏览器等，资源消耗会更少。
2) 在Python爬虫代码里使用Selenium和PhantomJS组合，相当于真实浏览器的执行状态，可以直接获取动态HTML数据（如JavaScript、Ajax加载的数据等），并且支持模拟键盘事件、鼠标点击事件、执行JavaScript语句等。在一些反爬虫极端情况下，Selenium+PhantomJS可以作为终极解决方案。


7、简单介绍下scrapy的异步处理。
答：scrapy框架的异步机制是基于twisted异步网络框架处理的，在settings.py文件里可以设置具体的并发量数值（默认是并发量16）。


基础概念理解:
0. 进程间通信-Queue队列
    	创建 
    		q = multiprocessing.Queue() 参数表示队列长度 -- 数据条数
    	往里面放数据
    		q.put(data)
    	取出数据
    		q.get()
    	判断满
    		q.full()
    	判断空
    		q.empty()
    	获取队列中的数据数量 mac会崩溃
    		q.qsize()

    	put(obj[, block[, timeout]])
    		obj表示数据对象
    		block表示是否阻塞等待 True表示阻塞等待 False表示不阻塞 不等待
    		timeout 表示如果等待  等待最长的时间 

            如果超时等待或者 不阻塞等待都没有获取到数据 则抛出异常

        put(data,block=True,timeout=-1)

            put(data,True,10)
            put(data,False) 不等待 put_nowait(data)
                如果超时放入 或者 非阻塞放入数据 没有完成任务 都会抛出异常

        get(block=True, timeout=-1])
            block表示是否阻塞等待 True表示阻塞等待 False表示不阻塞 不等待
            timeout 表示如果等待  等待最长的时间  -1表示死等

            get() == get(True)
            get(True,10) 最多超时等待10s 如果没有取到数据 就抛出异常
            get(False) 不阻塞等待  直接获取数据 如果没有取到数据 就抛出异常


1. 进程池
        
        创建进程池 pool = Pool(进程的最大数量)
        添加任务   
            apply是阻塞的任务添加方式  会等待添加的任务执行完成才会继续往下执行
            apply_async 是非阻塞的任务添加方式  只管添加  不等任务结束

        关闭进程池
            .close()
            pool.terminate()  终止进程池中所有的正在执行的进程任务  

        等待所有任务执行完成 
            .join()       保持主进程存活 等待所有的工作进程 全部退出

    注意事项:
        1. 如果需要在进程池中 使用进程间通信Queue 不要使用multiprocessing.Queue() (要求是通过继承的方式创建的进程)
        应该使用 multiprocessing.Manager().Queue()

        2. .join()之前 一定要调用 .close() 或者.terminate()
        3. 在正常情况下 是不需要teminate()终止所有工作进程的
	
迭代器生成器语法
	1. 迭代
    根据记录的前面的元素的位置信息 去访问后续的元素的过程 -遍历 迭代


2. 可迭代对象 iterable

    能够被迭代访问的对象 for in 
    常用可迭代对象-list tuple str
    from collections import Iterable
    isinstance(obj, Iterable)

3. 可迭代对象
    
    可迭代对象通过__iter__方法提供一个 可以遍历对象中数据的工具-迭代器
        iter(可迭代对象) 可以获取可迭代对象的迭代器

    通过迭代器可以迭代访问 数据
        next(迭代器)  =====  迭代器对象.__next__()

        如果需要实现一个迭代器 就需要实现__next__()   

4. 迭代器 iterator -- 迭代器访问可迭代对象中数据
    判断对象是否是迭代器类型

    from collections import Iterator
    isinstance(obj, Iterator)

    自己实现
        迭代器本身也是可迭代对象  __iter__()  提供迭代器(self)
        下一个元素的值 = next(迭代器)  =====>  __next__()

5. 生成器 generator
    生成器是一种特殊的迭代器  --- 是迭代器 并且有自己的特点
    1 创建生成器表达式  [] ----》 （x for x in range(100)）
    2 生成器函数
        凡是有yield关键字的函数都不是普通函数了 而是生成器函数



6. yield关键字的作用

        挂起当前函数  将后面表达式的值 返回到调用生成器的地方
        接收数据 并唤醒当前函数  并且紧接着上次运行的地址继续执行

7. 唤醒生成器的两种方式

        生成器.send("数据") 
        next(生成器) === 生成器.send(None)

        在第一次调用生成器对象的是 必须使用next()
            在后续的情况下 send和next可以混用 
