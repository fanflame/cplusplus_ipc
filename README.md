## 进程间通信

### 管道：
#### 无名管道
#### 特点
底层用队列实现；
管道中内容，读完就删除了；
缺点：只能在父子进程或有亲缘关系的进程中使用
#### 使用：
```
int	 pipe(int [2]);//创建无名管道,参数返回写和读文件操作符
```
读写使用read/write函数；
close关闭文件操作符
#### 相关代码：
pipe_unname.cpp
#### 有名管道
#### 特点
在文件系统中存在文件节点：管道文件；
该文件不占磁盘空间；
可以实现无亲缘关系进程间通信；
本质：内核中以队列形式存在的缓存；
#### 使用
```
int	mkfifo(const char *, mode_t);//创建管道对象
int	open(const char *, int, ...)；//打开管道
```
读写使用read/write函数；
相关代码：
pipe_name.cpp；
pipe_name_antherprogress.cpp

### 信号通信：
#### 特点
使用内核中已经存在的信号对象；
kill -l查看内核中支持多少种信号；
需要接收进程存在；
raise函数把信号发给当前进程；
alarm函数：定时一段时间发出信号给当前进程，终止进程；
接收信号的进程条件不能结束：；
sleep;while(1)；
pause()与sleep状态一样；
 
### 共享内存
#### 特点
共享内存读完之后，内容还存在；
#### 使用
```
key_t	ftok(const char *, int);//创建key
int	shmget(key_t, size_t, int);//创建共享内存对象
void	*shmat (int, const void *, int);//内存映射
int	shmdt(const void *);//将用户空间的内存释放
int	shmctl(int, int, struct shmid_ds *)//将内核空间的内存释放
```
### 消息队列
#### 特点
链式队列；
读完内容之后，消息就删除了；
一个消息队列可以供两个进程双向通信
#### 使用
```
int msgget(key_t, int);//创建消息队列对象
int msgsnd(int, const void *, size_t, int)//发送消息
ssize_t msgrcv(int, void *, size_t, long, int)//接收消息
int msgctl(int, int, struct msqid_ds *)//删除、设置读取消息队列对象
```
### 信号灯
#### 特点
进程、线程间同步
略

### 内存映射
#### 使用
```
void *	mmap(void *, size_t, int, int, int, off_t);//内存映射
int	munmap(void *, size_t)；//释放
```
内存映射完成之后，可以直接操作内存
 
 


