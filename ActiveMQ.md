

##  JMS两种消息模式

### 点对点的消息模式

点对点的模式主要建立在一个队列上面，当连接一个列队的时候，发送端不需要知道接收端是否正在接收，可以直接向ActiveMQ发送消息，发送的消息，将会先进入队列中，如果有接收端在监听，则会发向接收端，如果没有接收端接收，则会保存在activemq服务器，直到接收端接收消息，点对点的消息模式可以有多个发送端，多个接收端，但是一条消息，只会被一个接收端给接收到，哪个接收端先连上ActiveMQ，则会先接收到

### 订阅模式

订阅/发布模式，同样可以有着多个发送端与多个接收端，但是接收端与发送端存在时间上的依赖，就是如果发送端发送消息的时候，接收端并没有监听消息，那么ActiveMQ将不会保存消息，将会认为消息已经发送，换一种说法，就是发送端发送消息的时候，接收端不在线，是接收不到消息的，哪怕以后监听消息，同样也是接收不到的。这个模式还有一个特点，那就是，发送端发送的消息，将会被所有的接收端给接收到，不类似点对点，一条消息只会被一个接收端给接收到。

## 实现代码

```xml
 <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.12.0</version>
        </dependency>

        <dependency>
            <groupId>org.apache.activemq</groupId>
            <artifactId>activemq-all</artifactId>
            <version>5.15.9</version>
        </dependency>
        <dependency>
            <groupId>org.apache.xbean</groupId>
            <artifactId>xbean-spring</artifactId>
            <version>3.16</version>
        </dependency>
```



### 发布订阅模式

发送端

```java
public class ActivePro_Topic {
    public static void main(String[] args) throws JMSException {
        //建立工厂
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        //工厂建立连接
        Connection connection = factory.createConnection();
        connection.start();
        //连接建立对话
        Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        //建立目的地
        Topic t1 = session.createTopic("t1");
        MessageProducer producer = session.createProducer(t1);

        for (int i = 0; i < 3; i++) {
            TextMessage textMessage = session.createTextMessage("nihaoa"+i);
            producer.send(textMessage);
        }
    }
}
```



```java
public class ActiveCon_Topic {
    public static void main(String[] args) throws JMSException, IOException {
        //建立工厂
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        //工厂建立连接
        Connection connection = factory.createConnection();
        connection.start();
        //连接建立对话
        Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        //会话建立目的地
        Topic t1 = session.createTopic("t1");
        MessageConsumer consumer = session.createConsumer(t1);
        //第一种:一直等待    
        //receive(Long long):超时不候
//        while (true) {
//            TextMessage receive =(TextMessage) consumer.receive();
//            if (receive!=null){
//                System.out.println(receive);
//            }else {
//                break;
//            }
//        }
        //第二种:监听事件
        consumer.setMessageListener(new MessageListener() {
            @Override
            public void onMessage(Message message) {
                if (message != null &&  message instanceof  TextMessage) {
                    TextMessage message1= (TextMessage) message;
                    try {
                        System.out.println("----"+message1.getText());

                    } catch (JMSException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        System.in.read();
    }
}


```



### 点对点模式



```java
public class ActiveProduce {
    public static void main(String[] args) throws JMSException {
        //建立工厂
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        //工厂建立连接
        Connection connection = factory.createConnection();
        connection.start();
        //连接建立对话
        Session session = connection.createSession(false,Session.AUTO_ACKNOWLEDGE);
        //建立目的地
        Queue queue1 = session.createQueue("queue1");
        //会话建立生产者
        MessageProducer producer = session.createProducer(queue1);
        for (int i = 0; i < 3; i++) {
            TextMessage textMessage = session.createTextMessage("nihao" + i);
            producer.send(textMessage);
        }
        producer.close();
        session.close();
        connection.close();
        System.out.println("=============");
    }
}

```





