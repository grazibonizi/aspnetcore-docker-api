FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY AspNetCore.Docker.API.sln ./
COPY AspNetCore.Docker.API/AspNetCore.Docker.API.csproj AspNetCore.Docker.API/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/AspNetCore.Docker.API
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN dotnet publish --no-restore -c Release -o /app

FROM microsoft/aspnetcore:2.0 AS final
WORKDIR /app
EXPOSE 8080
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCore.Docker.API.dll"]
