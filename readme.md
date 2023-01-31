
# Zorro project template
An ideal starting point of a C++ Zorro project with Visual Studio.<br />

## What is Zorro?
>Zorro is a free institutional-grade software tool for data collection, financial research, and algorithmic trading with C / C++.  It's compact, portable, easy to learn, and magnitudes faster than R or Python. It does anything that automated trading platforms do - only better. Zorro offers extreme flexibility and features otherwise not found in consumer trading software. Any data analysis, visualization, or algo trading system can be realized with a small C or C++ script. R and Python machine learning libraries are also supported. _–_ <https://zorro-project.com/>

## C++ and Visual Studio
Zorro's native language is "lite-C", however the built-in functions are totally compatible with C and C++ as expected. In the Zorro Help you can find a tutorial about setting up a project in Visual Studio and/or it's compiler for making Zorro scripts: "Developing Algo Trading Systems in C++". I made this sample project to kickstart your development, therefore you don't need to do all the setup procedure every time you start to work on something new. I use Visual Studio 2022 simply because Zorro advise to use that - but I'm sure that any C++ compiler could to the work.

## About this Solution

This is a custom Visual Studio 2022 Solution folder, therefore

* you can build as huge software as you want even with a complex structure without messing up the strategy folder,
* you don't need to squeeze your files to Zorro's standard folders, and
* you can version control your entire project independently from your other strategies.

The result DLL file will be automatically copied to your Zorro's strategy folder, then you can run that script immediately. To start editing you just need to open the `project.sln` with Visual Studio (not Visual Studio Code).

## Zorro's custom strategy folder

It's recommended to create a custom strategy folder where you can keep all your scripts separately from the standard Zorro sample projects. You can do this simply by define the strategy folder in the `ZorroFix.ini` file of the root folder like this:
```
StrategyFolder = "myStrategy"
```
<https://zorro-project.com/manual/en/ini.htm>

## Solution config

There are only 2 variables you need to check before using this Solution. You can find them in the `ZorroProperties.props`, which is a simple text file.

* `ZorroLocation` is the install folder of Zorro **without trailing slash**. Default value is `C:\zorro`.
* `ZorroStrategyFolder` is the folder in the Zorro location, where you keep your strategies, pointed by `ZorroFix.ini`. Default value is `myStrategy`.

So if you install Zorro to `C:\zorro` and you use `myStrategy` for strategy folder, you don't need to change anything.

## Details

* It uses the following dependency: `$(ZorroLocation)\Source\VC++\ZorroDLL.cpp`
* It uses the following include directory: `$(ZorroLocation)\include` (therefore you can import `<zorro.h>` in .cpp files)
* Compiles intermediate files to project's `tmp` directory
* Compiles result files to the project's `bin` directory
* ...then copy the result DLL file from `bin` to `$(ZorroLocation)\$(ZorroStrategyFolder)`

...then you can run it from Zorro.

The Solution's name and also the project's name are the same: simply just "project". But the result DLL file's name generated from the parent folder's name by the after-build script. Therefore you don't need to setup or rename anything - just copy the files of this repository to a different folder and start the development. The after-build script will do the rest:
```
set "str=$(MSBuildProjectDirectory)"
set "result=%str:\=" & set "result=%"
Rem echo %result%
copy /Y "$(TargetDir)$(TargetName).dll" "$(ZorroLocation)\$(ZorroStrategyFolder)\"%result%"64.dll"
```
In 64 bit version, you will see that DLL filenames end with "64", because it's neccessary for running with Zorro64. Also note that if you don't have Zorro S subscription you can only run DLLs created in Release mode.