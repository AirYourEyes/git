# 第一章 初次运行git的配置
### 1. 设置用户名和用户邮箱  
```  
~$ git config --global user.name "John"
~$ git config --global user.email "John@163.com"
```  
***若要给指定的项目使用其他的邮箱和用户名，可以去掉global参数***    
### 2. 查看所有配置信息    
```
~$ git config --list
```    
### 3. 查看指定的信息
#### 3.1 查看用户名  
```  
~$ git config user.name
```  
#### 3.2 查看用户邮箱  
```  
~$ git config user.email
```    
### 4. 获取帮助
```
~$ git help <verb>
~$ git <verb> --help
~$ man git-<verb>
```    
如：  
```
~$ git help config
~$ git config --help
~$ man git-config
```  

  