```java
public class ActiveConsume {
    public static void main(String[] args) throws JMSException {
        //建立工厂
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        //工厂建立连接
        Connection connection = factory.createConnection();
        connection.start();
        //连接建立对话
        Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        //建立目的地
        Queue queue12 = session.createQueue("queue1");
        MessageConsumer consumer = session.createConsumer(queue12);
        //第一种:一直等待后者/超时不候
//        while (true) {
//            TextMessage receive =(TextMessage) consumer.receive();
//            if (receive!=null){
//                System.out.println(receive);
//            }else {
//                break;
//            }
//        }
        //第二种:监听事件
        consumer.setMessageListener(new MessageListener() {
            @Override
            public void onMessage(Message message) {
                if (message != null &&  message instanceof  TextMessage) {
                    TextMessage message1= (TextMessage) message;
                    try {
                        System.out.println("----"+message1.getText());

                    } catch (JMSException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
    }
}

```



## 数据支持类型

```java
 		   //纯字符串的数据
            session.createTextMessage();
            //序列化的对象
            session.createObjectMessage();
            //流，可以用来传递文件等
            session.createStreamMessage();
            //用来传递字节
            session.createBytesMessage();//发送文件
            //这个方法创建出来的就是一个map，可以把它当作map来用，当你看了它的一些方法，你就懂了
            session.createMapMessage();
            //这个方法，拿到的是javax.jms.Message，是所有message的接口
            session.createMessage();
```

```java
传递一个java对象，可能是最多的使用方式了，而且这种数据接收与使用都方便，那么，下面的代码就来演示下如何发送一个java对象

当然了，这个对象必须序列化，也就是实现Serializable接口
            //通过这个方法，可以把一个对象发送出去，当然，这个对象需要序列化，因为一切在网络在传输的，都是字节
            ObjectMessage obj = session.createObjectMessage();
            for(int i = 0 ; i < 100 ; i ++){
                Person p = new Person(i,"名字");
                obj.setObject(p);
                producer.send(obj);
            }
  -----------------------------------
            //实现一个消息的监听器
            //实现这个监听器后，以后只要有消息，就会通过这个监听器接收到
            consumer.setMessageListener(new MessageListener() {
                @Override
                public void onMessage(Message message) {
                    try {
                        //同样的，强转为ObjectMessage，然后拿到对象，强转为Person
                        Person p = (Person) ((ObjectMessage)message).getObject();
                        System.out.println(p);
                    } catch (JMSException e) {
                        e.printStackTrace();
                    }
                    
                }
            });
```



![image-20210117195428714](F:\文档\JAVA笔记\Typora\image-20210117195428714.png)

## JMS组成结构

1. JMS provider : 服务提供者 一般就指的是MQ服务器
2. JMS producer :服务生产者 负责将消息发送给服务器
3. JMS consumer :服务消费者 处理服务器上的消息
4. JMS Message :
   - 消息头: 
     - JMSDestination  : 消息发往的目的地  Queue 还是Topic
     - JMSDeliveryMode  : 消息是否持久化  持久模式和非持久模式。一条持久性的消息：应该被传送“一次仅仅一  次”，这就意味着如果JMS提供者出现故障，该消息并不会丢失，它会在服务器恢复之后再次传递。一条非持久的消息：最多会传递一次，这意味着服务器出现故障，该消息将会永远丢失。
     - JMSExpiration  : 消息过期时间 
     - JMSPriority : 消息紧急处理策略 默认4 ,大于5为加急
     - JMSMessageID : 消息ID
   - 消息属性
     - 封装具体的消息数据
     - ==发送和接收的消息体类型必须一致对应== (需要强转)
   - 消息体
     -    如果需要除消息字段以外的值，那么可以使用消息属性 setxxxproperty





## 保证消息处理成功

###  签收模式

```java
 //连接建立对话
        Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
//在建立连接对话时,可以选择CLIENT_ACKNOWLEDGE模式,必须接收端手动签收,否则消息不会消失
		Session session = connection.createSession(false, CLIENT_ACKNOWLEDG);
//这时.接收端就必须通过  message.acknowledge()  方法来确认签收
```

**注意：只在点对点中有效，订阅模式，即使不确认，也不会保存消息**

### 持久化

```java
messageProducer.setDeliveryMode(DeliveryMode.NON_PERSISTENT)//非持久化 
messageProducer.setDeliveryMode(DeliveryMode.PERSISTENT)//持久化
```

