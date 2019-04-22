FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 9002

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["ProductsAPIServices/ProductsAPIServices.csproj", "ProductsAPIServices/"]
RUN dotnet restore "ProductsAPIServices/ProductsAPIServices.csproj"
COPY . .
WORKDIR "/src/ProductsAPIServices"
RUN dotnet build "ProductsAPIServices.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProductsAPIServices.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProductsAPIServices.dll"]