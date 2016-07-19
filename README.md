# rapid-framework-4.0.5
来自https://github.com/badqiu/rapid-framework release的项目

#开发日记
##2016-04-24
1. 添加生成文档的相关方法，参数为tables
  - 使用方法：g.generateDoc();g.deleteDoc();
2. 添加移除列名前缀的方法，与移除table前缀的方法一致
  - 使用方法：在generator.xml文件里面添加<entry key="columnRemovePrefixes">f</entry>，可以使多个字符，逗号分隔
3. Column添加getNullable(),getIsPrimaryKey()方法
  - nullable可以用来判断字段是否为空，isPrimaryKey()可以使用!isNotIdOrVersionField()替换，但是较为繁琐，不直接
4. 解决无法获取Oracle表注释的问题
  - 修改获取Connection的方式，使用DriverManager.getConnection(url,properties)方式获取

##2016-04-30
1. 移除g.generateDoc();g.deleteDoc();
  - 后来发现可以使用现有的方法实现这种需求。  
    ```java
    GeneratorFacade g = new GeneratorFacade();  
    List<Table> tables = TableFactory.getInstance().getAllTables();  
    GeneratorModel model = GeneratorModelUtils.newGeneratorModel("tables", tables);  
    
    g.generateBy(model);
    ```
2. 修改列移除前缀时，className不正确的问题

##2016-07-13
1.使用jackson的@JsonIgnore注解，解决将结果转为json字符串时，循环引用导致stackoverflow的问题
2.包括Column的isNullable()方法也添加了上述注解
