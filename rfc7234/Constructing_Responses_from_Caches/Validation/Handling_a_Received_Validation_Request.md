每个在请求链上的客户端都可能有它自己的缓存，所以对一个作为中介的缓存来说从其他缓存（出站）接收条件请求是普遍的。同样，一些用户代理利用条件请求来限制数据转移到最近被修改的表示或完成部分取回表示的转移。

如果一个缓存接受了一个可以通过重用一个它存储的200或206响应来满足的请求，那么缓存**应该**以包含在被选响应中的对应验证器来评估任何适用的包含在那个请求中的条件头字段先决条件。缓存**不得**评估只对源服务器适用的条件头字段，在请求中发现的带有不能被已缓存响应满足的语义，或应用于没有存储响应的目标资源；这个先决条件可能确实是针对其他（入站）服务器的。

缓存正确评估条件请求基于被接收到的先决条件头字段和他们的优先权，如RFC7232中第6节定义。If-Match和If-Unmodified-Since条件头字段不适用于缓存。

包含If-None-Match头字段（RFC7232，3.2节）的请求表示客户端想要将一个或多个它已存储的响应与缓存已存储的被选响应进行比较来进行验证。如果字段值是“*”，或者如果字段是是一个实体标签i了表并且至少其中的一个匹配了被选的已存储响应的实体标签，缓存接收者**应该**生成一个304响应（适用被选已存储响应的元数据）代替那么已存储的响应。

当一个缓存决定为一个包含列出实体标签的If-None-Match头字段的请求重新验证它自己的已存储响应时，缓存**可能**将接收到的列表与来自其自身存储的响应集的实体标签列表组合并发送者两个列表的联合作为被转发的请求中的替换的If-None-Match头字段的值。如果一个已存储响应只包含部分内容，缓存**不得**在组合中包括它的实体标签，除非请求是一个可以被已存储的部分完全满足的range请求。如果被转发请求的响应是304并且有一个不在客户端列表中的实体标签ETag头字段，缓存**必须**通过复用由304响应元数据更新的它对应的已存储响应来生成一个200响应给客户端（4.3.4节）。

如果一个If-None-Match头字段没有出现，一个包含If-Modified-Since头字段（RFC7232，3.3节）的请求表示客户端想要通过修改日期来验证一个或多个它的已存储响应。如果下列任意条件为真，一个缓存接收者**应该**生成一个304响应（适用被选已存储响应的元数据）：

1. 被选已存储响应由一个Last-Modified字段值，它小于等于条件请求的时间戳；
2. 没有Last-Modified字段出现在被选已存储响应中，但是它由一个Date字段值，它小于等于条件请求的时间戳；
3. Last-Modified和Date都没有出现在被选已存储响应中，但是缓存记录了它被接收到的时间，它小于等于条件请求的时间戳。

实现了对范围请求的部分响应的缓存，如RFC7233中定义，也需要根据它的被选已存储响应来评估接收到的If-Range头字段（RFC7233，3.2节）。