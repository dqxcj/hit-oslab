改写 `bootsect.s` 主要完成如下功能：

1.  bootsect.s 能在屏幕上打印一段提示信息“XXX is booting...”，其中 XXX 是你给自己的操作系统起的名字，例如 LZJos、Sunix 等（可以上论坛上秀秀谁的 OS 名字最帅，也可以显示一个特色 logo，以表示自己操作系统的与众不同。）

我的做法:
1. 修改bootsect.s第244行的显示信息，如下:
```asm                                                                                                                            
244 msg1:                                                                                                                             
245     .byte 13,10
246     .ascii "****************"
247     .byte 13,10
248     .ascii "Loading WuOs ..."
249     .byte 13,10
250     .ascii "****************"
251     .byte 13,10,13,10
```

2. 修改bootsect.s第99行的字符个数，上面共58个字符，故将99行处的cx的值由24改为58
3. 重新编译运行

运行结果如图:

![](https://raw.githubusercontent.com/dqxcj/Study/test/test2/test7/test8/202211141210390.png)