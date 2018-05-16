---
title: 从eclipse到idea Community
tags:
- idea
- eclipse
- jetBrain
---

### 调整设置

1. 将import * 调整为500

   `File`-> `Setting` -> `Code Style`->`Java`选择Imports 

   将`Class count to use import with '*'`修改为500(建议值)

   将`Names count to use static import with '*'` 修改为500(建议值)

   > Class count to use import with '*' 导入class达到500条时使用import \*代替

   ​

2. 调整import 顺序

   `File`-> `Setting` -> `Code Style`->`Java`选择Imports

   设置Import Layout

   ```
   static all other, 
   blank, 
   java.*, 
   blank, 
   javax.*, 
   blank, 
   org.*, 
   blank, 
   com.*, 
   blank, 
   all other imports
   ```

   如图所示

   ![layout1](http://om8bq99t5.bkt.clouddn.com/17-5-12/4131747-file_1494587266082_920d.png)
   ![layout2](http://om8bq99t5.bkt.clouddn.com/17-5-12/78262524-file_1494587507430_6d4d.png)

3. tab用四个空格键代替

   `File`->`Setting`->`Code Style`->`Groovy`选择Tabs and Indents 将 `Use tab character` 的勾去掉

   ![img](http://om8bq99t5.bkt.clouddn.com/17-5-12/87029098-file_1494586782026_6f78.png)

   ​

4. idea+spring-boot+devtools热部署

   - 在`pom.xml` 文件中加入新依赖 

     ```xml
     <dependency>  
         <groupId>org.springframework.boot</groupId>  
         <artifactId>spring-boot-devtools</artifactId>  
         <optional>true</optional>  
     </dependency>  
     ```

   - 在`pom.xml`的builder中加入

     ```xml
     <build>  
         <plugins>  
             <plugin>  
                 <groupId>org.springframework.boot</groupId>  
                 <artifactId>spring-boot-maven-plugin</artifactId>  
                 <configuration>  
                 <!--fork :  如果没有该项配置，肯呢个devtools不会起作用，即应用不会restart -->  
                 <fork>true</fork>  
                 </configuration>  
             </plugin>  
         </plugins>  
     </build>  
     ```

   - 在idea 中 `File`>`Build,Execution,Deployment`>`Compiler`给`Build priject automatically`打√

     ![](http://om8bq99t5.bkt.clouddn.com/17-5-13/52539784-file_1494665551221_dedd.png)

   - 在idea中按下`ctrl+shift+alt+/`呼出配置菜单，选择Registry

     ![](http://om8bq99t5.bkt.clouddn.com/17-5-13/50475758-file_1494665660680_a0fb.png)

   - 找到`compiler.automake.allow.when.app.running`并打勾

   - ![](http://om8bq99t5.bkt.clouddn.com/17-5-13/3861166-file_1494665712905_11897.png)




### 插件

`File`>`Setting` > `Plugins` `> `

1.代码缩略图 `CodeGlance`

![](http://om8bq99t5.bkt.clouddn.com/17-5-13/9955948-file_1494666008157_bc50.png)

### 快捷键







