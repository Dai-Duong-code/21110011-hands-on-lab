# Conduct buffer overflow attack on bof1.c, bof2.c, bof3.c programs
## 2110011 - Trần Đại Dương
### 1. bof1.c
1. To make a buffer overflow attack in bof1.c program, we see the program has array with size of 200 inside vuln function, we can visualize as model below:
  
  ![image](https://github.com/user-attachments/assets/7f728e32-0ee4-4024-9fcb-ca350d762b76)
  
  Build the program using gcc -g bof1.c -o bof1.o and -fno-stack-protection to disable stack protection and set boundary = 2:
  
 Go to gdp of 'bof1.out' with the command gdb bof1.out -q, and find the address of the 'selectFunc' function with the command disas secretFunc. So we can get the address of function 'selectFunc' as follows '0x0804846b'
