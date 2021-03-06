响应消息的第一行是状态行，由协议版本，一个空格符（SP），状态码，另一个空格符，一个可能为空的描述状态码的文本短语和结尾的CRLF构成。

> ```
> status-line = HTTP-version SP status-code SP reason-phrase CRLF
> ```

status-code元素是一个3位数的整数号码，描述了服务器试图理解和满足对应客户端请求的结果。响应消息的其余部分将根据为该状态码定义的语义进行解释。查看RFC7231的第6节了解状态码语义信息，包括状态码的分类，本协议对状态码的定义，新状态码定义的考虑和IANA注册管理机构。

> ```
>  status-code    = 3DIGIT
> ```

原因短语元素的存在仅仅是为了提供与数字状态码相关的文本描述，主要不在于早期的互动式文本客户端更常使用的互联网应用协议。客户端应该忽略原因短语的内容。

> ```
>   reason-phrase  = *( HTAB / SP / VCHAR / obs-text )
> ```