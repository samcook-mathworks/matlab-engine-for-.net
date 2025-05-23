# MATLAB Engine API for .NET
The MATLAB&reg; Engine API for .NET&reg; provides an interface between .NET programming languages and MATLAB. This API enables programs to launch MATLAB, evaluate MATLAB functions with arguments, and exchange data between MATLAB and .NET programs.

---
## Requirements
### Required MathWorks Products
* MATLAB release R2022b or later

### Supported Versions of .NET
For version information, see [MATLAB Interfaces to Other Languages](https://www.mathworks.com/support/requirements/language-interfaces.html). Install both the .NET SDK and the .NET Runtime from https://dotnet.microsoft.com/download.

---
## Install
MATLAB Engine API for .NET is included with your MATLAB install under `<matlabroot>/extern/dotnet/netstandard2.0`. The folder contains two libraries:
* MathWorks.MATLAB.Types.dll
* MathWorks.MATLAB.Engine.dll

Both libraries must be referenced to use MATLAB Engine API for .NET.

---
## Run-Time Environment
To run your application, set one of these environment variables to the specified path.
| OS | Variable | Path |
| --- | --- | --- |
| Windows&reg; | PATH | *matlabroot*\extern\bin\win64 |
| macOS with Apple silicon | DYLD_LIBRARY_PATH | *matlabroot*/extern/bin/maca64 |
| macOS with Intel&reg; | DYLD_LIBRARY_PATH | *matlabroot*/extern/bin/maci64 |
| Linux&reg; | LD_LIBRARY_PATH | *matlabroot*/extern/bin/glnxa64:*matlabroot*/sys/os/glnxa64 |

---
## Getting Started
You can use the .NET CLI to create a project from the command line:
```Shell
> dotnet new console --name MyApp
```

In your IDE, add references to `MathWorks.MATLAB.Types.dll` and `MathWorks.MATLAB.Engine.dll`. Alternatively, edit the `MyApp.csproj` file to contain the following:
<details>
<summary>MyApp.csproj</summary>
  
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <!-- Enables interop between .NET and MATLAB -->
    <Reference Include="MathWorks.MATLAB.Types" >
      <HintPath>$(matlabroot)/extern/dotnet/netstandard2.0/MathWorks.MATLAB.Types.dll</HintPath>
    </Reference>
    
    <!-- Provides an interface to MATLAB Engine API -->
    <Reference Include="MathWorks.MATLAB.Engine" >
      <HintPath>$(matlabroot)/extern/dotnet/netstandard2.0/MathWorks.MATLAB.Engine.dll</HintPath>
    </Reference>
    
    <!-- Enables using the 'dynamic' keyword -->
    <PackageReference Include="Microsoft.CSharp" Version="4.7.0" />
  </ItemGroup>
</Project>
```

</details>


This C# code will test if MATLAB Engine API for .NET is properly configured. It uses top-level statements introduced in C# 9.

```csharp
using System;
using MathWorks.MATLAB.Engine;
using MathWorks.MATLAB.Types;

using dynamic matlab = MATLABEngine.StartMATLAB();
matlab.disp(new RunOptions(nargout: 0), "Hello, .NET!");
```

Running the code should display the following:
```
Hello, .NET!
```

---
Copyright &copy; 2025 MathWorks, Inc. All rights reserved.
