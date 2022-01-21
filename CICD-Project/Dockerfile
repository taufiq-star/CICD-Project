#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["./CICD-Project.csproj", "CICD-Project/"]
RUN dotnet restore "CICD-Project/CICD-Project.csproj"
COPY . .
WORKDIR src
RUN dotnet build "CICD-Project/CICD-Project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CICD-Project/CICD-Project.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICD-Project.dll"]
