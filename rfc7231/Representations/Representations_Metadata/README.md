表示头字段提供了与表示形式相关的元数据。当一个消息包含负载体时，表示形式头字段描述了如何解释包含在负载体中的表示数据。在一个HEAD请求的响应中，表示形式头字段描述了在相同的GET请求的负载体包含的表示数据。

下面头字段传达了表示形式元数据：
> ```
> +-------------------+-----------------+
> | Header Field Name | Defined in...   |
> +-------------------+-----------------+
> | Content-Type      | Section 3.1.1.5 |
> | Content-Encoding  | Section 3.1.2.2 |
> | Content-Language  | Section 3.1.3.2 |
> | Content-Location  | Section 3.1.4.2 |
> +-------------------+-----------------+
> ```

