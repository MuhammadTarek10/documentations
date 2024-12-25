# Notes

Making multiple project solution using dotnet cli

1. Create a new solution

```bash
dotnet new sln -n <solution-name>
```

2. Create a new project

```bash
dotnet new <project-type> -n <project-name>
```

for EG.

```bash
dotnet new mvc -n Lagoon.Web
```

3. Add the project to the solution

```bash
dotnet sln add <project-name>
```

4. Build the solution

```bash
dotnet build
```

- To run the project

```bash
dotnet run --project <project-filename>
```

- Add reference to the project

```bash
dotnet add <project-name> reference <project-filename>
```

for EG.

```bash
dotnet add Lagoon.Web reference Lagoon.Infrastructure/Lagoon.Infrastructure.csproj
```

- To remove reference

```bash
dotnet remove <project-name> reference <project-filename>
```

- To remove project from solution

```bash
dotnet sln remove <project-name>
```

- To add package to specefic project

```bash
dotnet add <project-filename> package <package-name>
```
