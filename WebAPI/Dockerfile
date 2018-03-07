FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
LABEL version="1.0" description="My Test"
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
RUN pwd
COPY *.sln ./
COPY WebAPI/WebAPI.csproj WebAPI/
RUN dotnet restore
COPY . .
WORKDIR /src/WebAPI
CMD "echo" "building the container"
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebAPI.dll"]
