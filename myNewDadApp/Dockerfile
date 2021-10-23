FROM mcr.microsoft.com/dotnet/aspnet:3.1-focal AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:3.1-focal AS build
WORKDIR /src
COPY ["myNewDadApp/myNewDadApp.csproj", "myNewDadApp/"]
RUN dotnet restore "myNewDadApp/myNewDadApp.csproj"
COPY . .
WORKDIR "/src/myNewDadApp"
RUN dotnet build "myNewDadApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myNewDadApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myNewDadApp.dll"]
