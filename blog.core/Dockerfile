#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["blog.core/blog.core.csproj", "blog.core/"]
RUN dotnet restore "blog.core/blog.core.csproj"
COPY . .
WORKDIR "/src/blog.core"
RUN dotnet build "blog.core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "blog.core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "blog.core.dll","-b","0.0.0.0"]