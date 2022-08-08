FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY backend.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c release -o /app

#Ele executará as seguintes etapas sequencialmente quando invocado:

#   - Efetue pull da imagem mcr.microsoft.com/dotnet/sdk:6.0 e dê a ela o nome build
#   - Defina o diretório de trabalho dentro da imagem como /src
#   - Copie o arquivo chamado backend.csproj encontrado localmente para o diretório /src recém-criado
#   - Chama dotnet restore no projeto
#   - Copie tudo do diretório de trabalho local para a imagem
#   - Chama dotnet publish no projeto


FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT ["dotnet", "backend.dll"]

#Ele executará as seguintes etapas sequencialmente quando invocado:

#   - Efetue pull da imagem mcr.microsoft.com/dotnet/aspnet:6.0
#   - Defina o diretório de trabalho dentro da imagem como /app
#   - Expõe as portas 80 e 443
#   - Copie tudo do diretório /app da imagem de build criada acima para o diretório raiz dessa imagem
#   - Defina o ponto de entrada dessa imagem como dotnet e transmita backend.dll como um argumento