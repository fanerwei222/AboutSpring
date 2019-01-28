
### 1.AOP (Aspect Oriented Programming) 面向切面编程

### 2.切面： 编程中，对象与对象之间，方法与方法之间，模块与模块之间都是一个个切面
            用刀把一个西瓜分成两瓣，切开的切口就是切面；炒菜，锅与炉子共同来完成炒菜，锅与炉子就是切面。
            web层级设计中，web层->网关层->服务层->数据层，每一层之间也是一个切面。
            
### 3.术语： 
            a.join point(连接点)--> 程序中一些特定的时间点，例如一个方法的执行、一个异常的处理。
                                    SpringAOP中总是方法的执行点，即SpringAOP中只有方法连接点。
            b.point cut(切点)-----> 一组限定join point(连接点)的规则。
                                    例如：join point是一个除法函数，那么point cut就必须有除数不能为0这一条规则。
            c.advice(增强)--------> 由 aspect 添加到特定的 join point(即满足 point cut 规则的 join point) 的一段代码.
                                    许多 AOP框架, 包括 Spring AOP, 会将 advice 模拟为一个拦截器(interceptor), 
                                    并且在 join point 上维护多个 advice, 进行层层拦截。
                                    例如：在获取用户信息方法之前执行登录对象是否合法，是否有权限访问该用户登录方法，没有权限则抛出异常。
            
            d.target(目标对象)----> 织入 advice 的目标对象. 目标对象也被称为 advised object.
                                    因为 Spring AOP 使用运行时代理的方式来实现 aspect, 因此 adviced object 总是一个代理对象(proxied object)
                                    注意, adviced object 指的不是原来的类, 而是织入 advice 后所产生的代理类.
                                    
            e.Aspect(切面)--------> 由advice 和 point cut 组成，主要作用是如何将advice(增强)织入target(目标对象)的join point(连接点)上：
                                    1.如何通过advice和point cut定位到特定的join point上；
                                    2.如何在advice中编写切面代码。
            

