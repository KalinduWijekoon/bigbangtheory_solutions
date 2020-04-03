Use `'gdb'` with `sheldon1`.<br>
As now, we know the specific function to be disassembled. In this case its `phase_2`. <br>
Disassemble `phase_2` and identify that it requires 6 numbers as its parameters. <br>
![](https://user-images.githubusercontent.com/37071700/78338061-b08d5380-75af-11ea-8a40-331b4bebc7a7.png)<br><br>
So, create a breack point in `phase_2` by using `b` and run the program using `r`. <br>
Provide the previous level's passphrase and hit enter. As for the next one we know that it required 6 numbers so, for this moment just enter ` 1 2 3 4 5 6` and hit enter, the breakpoint will be created.<br>
![](https://user-images.githubusercontent.com/37071700/78336761-8aff4a80-75ad-11ea-9e5d-6289e46534f9.png)<br><br>
Disassemble the function using `disas`. You can see that the first comparison is compared with number `1` in the assembly code it represent as bellow,<br><br>
**`cmp    DWORD PTR [ebp-0x18], 0x1`** <br><br>
![](https://user-images.githubusercontent.com/37071700/78339532-3dd1a780-75b2-11ea-8092-e0bba077da2d.png)<br>
So, we can guess that the first number is **" 1 "**.<br><br>
Using `ni` command (next instruction) or `until` command, go somewhere below to the next comparison statement which is **`cmp    DWORD PTR [esi+ebx*4], eax`** and get the information about current registry values using `i r` (info registers). After that, you can identify the register `"eax"` holds the value of **" 2 "**. According to the comparison statement, `[esi+ebx*4]` is compared with `eax`, so we can guess that our second number is **" 2 "**.<br>
![](https://user-images.githubusercontent.com/37071700/78341288-0d3f3d00-75b5-11ea-8370-2489f7d0d342.png)<br><br>
luckily, we entered `1 2 3 4 5 6` as our parameter so that the first two digits are OK.<br>
Moving on with the function, you can again run `ni` through the function to identify its behaviour.<br>
You will identify that the instruction pointer will move again to the instruction where **`lea    esi, [ebx+0x1]`**<br>
![](https://user-images.githubusercontent.com/37071700/78342055-517f0d00-75b6-11ea-8573-1f142f7ec60d.PNG)<br><br>
Again, move to the comparison function **`cmp    DWORD PTR [esi+ebx*4], eax`** using `ni` and view the register information to get an idea about the next integer that `eax` holds.<br>
![](https://user-images.githubusercontent.com/37071700/78342873-9bb4be00-75b7-11ea-83f3-4f0488a193d7.png)<br>
So, now `eax` holds **" 6 "**<br><br>
So far we identified that our first three integers are **1** **2** and **6**. As you can see, there is a pattern here and you don't need to go again through the fucntion to get the next numbers. (If you want, you can).<br>
After analyzing the number pattern we can represent the pattern using the below formula,<br><br>
**V[ i ] = V[ i-1 ] * i + 1** <br><br>
Where V[ i ] is the array value of the "i" th index<br>
Example : As now we know our first three parameters are **1 2 6**, so to find the fourth,<br>

    V[ 3 ] = V [ 3-1 ] * 4 + 1  ;  V [ 3-1 ] is the array value of the 2nd index which is 6 (Arrays are starting from **0**) 
      msg db '/bin/sh'
      
    section .text
      global _start
      
    _start:
      mov eax, 11
      mov ebx, msg
      mov ecx, 0
          
          


