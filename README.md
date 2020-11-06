**Context**

This is to reproduce error when adding gRPC to existing .NET core web service. The bug opened here : https://github.com/dotnet/AspNetCore.Docs/issues/20431.



The [document here](https://docs.microsoft.com/en-us/aspnet/core/grpc/browser?view=aspnetcore-3.1) suggests to add following line in *Startup.cs*

`app.UseGrpcWeb(new GrpcWebOptions { DefaultEnabled = true });`

However, `IApplicationBuilder` does not have this method or extension. Also in the GRPC project created using `dotnet new grpc`, this line is missing.



To check error: 

```bash
docker build .
# Startup.cs(46,32): error CS0246: The type or namespace name 'GrpcWebOptions' could not be found (are you missing a using directive or an assembly reference?) [/source/Service.csproj]
# Startup.cs(46,17): error CS1061: 'IApplicationBuilder' does not contain a definition for 'UseGrpcWeb' and no accessible extension method 'UseGrpcWeb' accepting a first argument of type 'IApplicationBuilder' could be found (are you missing a using directive or an assembly reference?) [/source/Service.csproj]
# The command '/bin/sh -c dotnet publish -c release -o /app --no-restore' returned a non-zero code: 1
```

