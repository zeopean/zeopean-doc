
## 约定优先与配置

举个例子，假设${basedir}表示项目路径，下面的表格展示了项目源码文件目录、资源文件目录和其他配置的默认值：


source code	${basedir}/src/main/java
resources		${basedir}/src/main/resources
Tests			${basedir}/src/test
Complied byte code	${basedir}/target
distributable JAR	${basedir}/target/classes



## maven 常见插件

下面是一些常用的插件的列表：
插件		描述
clean		构建完成后清理目标，删除目标目录。
compiler	编译Java源文件。
surefile	运行JUnit单元测试，生成测试报告。
jar			从当前项目生成JAR文件。
war			从当前项目生成WAR文件。
javadoc	生成项目的Javadoc。
antrun		运行任意指定构建阶段的一系列ant任务。




```
mvn 	-v 	查看版本
		compile 编译
		test 测试
		package 打包
		
		clean  清除 target
		install 安装jar 包到本地仓库
		
		clean package -U		 创建项目快照
		archetype:generate   使用maven 构建项目
		

```