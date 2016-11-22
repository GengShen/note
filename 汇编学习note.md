- unix64 汇编环境

        编译器:nasm
            linux:nasm -elf64 **.asm
            mac:nasm -macho64 **.asm
            nasm语法:
                - 寄存器别名
                - 内存偏移
                - 源程序框架
                    > gloabl main
                    > main:
                    > 程序
                    > ret
                    
        连接器: gcc
            gcc -m64 **.o -o **
            
        调试器:gdb
            gdb ./**
            > set assembly-flavor intel 
            > disas main  进入主程序，将指令内存以intel输出
            > break *内存偏移
            > run
            > info register eax
            > info all
            > stepi
            > disas  查看到哪一步
            > continue


- 数据create及update
        
        都要在寄存器中进行
            move 寄存器 数据
            move 寄存器 寄存器
            add 寄存器 ..
            sub 寄存器 ..


- 字的传送

        8086为16位数据线，故指出寄存器为x就成


- 段
        
        数据段 ds | mov add sub
        代码段 cs:ip
        栈段 sp:ss | pop push


- 代码数据

        寄存器 -> cs:ip -> 指令首位


- 内存段偏移寻址

        ds+[num] -  数据定位:出现[x] 即为 ds+x的内存地址
        寄存器:[bx] - 寄存器做段地址，bx中数据做偏移量
        
        ------------
        
        寄存器写入内存单元

        mov bx 1000H  //2个字节
        mov ds,bx   //2个字节成为段地址
        mov [0],al  //0为偏移量，al为1个字节
        or
        mov al,[0] //语境都是ds为段地址


- 栈

        ss:sp -> 栈顶
        出入栈默认ss:sp
        
        --------------

        push x x数据进栈
        pop x 出栈进x
        push及pull操作，都只修改sp，故栈空间为00 00 - FF FF
        sp以ss为起始，在00 00 - FF FF循环

- 指令转移
        
        jmp
            跳转到标志
                short 只改ip
                far cs:ip都改
        ret
        call
        
        loop
             mov cx 12
           s:代码段1
             代码段2
             loop s     ->判断s-1是否为0，否则回到s地址，是则执行下面代码
         
        if

- 内存数据寻址 存取值

        - 位置：
            cpu 内存 端口
        
        - 位置表达
            内存：
                立即数：直接以数字表达 eg：2000h 00010000b
                基址+偏移地址，[ ] 
            寄存器：
                寄存器名

- 数据大小表达
        
        寄存器
        
        内存
        
        常量初始化
            db 1byte
            dw 2byte
            dd 4byte

- 计算
      
        加 add
        减 sub
        乘 mul
        除
            寄存器保存被除数及结果

- 中断
        
        标志寄存器
            外部
            内部

- 端口访问
