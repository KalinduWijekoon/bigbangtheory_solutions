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
So far we identified that our first three integers are **1** **,** **2** and **6**. As you can see, there is a pattern here and you don't need to go again and again through the fucntion to get the next numbers. (If you want, you can).<br>
After analyzing the number pattern we can represent the pattern using the below formula,<br><br>
**V[ i ] = V[ i-1 ] * i + 1** <br><br>
Where V[ i ] is the array value of the "i" th index<br>
As now we know our first three parameters are `1 , 2, and 6`, **(0th == 1 , 1st == 2 , 2nd == 6)**  so to find the fourth number which is the 3rd index,<br>

    V[ 3 ] = V [ 3-1 ] * 3 + 1  ; V [ 3-1 ] is the array value of the 2nd index which is 6 (Arrays are starting from 0)
    V[ 3 ] = V [ 2 ] * 4
    V[ 3 ] = 6 * 4
    V[ 3 ] = 24 

So we got our fourth number which is `24`<br><br>
Now we have our first four parameters which are `1, 2, 6, and 24`, **(0th == 1 , 1st == 2 , 2nd == 6 , 3rd == 24)**  so to find the fifth number which is the 4th index,<br>

    V[ 4 ] = V [ 4-1 ] * 4 + 1  ; V [ 4-1 ] is the array value of the 3rd index which is 24 (Arrays are starting from 0)
    V[ 4 ] = V [ 3 ] * 5
    V[ 4 ] = 24 * 5
    V[ 4 ] = 120
    
So we got our fifth number which is `120`<br><br>
Now we have our first five parameters which are `1, 2, 6, 24, and 120`, **(0th == 1 , 1st == 2 , 2nd == 6 , 3rd == 24 , 4th == 120)**  so to find the final number which is the 5th index,<br>

    V[ 5 ] = V [ 5-1 ] * 5 + 1  ; V [ 5-1 ] is the array value of the 4th index which is 120 (Arrays are starting from 0)
    V[ 5 ] = V [ 4 ] * 6
    V[ 5 ] = 120 * 6
    V[ 5 ] = 720 
    
So we got our sixth number which is `720`<br><br>
Now we have all our six parameters which are **`1 2 6 24 120 720`**<br><br>
Run the program again and use the previous level's passphrase (you can use a text file contains all previous level passphrases as well) and as for the second passphrase, type **1 2 6 24 120 720** and hit enter.<br> 
![](https://user-images.githubusercontent.com/37071700/78348443-a410f700-75bf-11ea-8091-56c6e8d06f27.png)















