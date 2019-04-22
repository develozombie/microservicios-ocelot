FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 9001

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["CustomersAPIServices/CustomersAPIServices.csproj", "CustomersAPIServices/"]
RUN dotnet restore "CustomersAPIServices/CustomersAPIServices.csproj"
COPY . .
WORKDIR "/src/CustomersAPIServices"
RUN dotnet build "CustomersAPIServices.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CustomersAPIServices.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CustomersAPIServices.dll"]