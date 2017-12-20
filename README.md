# Cotizaciones

* dotnet new mvc -o Cotizaciones
* dotnet add package Microsoft.EntityFrameworkCore.Design --version 2.0.1
* dotnet add package Microsoft.Extensions.Logging --version 2.0.0
* dotnet add package Microsoft.Extensions.Logging.Abstractions --version 2.0.0

* Add in file: Cotizaciones.csproj:

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.1" />
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
</ItemGroup>
```
