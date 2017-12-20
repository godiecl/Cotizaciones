# Cotizaciones

## Creación de Proyecto

```bash
dotnet new mvc -o Cotizaciones
```

## Agregar Dependencias

```bash
dotnet add package Microsoft.EntityFrameworkCore.Design --version 2.0.1
dotnet add package Microsoft.Extensions.Logging --version 2.0.0
dotnet add package Microsoft.Extensions.Logging.Abstractions --version 2.0.0
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Desig --version 2.0.1
```

## Agregar Dependencias de tooling: Cotizaciones.csproj

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.1" />
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
</ItemGroup>
```

## Crear clase Clase Persona

```csharp
/// <summary>
/// Archivo donde se definen las clases del Dominio del problema.
/// </summary>
namespace Cotizaciones.Models {

    /// <summary>
    /// Clase que representa a una persona en el Sistema.
    /// </summary>
    /// <remarks>
    /// Esta clase pertenece al modelo del Dominio y posee las siguientes restricciones:
    /// - No permite valores null en sus atributos.
    /// </remarks>
    public class Persona
    {
        public int Id { get; set; }

        public string Rut { get; set; }

        public string Nombre { get; set; }

        public string Paterno { get; set; }

        public string Materno { get; set; }

    }
}
```

## Crear Contexto (ORM)

```csharp
using Microsoft.EntityFrameworkCore;
using Cotizaciones.Models;

namespace Cotizaciones.Data {
    public class CotizacionesContext : DbContext
    {
        public CotizacionesContext(DbContextOptions<CotizacionesContext> options) : base(options)
        {
        }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            // Utilizacion de SQLite como backend
            optionsBuilder.UseSqlite("Data Source=cotizaciones.db");
        }

        public DbSet<Persona> Personas { get; set; }

    }
}
```

## Agregar en el archivo Startup.cs

```csharp
        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
            services.AddDbContext<CotizacionesContext>();
        }
```

## Creacion de la base de datos via ORM EntityFramework

```bash
dotnet ef migrations add InitialCreate --verbose
dotnet ef database update --verbose
```

## Creacion del Controller de Personas

```bash
dotnet aspnet-codegenerator controller --controllerName PersonaController --model Persona --dataContext CotizacionesContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries
```