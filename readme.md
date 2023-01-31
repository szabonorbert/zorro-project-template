# Zorro project template
An ideal starting point of a C++ Zorro project with Visual Studio.<br />

## What is Zorro?
>Zorro is a free institutional-grade software tool for data collection, financial research, and algorithmic trading with C / C++.  It's compact, portable, easy to learn, and magnitudes faster than R or Python. It does anything that automated trading platforms do - only better. Zorro offers extreme flexibility and features otherwise not found in consumer trading software. Any data analysis, visualization, or algo trading system can be realized with a small C or C++ script. R and Python machine learning libraries are also supported. - <https://zorro-project.com/>

## C++ and Visual Studio
Zorro's native language is "lite-C", however it's built-in functions are totally compatible with C and C++ as expected. In the Zorro Help you can find a tutorial about setting up a project in Visual Studio and/or it's compiler for making Zorro scripts ("Developing Algo Trading Systems in C++"). But it's not neccessarly fully documented, because there are some unmentioned gotchas you need to take care. I made this sample project to kickstart your development, therefore you don't need to do all the setup procedure every time you start to work on something new. I use Visual Studio simply because Zorro advise to use that - but I guess you can use any C++ compiler.

## How this project works

This project is a custom Visual Studio Solution folder, therefore you can build as huge script as you want, you don't need to stuck on Zorro's folder, and you can version control your entire project. After compiling, the result DLL file will be automatically copied to the Zorro's `myStrategy` folder, then you can run that immediately.

## Zorro setup requirements

* My Zorro setup folder is `C:\zorro\` but if you have different setup location you need to change this in the Solution files.
* In Zorro folder, you should make the `ZorroFix.ini` file, where you can define the strategy folder. My strategy folder is `myStrategy` and the solution copies the result files here, so I have a record in `ZorroFix.ini` file:
```
StrategyFolder = "myStrategy"
```
<https://zorro-project.com/manual/en/ini.htm>

## Solution notes

* It uses the following dependency: `C:\zorro\Source\VC++\ZorroDLL.cpp`
* It uses the following include directory: `C:\zorro\include` (therefore you can import `<zorro.h>` in .cpp files)
* Compiles neccessary files to project's `intermediate_dir` directory
* Compiles result files to the project's `bin` directory
* ...then copy the result .dll file from `bin` to `C:\Zorro\myStrategy` (32bit version: `[project folder name].dll`, 64bit version: `[project folder name]64.dll`)
* ...then you can run it from Zorro

The Visual Studio Solution and project name is simply just "project", and the result DLL file's name is coming from the parent folder name by the following after-build script, therefore you don't need to setup or rename anything, just copy the sources to a different folder and start the development. The after-build script:
```
set "str=$(MSBuildProjectDirectory)"
set "result=%str:\=" & set "result=%"
Rem echo %result%
copy /Y "$(TargetDir)$(TargetName).dll" "C:\zorro\myStrategy\"%result%"64.dll"
```
In 64 bit version, you will see that DLL filenames end with "64", because it's neccessary for running with Zorro64.