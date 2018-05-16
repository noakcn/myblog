与其他指令一样，ng-if指令也会创建一个子级作用域，因此，如果在ng-if指令中添加了元素，并向元素属性增加 ng-model指令，那么ng-model指令对应的作用域属性子级作用域，而并非控制器注入的$scope作用域对象，这点在进行双向数据绑定时，需要引起注意。



### 解决

1.可以在ng-if里面的ng-model中使用`$parent`来绑定父类的变量，如 `$parent.value`



2.使用controller as来代替$scope



3.懒人法，使用ng-show代替ng-if