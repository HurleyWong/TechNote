## SpringBoot:No identifier specified for entity

遇到这种情况一般是因为实体类没有声明主键或者是@Id的位置放的不对，解决的方法就是声明主键或者将@Id放在对应字段的get()方法上

