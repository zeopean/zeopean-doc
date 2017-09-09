

类内方法定义顺序依次是：公有方法或保护方法 > 私有方法 > getter/setter 方
法。

依赖关系  uses-a
聚合关系  has-a
继承关系	 is-a


java 允许重载任何方法



@param  	变量描述
	
@return 	返回值描述

@throws 	类描述

@version 	版本描述

@see 		引用描述




equals：
	自反性：对于任何非空引用，x.equals(x) 返回true
	对称性：对于任何引用 x， y， 当且仅当 y.equals(x) => true , x.equals(y) => true
	传递性：对于任何 x, y, z ，如果x.equals(y) => true , y.equals(z) => true, 那么 x.equals(z) => true
	一致性：如果x 和y 的引用对象没变化，反复调用 x.equals(y) 要改返回同样的结果
	对于任意非空引用x, x.equals(null) => false


int hashCode ： 返回对象的散列码
int hash     :  返回散列码 


java的反射解读：
	getName()  		获取类的名称
	getSimpleName()		获取类名，不包括包名
	getSuperClass() 	获取超类的类名
	getInterfaces()		获取本类所实现的所有接口的class对象
	Field[] getFields()	获取所有public属性，包括继承，接口中的，自定义的
	Field[] getDeclaredFields() 	获取当前类自己定义的属性


java内部类的使用


