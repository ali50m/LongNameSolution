# dotnet can not add too much projects to solution file

## problem description

when I add too much projects to solution file, dotnet will throw an exception. If you reduce the number of projects (e.g. to 300 items), it will work.

## how to add all projects to solution
```pwsh
dotnet sln add --in-root (ls -r src/**/*.csproj)
```

## error output:  
```
ResourceUnavailable: Program 'dotnet.exe' failed to run: An error occurred trying to start process 'C:\Program Files\dotnet\dotnet.exe' with working directory 'C:\Users\liu\source\repos\LongNameSolution'. 文件名或扩展名太长。At line:1 char:1
+ dotnet sln add --in-root (ls -r src/**/*.csproj)
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~.
```

## script to create this solution

```pwsh
mkdir LongNameSolution && cd LongNameSolution && dotnet new sln ; $i = 1; while ($i -le 5) { $num = "{0:000}" -f $i; dotnet new classlib -o "src\LongNameProject$num"  | Out-Null ; $i += 1; }
```

## Environment

```
dotnet 7
Windows 10
```