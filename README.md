## Requisitos
 * .NET 6

## Execução Local
Execute o seguinte comando para execução local:
```
dotnet restore
dotnet run --project aspnet-demo-api
```

## Execução em container
Existe a possibilidade de executar o projeto no Visual Studio através do Dockerfile contido em [**aspnet-demo-api/Dockerfile**](./aspnet-demo-api//Dockerfile).

Também existe outro Dockerfile destinado ao CI que se encontra na pasta raiz do repositório, o mesmo espera que o projeto já tenha sido compilado previamente ( ponto este que difere do Dockerfile contido em [**aspnet-demo-api/Dockerfile**](./aspnet-demo-api//Dockerfile)).

Para utilizar o segundo Dockerfile manualmente execute os seguintes comandos para realizar o build do container final da aplicação:
```
dotnet restore
dotnet build "aspnet-demo-api/aspnet-demo-api.csproj" -c Release -o ./app/build
dotnet publish "aspnet-demo-api/aspnet-demo-api.csproj" -c Release -o ./app/publish /p:UseAppHost=false
docker build -t aspnet-demo-api:latest .
docker run --rm -it -p 8080:8080 aspnet-demo-api:latest
```

## Execução em produção
Para executar em produção execute os seguintes comandos:
```
dotnet restore
dotnet build "aspnet-demo-api/aspnet-demo-api.csproj" -c Release -o ./app/build
dotnet publish "aspnet-demo-api/aspnet-demo-api.csproj" -c Release -o ./app/publish /p:UseAppHost=false
dotnet ./app/publish/aspnet-demo-api.dll
```