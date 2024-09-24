# Conduct buffer overflow attack on bof1.c, bof2.c, bof3.c programs
## 2110011 - Trần Đại Dương
### 1. bof1.c
1. To make a buffer overflow attack in bof1.c program, we see the program has array with size of 200 inside vuln function, we can visualize as model below:
  
  ![image](https://github.com/user-attachments/assets/7f728e32-0ee4-4024-9fcb-ca350d762b76)
  
  Build the program using gcc -g bof1.c -o bof1.o and -fno-stack-protection to disable stack protection and set boundary = 2:
  
 Go to gdp of 'bof1.out' with the command gdb bof1.out -q, and find the address of the 'selectFunc' function with the command disas secretFunc. So we can get the address of function 'selectFunc' as follows '0x0804846b'

Go to gdp of 'bof1.out' with the command gdb bof1.out -q, and find the address of the 'selectFunc' function with the command disas secretFunc. So we can get the address of function 'selectFunc' as follows '0x0804846b'

Run the program with the 204 letter 'a' plus the address of the 'selectFunc' function with the following command (python -c "print('a'*204+'\x6b\x84\x04\x08')") | ./bof1.out
![image](https://github.com/user-attachments/assets/24ac1b3e-adc8-422f-98dc-a9c4eecbc4b8)
The terminal showing the 'Congratulation!' line from the 'secretFunc' function which means this method worked

### 2. bof2.c 
In this program, we need to make buffer overflow to spill the data into ‘check’ variable to make it equals to 0xdeadbeef to satisfy the condition. First, we visualize the Stack frame:

![image](https://github.com/user-attachments/assets/85c7574a-a22e-4bb9-9bcf-a303a15f3bd0)

Build the program using gcc -g bof2.c -o bof2.out and -fno-stack-protection to disable stack protection and set boundary = 2: gcc -g bof2.c -o bof2.out -fno-stack-protector -mpreferred-stack-boundary=2. Go to gdp of 'bof2.out' with the command gdb bof2.out -q, and find the address of the 'main' function with the command disas main. So we can get the address of function 'main'

![image](https://github.com/user-attachments/assets/c1192dbc-f6ac-44a8-b6ab-b1a3bfd520f3)

If you run the program with the 40 letter 'a' plus an address other than the following address 0xdeadbeef with the following command (python -c "print('a'*40+'\xef\xbe\xad\xdf')") | ./bof2.out

![image](https://github.com/user-attachments/assets/1af522bf-edd9-4fd3-b553-efc76ed9fc24)

The terminal showing the 'You are on the right way!' line from the 'main' function which means that you need to use 0xdeadbeef

Run the program with the 40 letter 'a' plus the address of the 0xdeadbeef with the following command (python -c "print('a'*40+'\xef\xbe\xad\xde')") | ./bof2.out

![image](https://github.com/user-attachments/assets/dea1c678-6ad1-42fd-9fd0-d1779e6e7613)

The terminal showing the 'Yeah! You win!' line from the 'main' function which means this method worked


