---
title: "杭电计算机组成实验 实验6-MIPS汇编器与模拟器实验"
description: "Welcome to XdpCs’s blog!"
date: "2020-12-22"
tags: ["MIPS"]
---

## 实验内容

1. 学习 MIPS指令系统，熟悉 MIPS指令格式及其汇编指令助记符，掌握机器
   指令编码方法
2. 学习 MIPS汇编程序设计，学会使用 MIPS 汇编器将汇编语言程序翻译成二
   进制文件
3. 了解使用 MIPS教学系统模拟器运行程序的方法

## 解决方法

1. 下载 PCSpim 软件
2. 给大家一个下载的地方，只要关注我，就可以下载到[PCSpim下载地址](https://download.csdn.net/download/DoMoreSpeakLess/13758567)
3. 按照书上的要求，在文本编辑器中输入汇编程序，然后装入PCSpim
4. 左侧内为指令地址，中间是十六进制的指令编码，右侧是相应的标准汇编指
   令，主要注意的是第二个程序，必须在裸机执行方式
5. 书上的汇编和结果展示：

**test.asm**

```bash
main:	li $v0 , 5
	syscall
	move  $t0,$v0
	li   $v0,5
	syscall	
	move $t1 , $v0
	bgt $t0,$t1,t0_bigger
	move $t2,$t1
	b endif
t0_bigger : move $t2,$t0
    endif :move $a0,$t2
           li $v0,1
	syscall
	jr $ra
```

**R_CPU_Test.asm**

```bash
main:nor $1,$0,$0;		#$1 = FFFF_FFFF	
sltu $2,$0,$1;		#$2 = 0000_0001 if($2<$3) $1=1 else $1=0
add $3,$2,$2;		#$3 = 0000_0002
add $4,$3,$2;		#$4 = 0000_0003
add $5,$4,$3;		#$5 = 0000_0005
add $6,$5,$3;		#$6 = 0000_0007
sllv $7,$6,$2;		#$7 = 0000_000E $1=$2<<$3
add $9,$5,$6;		#$9 = 0000_000C
sllv $8,$6,$9;		#$8 = 0000_7000
xor $9,$1,$8;		#$9 = FFFF_8FFF
add $10,$9,$1;		#$10 = FFFF_8FFE
sub $11,$8,$7; 		#$11 = 0000_6FF2
sub $12,$7,$8;		#$12 = FFFF_900E
and $13,$9,$12; 	#$13 = FFFF_800E
or $14,$9,$12;		#$14 = FFFF_9FFF
or $15,$6,$7;		#$15 = 0000_000F
nor $16,$6,$7;		#$16 = FFFF_FFF0
add $17,$7,$3;		#$17 = 0000_0010
sllv $18,$8,$17;	#$18 = 7000_0000
sllv $19,$3,$17;	#$19 = 0002_0000
sllv $20,$19,$7;	#$20 = 8000_0000
add $21,$20,$1; 	#$21 = 7FFF_FFFF
or $22,$18,$21		#$22 = 7FFF_FFFF
add $23,$20,$22;	#$23 = FFFF_FFFF
sub $24,$20,$22;	#$24 = 0000_0001
sub $25,$22,$20;	#$25 = FFFF_FFFF
xor $26,$18,$1;		#$26 = 8FFF_FFFF
sltu $27,$22,$20;	#$27 = 0000_0001
sltu $28,$26,$20;	#$28 = 0000_0000
add $29,$22,$2;		#$29 = 8000_0000
sub $30,$20,$2;		#$30 = 7FFF_FFFF
add $31,$11,$26;	#$31 = 9000_6FF1
```

**结果机器码展示**

```verilog
00000827 0001102b 00421820 00622020 00832820 00a33020 00463804 00a64820 01264004 00284826 01215020 01075822 00e86022 012c6824 012c7025 00c77825 00c78027 00e38820 02289004 02239804 00f3a004 0281a820 0255b025 0296b820 0296c022 02d4c822 0241d026 02d4d82b 0354e02b 02c2e820 0282f022 017af820
```

## 代码地址

[代码地址](https://github.com/XdpCS/HDU-Computer-Organization-And-Architecture-Experiment/tree/master/Sixth_experiment)

