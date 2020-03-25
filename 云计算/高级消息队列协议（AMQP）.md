## 高级消息队列协议（AMQP）

### 消息队列

消息队列（Message Queue）是一种进程间通信或同一进程的不同线程间的通信方式。消息的发送者和接收者不需要同时与消息队列交互。消息会保存在队列中，直到接收者取回它。

消息队列是分布式系统中重要的组件。

### 场景及作用

- 解耦：通过消息队列中间件的引入，降低各模块之间的复杂度，达到解耦的目的。
- 异步：消息队列投递，通过消息队列的引入，有更加灵活的处理方式（主动拉取，服务推送），并且可以堆叠消费者进行并行处理消息。
- 限流：同一时间大规模的消息生成，通过消息中间件进行负载均衡，达到限流的目的。

### 高级消息队列

高级消息队列协议（AMQP）是一个异步消息传递所使用的应用层协议规范，是应用层协议的一个开放标准，为面向消息的中间件设计。作为线路层协议，AMQP客户端能够无视消息的来源任意发送和接收消息。基于此协议的客户端与消息中间件可传递消息，并不受客户端/中间件不同产品，不同的开发语言。AMQP模型统一了消息模式，包括发布/订阅，队列，事务以及流数据，并且添加了额外的特性，例如更易于扩展，基于内容的路由等。

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/16c47c799e73e1bf.png)

**Publisher application**：生产者应用生产的信息放到Server端

**Server**：指RabbitMQ节点

**Virtual host**：虚拟主机，类似路由器

**Exchange**：交换机，生产者直接将消息投递到Exchange中，经历三个过程：Server -> Virtual host -> Exchange

> 先确定将消息发送到哪台服务器，那么就需要先去建立连接，设置一些地址等等。 第二层，投递到哪个Virtual host需要定义。 第三层，投递到哪个Exchange也需要定义。
>
> 再看Consumer application消费者的应用端，消费端只需要监听Message Queue，当队列中有消息的时候，就拿出来消费。因此在Exchange和Message Queue之间有绑定的关系存在。

### 为什么使用AMQP

通过AMQP，让消息中间件的能力最终被网络本身所具有，并且通过消息中间件的广泛使用发展出一系列有用的应用程序，实现一种在全行业广泛使用的标准消息中间件技术，以降低企业和系统集成的开销，并且向大众提供工业级的集成服务。

### AMQP的核心概念

- Server：又称Broker，接收客户端的连接，实现AMQP实体服务
- Connection：连接，应用程序与Broker的网络连接
- Channel：网络信道，几乎所有的操作（数据读写）都在Channel中进行，Channel是进行消息读写的通道。客户端可建立多个Channel，每个Channel代表一个会话任务。
- Message：消息，服务器和应用程序之间传送的数据，由Properties和Body组成。Properties可以对消息进行修饰，比如消息的优先级、延迟等高级特性；Body则是消息体内容。
- Virtual host：虚拟地址，用于进行逻辑隔离，最上层的消息路由。一个Virtual host里面可以有若干个Exchange和Queue，但同一个Virtual host里面不能有相同名称的Exchange和Queue。用来划分具体的服务。
- Exchange：交换机，接收消息，根据路由键转发消息到绑定的队列。
- Binding：Exchange和Queue之间的虚拟连接，Binding中可以包含Routing key。
- Routing key：一个路由规则，虚拟机可用它来确定如何路由一个特定消息。
- Queue：消息队列，保存信息并将它们转发给消费者。

### 主流产品

- ActiveMQ
- RabbitMQ                               

### RabbitMQ

#### 架构模型

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/16c47c799ef7013e.png)

> 生产者把消息投递到Exchange,Exchange投递到Queue. 因此我们的生产者只需要关注把消息投递到指定的Exchange即可,我们的消费者只需要监听指定Queue即可。就是这么简单的机制。 通过上图我们也能看到，生产者不需要关注投递到哪个队列，消费也不需要关注是从哪个Exchange上来的，这两块没有耦合的情况。主要是应为Exchange和Queue有一个绑定的关系。

#### 消息如何流转

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/16c47c799f0f321e.png)

> 生产者publisher application 生产消息Message投递到Exchange上，Exchange绑定MessageQueue，可以绑定过多个MessageQueue，为什么三个队列只有其中一个队列收到了消息呢？主要是由于Exchange是有一个路由功能的。这个路由就是routing key,这个路由有两个非常关键的点， 第一个：你的消息是需要发送到哪个Exchange。 第二个：你发消息的时候需要带上routing key，然后通过Exchange 和 MessageQueue 建立一个绑定关系，通过路由key把消息路由到一个指定的队列上。然后我们的消费端直接监听队列就行了，就可以消费了。