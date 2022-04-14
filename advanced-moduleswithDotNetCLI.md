## Installing the PowerShell Standard module template
If creating a new module, the recommendation is to use the .NET CLI.

```powershell
#install the module template
dotnet new -i Microsoft.PowerShell.Standard.Module.Template

#create a new module
mkdir myModule
cd myModule
dotnet new psmodule

#build the module
dotnet build

#test the module
Import-Module .\bin\Debug\netstandard2.0\myModule.dll
Test-SampleCmdlet -?
Test-SampleCmdlet -FavoriteNumber 7 -FavoritePet Cat


```