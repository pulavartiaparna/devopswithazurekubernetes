FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["Newprojfordevopsaks.csproj", "Newprojfordevopsaks/"]

RUN dotnet restore Newprojfordevopsaks/Newprojfordevopsaks.csproj
COPY . .
WORKDIR "/src"
RUN dotnet build "Newprojfordevopsaks.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Newprojfordevopsaks.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Newprojfordevopsaks.dll"]