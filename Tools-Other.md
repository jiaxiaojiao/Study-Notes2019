## 其他工具

- [常见的Bean映射工具（BeanUtils Dozer）](#常见的Bean映射工具)

### 常见的Bean映射工具：

不同业务层传输对象存在不同的格式，因此我们需要编写映射代码将对象中的属性值从一种类型转成另一种类型。进行这种转换除了手动编写大量的get/set代码，还可以使用一些方便的类库，常用的有apache的BeanUtils，spring的BeanUtils，cglib的BeanCopier。

- **BeanUtils**

    apache的BeanUtils和spring的BeanUtils中拷贝方法的原理都是先用jdk中 java.beans.Introspector类的getBeanInfo()方法获取对象的属性信息及属性get/set方法，接着使用反射（Method的invoke(Object obj, Object... args)）方法进行赋值。apache支持名称相同但类型不同的属性的转换，spring支持忽略某些属性不进行映射，他们都设置了缓存保存已解析过的BeanInfo信息。

- **BeanCopier**
    
    cglib的BeanCopier采用了不同的方法：它不是利用反射对属性进行赋值，而是直接使用ASM的MethodVisitor直接编写各属性的get/set方法（具体过程可见BeanCopier类的generateClass(ClassVisitor v)方法）生成class文件，然后进行执行。由于是直接生成字节码执行，所以BeanCopier的性能较采用反射的BeanUtils有较大提高，这一点可在后面的测试中看出。

- **Dozer**

    使用以上（1和2）类库虽然可以不用手动编写get/set方法，但是他们都不能对不同名称的对象属性进行映射。在定制化的属性映射方面做得比较好的有Dozer，Dozer支持简单属性映射、复杂类型映射、双向映射、隐式映射以及递归映射。可使用xml或者注解进行映射的配置，支持自动类型转换，使用方便。但Dozer底层是使用reflect包下Field类的set(Object obj, Object value)方法进行属性赋值，执行速度上不是那么理想。

- **Orika**

    特性丰富，速度又快。底层采用了javassist类库生成Bean映射的字节码，之后直接加载执行生成的字节码文件，因此在速度上比使用反射进行赋值会快很多。
    
    Github上项目的地址： <https://github.com/orika-mapper/orika>

- [**MapStruct**](http://mapstruct.org/)
    
    只需要定义一个 Mapper 接口，MapStruct 就会自动实现这个映射接口，避免了复杂繁琐的映射实现。



[**返回首页目录**](README.md)