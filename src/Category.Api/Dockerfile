	#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Category.Api/Category.Api.csproj", "src/Category.Api/"]
RUN dotnet restore "src/Category.Api/Category.Api.csproj"
COPY . .
WORKDIR "/src/src/Category.Api"



RUN dotnet build "Category.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Category.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
EXPOSE    5000
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Code.Category.Api.dll"]