Give execute permission to the file `sheldon1` and then run it using `./sheldon1` <br>
![](https://user-images.githubusercontent.com/37071700/76168871-5c05dc80-6199-11ea-93dd-af7874890469.PNG)<br><br>
Use `gdb` with `sheldon1`.<br>
![](https://user-images.githubusercontent.com/37071700/76168902-9b342d80-6199-11ea-945b-47ce8be62d4d.PNG)<br><br>
Use gdb's `info functions` command to get all available functions in sheldon1, and identify the `"main"` function (can use `start` as well).<br>
![](https://user-images.githubusercontent.com/37071700/76168923-c74fae80-6199-11ea-8c39-6cd5df608082.PNG)<br>
![](https://user-images.githubusercontent.com/37071700/76169039-a8055100-619a-11ea-8d05-8c9d1470eba8.PNG)<br><br>
Then set the `disassemble flavour` as `intel` and then disassemble the main function<br>
![](https://user-images.githubusercontent.com/37071700/76169103-26fa8980-619b-11ea-930c-366baaae9153.PNG)<br><br>
Find a special function called `phase_1`<br>
![](https://user-images.githubusercontent.com/37071700/76169144-780a7d80-619b-11ea-890e-c12902948205.PNG)<br><br>
Disassemble the `paese_1` function using `disas phase_1` command <br>
![](https://user-images.githubusercontent.com/37071700/76169189-c7e94480-619b-11ea-952b-e8bf744f8e85.PNG)<br><br>
Here, you can find an instruction named `test` and there the program will check the values of `eax` and `eax`. In top of that, about like 4 lines before, there is a static push to the stack.<br>
Print out the string value of this using `x/s` and get the passphrase for phase_1.<br>
![](https://user-images.githubusercontent.com/37071700/76169298-c9ffd300-619c-11ea-955a-6a036ed18e90.PNG)

