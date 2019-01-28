
### 1.AOP (Aspect Oriented Programming) 面向切面编程

### 2.切面： 编程中，对象与对象之间，方法与方法之间，模块与模块之间都是一个个切面
            用刀把一个西瓜分成两瓣，切开的切口就是切面；炒菜，锅与炉子共同来完成炒菜，锅与炉子就是切面。
            web层级设计中，web层->网关层->服务层->数据层，每一层之间也是一个切面。
            
### 3.术语： 
            a. join point(连接点)--> 程序中一些特定的时间点，例如一个方法的执行、一个异常的处理。
                                    SpringAOP中总是方法的执行点，即SpringAOP中只有方法连接点。
            b. point cut(切点)-----> 一组限定join point(连接点)的规则。
                                    例如：join point是一个除法函数，那么point cut就必须有除数不能为0这一条规则。
            c. advice(增强)--------> 由 aspect 添加到特定的 join point(即满足 point cut 规则的 join point) 的一段代码.
                                    许多 AOP框架, 包括 Spring AOP, 会将 advice 模拟为一个拦截器(interceptor), 
                                    并且在 join point 上维护多个 advice, 进行层层拦截。
                                    例如：在获取用户信息方法之前执行登录对象是否合法，是否有权限访问该用户登录方法，没有权限则抛出异常。
            
            d. target(目标对象)----> 织入 advice 的目标对象. 目标对象也被称为 advised object.
                                    因为 Spring AOP 使用运行时代理的方式来实现 aspect, 因此 adviced object 总是一个代理对象(proxied object)
                                    注意, adviced object 指的不是原来的类, 而是织入 advice 后所产生的代理类.
                                    
            e. Aspect(切面)--------> 由advice 和 point cut 组成，主要作用是如何将advice(增强)织入target(目标对象)的join point(连接点)上：
                                    1.如何通过advice和point cut定位到特定的join point上；
                                    2.如何在advice中编写切面代码。
                                    
            f. AOP proxy ----------> 一个类被 AOP 织入 advice, 就会产生一个结果类, 它是融合了原类和增强逻辑的代理类.
                                     在 Spring AOP 中, 一个 AOP 代理是一个 JDK 动态代理对象或 CGLIB 代理对象.
                                     Spring AOP 默认使用标准的 JDK 动态代理(dynamic proxy)技术来实现 AOP 代理, 通过它, 
                                     我们可以为任意的接口实现代理.如果需要为一个类实现代理, 那么可以使用 CGLIB 代理. 
                                     当一个业务逻辑对象没有实现接口时,
                                     那么Spring AOP 就默认使用 CGLIB 来作为 AOP 代理了. 
                                     即如果我们需要为一个方法织入 advice, 但是这个方法不是一个接口所提供的方法, 
                                     则此时 Spring AOP 会使用 CGLIB 来实现动态代理. 
                                     鉴于此, Spring AOP 建议基于接口编程, 对接口进行 AOP 而不是类
            
            g. Weaving(织入)-------->将 aspect 和其他对象连接起来, 并创建 adviced object 的过程.
                                    根据不同的实现技术, AOP织入有三种方式:
                                                1. 编译器织入, 这要求有特殊的Java编译器.
                                                2. 类装载期织入, 这需要有特殊的类装载器.
                                                3. 动态代理织入, 在运行期为目标类添加增强(Advice)生成子类的方式.
                                                   Spring 采用动态代理织入, 而AspectJ采用编译器织入和类装载期织入.
                                                   
            h. advice 的类型-------->before advice, 在 join point 前被执行的 advice. 虽然 before advice 是在 join point 前被执行, 
                                    但是它并不能够阻止 join point 的执行, 除非发生了异常(即我们在 before advice 代码中, 
                                    不能人为地决定是否继续执行 join point 中的代码)
                                                1. after return advice, 在一个 join point 正常返回后执行的 advice
                                                2. after throwing advice, 当一个 join point 抛出异常后执行的 advice
                                                3. after(final) advice, 无论一个 join point 是正常退出还是发生了异常, 都会被执行的 advice.
                                                4. around advice, 在 join point 前和 joint point 退出后都执行的 advice. 
                                                   这个是最常用的 advice.
            

