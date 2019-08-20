# Activiti 插件安装

## Eclipse安装Activiti Designer插件

在线安装：Version: 2019-06 (4.12.0)

1. Help

2. Install new SoftWare

3. Add...

4. Name：Activiti BPMN 2.0 designer

   Location：http://activiti.org/designer/update/

5. Next - Finish

6. 检验是否安装成功：
   
   File -> New -> Others -> Activiti

7. 设置： 
   
   Preferences - Activiti - Save Actions - 勾选：Create process definition image when saving the diagram
 

## IDEA 安装

安装： Version: IntelliJ IDEA 2018.2.5 (Ultimate Edition)

1. IntelliJ IDEA

2. Preferences...

3. Plugins 

4. 查询actiBPM
   
   Search in repositories

5. Install

6. Restart IntelliJ IDEA 重启

7. 检验是否安装成功：
   
   Plugins 中 actiBPM插件。
   
使用：

1. File -> New -> BpmnFile 

2. 流程设计（流程设计器页面）

3. 修改文件后缀。 把bpmn后缀修改为xml后缀。

4. 右击xml文件，选择 Diagrams -> Show BPMN 2.0 Diagrams...

5. 导出png图片： Export to file -> Save as image