# Estágio de compilação
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Copia o arquivo .csproj de dentro da subpasta local para dentro do container
COPY ["exemploApiKafka/exemploApiKafka.csproj", "exemploApiKafka/"]
RUN dotnet restore "exemploApiKafka/exemploApiKafka.csproj"

# Copia todo o restante dos arquivos do projeto
COPY . .

# Altera o diretório de trabalho para onde a build deve acontecer
WORKDIR "/src/exemploApiKafka"
RUN dotnet publish "exemploApiKafka.csproj" -c Release -o /app/publish /p:UseAppHost=false --no-restore

# Estágio de execução (Usando Runtime para ficar mais leve)
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "exemploApiKafka.dll"]
