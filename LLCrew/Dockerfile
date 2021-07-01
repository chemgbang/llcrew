#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
ENV TZ Asia/Shanghai
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["LLCrew/LLCrew.csproj", "LLCrew/"]
RUN dotnet restore "LLCrew/LLCrew.csproj"
COPY . .
WORKDIR "/src/LLCrew"
RUN dotnet build "LLCrew.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LLCrew.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LLCrew.dll"]