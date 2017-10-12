This is example of avro. <br>
<br>
Avro Introduction:<br>
    我们已经接触过很多序列化框架（或者集成系统），比如protobuf、hessian、thrift等，它们各有优缺点以及各自的实用场景，Avro也是一个序列化框架，它的设计思想、编程模式都和thirft非常相似，也都是Apache的顶级项目。Avro还提供了RPC机制，可以不需要生成额外的API代码即可使用Avro来存储数据和RPC交互，“代码生成”是可选的，这一点区别于protobuf和thrift。此外Hadoop平台上的多个项目正在使用（或者支持）Avro作为数据序列化的服务。<br>     
    Avro尽管提供了RPC机制，事实上Avro的核心特性决定了它通常用在“大数据”存储场景（Mapreduce），即我们通过借助schema将数据写入到“本地文件”或者HDFS中，然后reader再根据schema去迭代获取数据条目。它的schema可以有限度的变更、调整，而且Avro能够巧妙的兼容，这种强大的可扩展性正是“文件数据”存储所必须的。<br>      
    Avro是基于schema（模式），这和protobuf、thrift没什么区别，在schema文件中（.avsc文件）中声明数据类型或者protocol（RPC接口），那么avro在read、write时将依据schema对数据进行序列化。因为有了schema，那么Avro的读、写操作将可以使用不同的平台语言。Avro的schema是JSON格式，所以编写起来也非常简单、可读性很好。目前Avro所能支持的平台语言并不是很多，其中包括JAVA、C++、Python。<br>     
    当Avro将数据写入文件时，将会把schema连同实际数据一同存储，此后reader将可以根据这个schema处理数据，如果reader使用了不同的schema，那么Avro也提供了一些兼容机制来解决这个问题。     在RPC中使用Avro，Client和server端将会在传输数据之前，首先通过handshake交换Schema，并在Schema一致性上达成统一。<br>

![](https://github.com/changechenyu/ShakeToFresh/blob/master/app/src/main/res/drawable/shake.gif)
