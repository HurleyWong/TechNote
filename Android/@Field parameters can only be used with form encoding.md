## @Field parameters can only be used with form encoding

如果在使用Retrofit时的POST请求时出现以上错误，是意味着使用了@Field但是没有使用@FormUrlEncoded与之对应。

注意，@FormUrlEncoded和@Field简单的表单键值对。两个需要结合使用，否则会出现以上错误。