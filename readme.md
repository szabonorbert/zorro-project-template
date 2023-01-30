# Zorro project sample
An ideal starting point of a C++ Zorro project with Visual Studio<br />

## What is Zorro?
Zorro is a free institutional-grade software tool for data collection, financial research, and algorithmic trading with C/ C++.  It's compact, portable, easy to learn, and magnitudes faster than R or Python. It does anything that automated trading platforms do - only better. Zorro offers extreme flexibility and features otherwise not found in consumer trading software. Any data analysis, visualization, or algo trading system can be realized with a small C or C++ script. R and Python machine learning libraries are also supported. More info at <https://zorro-project.com/>.

## C++ and Visual Studio
Zorro's native language is "lite-C", however it's built-in functions are totally compatible with C and C++ as expected. In the Zorro help you can find a tutorial about setting up a project in Visual Studio and/or it's compiler for making Zorro softwares ("Developing Algo Trading Systems in C++"). But it's not neccessarly fully documented, because there are some unmentioned gotchas you need to take care. I made this sample project to kickstart your development, therefore you don't need to do all the setup procedure every time you start to work on something new. <br /> I use Visual Studio simply because Zorro advise to use that - but I guess you can use any C++ compiler.

## How this project works

This project is a custom Visual Studio solution folder, therefore you can build as huge script as you want, you don't need to stuck on Zorro's folder, and you can version control your entire project. After compiling, the result dll file will be copied to the Zorro's myStrategy folder, and you can run immediately.

## Zorro setup requirements

* My Zorro setup folder is C:\zorro\ but if you have different setup location you need to change this in the project files.<br />
* In Zorro folder, you should make the `ZorroFix.ini` file, where you can define the strategy folder. My strategy folder is myStrategy and the solution copies the result files here, so I have a record in ZorroFix.ini file:
```
StrategyFolder = "myStrategy"
```
<https://zorro-project.com/manual/en/ini.htm>