持久化代码:

==Queue 默认的持久化,这里使用Map Message==



```java
public class Pro_persistent {
    public static void main(String[] args) throws JMSException {
        ActiveMQConnectionFactory fa = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        Connection connection = fa.createConnection();
        Session session = connection.createSession(false,Session.AUTO_ACKNOWLEDGE);
        Topic xgw = session.createTopic("xgw");
        MessageProducer producer = session.createProducer(xgw);
        producer.setDeliveryMode(DeliveryMode.PERSISTENT);
        connection.start();

        for (int i = 0; i < 3; i++) {
            MapMessage mapMessage = session.createMapMessage();
            mapMessage.setString("k1","李文静小肥猪");
            producer.send(mapMessage);
        }
        session.close();
        producer.close();
        connection.close();
    }
}

```



```java
public class Con_persistent {
    public static void main(String[] args) throws JMSException {
        ActiveMQConnectionFactory activeMQConnectionFactory = new ActiveMQConnectionFactory("tcp://81.70.168.186:61616");
        Connection connection = activeMQConnectionFactory.createConnection();
        connection.setClientID("lwj");
        Session session = connection.createSession(false, DeliveryMode.PERSISTENT);
        Topic xgw = session.createTopic("xgw");
        TopicSubscriber nihaoa = session.createDurableSubscriber(xgw, "nihaoa");
        connection.start();
        Message receive = nihaoa.receive();
        while (null != receive) {
            MapMessage mapMessage = (MapMessage) receive;
            String k1 = mapMessage.getString("k1");
            System.out.println(k1);
            receive = nihaoa.receive();
        }
        session.close();
        nihaoa.close();
        connection.close();

    }
}

```



非持久订阅只有当客户端处于激活状态，也就是和MQ保持连接状态才能收发到某个主题的消息。如果消费者处于离线状态，生产者发送的主题消息将会丢失作废，消费者永远不会收到。一句话：先订阅注册才能接受到发布，只给订阅者发布消息。

客户端首先向MQ注册一个自己的身份ID识别号，当这个客户端处于离线时，生产者会为这个ID保存所有发送到主题的消息，当客户再次连接到MQ的时候，会根据消费者的ID得到所有当自己处于离线时发送到主题的消息当持久订阅状态下，不能恢复或重新派送一个未签收的消息。持久订阅才能恢复或重新派送一个未签收的消息。

### 事务

```java
Session session = connection.createSession(true, Session.AUTO_ACKNOWLEDGE);
```

==在开启事务后,签收功能不起作用==

## SpringBoot整合AvtiveMQ

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-activemq</artifactId>
        </dependency>
        <!--消息队列连接池-->
        <dependency>
            <groupId>org.apache.activemq</groupId>
            <artifactId>activemq-pool</artifactId>
            <version>5.15.14</version>
        </dependency>
```

```java
@Configuration
@EnableJms  //开启消息支持 
public class ActiveMQConfig {
    @Value("${myqueue}") //将yml文件中的属性赋值给队列/主题名
    private String name;
    @Bean
    public ActiveMQQueue activeMQQueue(){
        return new ActiveMQQueue(name); //向容器中注册一个队列
    }
    @Bean
    public ActiveMQTopic activeMQTopic(){ //向容器中注册一个主题
        return new ActiveMQTopic(name);
    }
}

```

生产者

```java
@Component
public class pro {
    @Autowired
    private ActiveMQQueue activeMQQueue;
    @Autowired
    private JmsMessagingTemplate template;
    @Scheduled(fixedDelay = 3000)//定时投放  还需要在主启动类上加注解
    public void sendto(){
        template.convertAndSend(activeMQQueue,"你好!!!!!!!!!!!");
        System.out.println("------------");
    }

```

==注意:定时投放 事件监听 需要掌握==

```java
@Component
public class consum {
    @JmsListener(destination = "${myqueue}") //事件监听
    public void rec(TextMessage message) throws JMSException {
        System.out.println(message.getText());
    }
}
```

