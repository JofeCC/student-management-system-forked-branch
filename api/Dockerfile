#  Build
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
# SDK => Software Developkment Kit

WORKDIR /src

ENV PATH="$PATH:/root/.dotnet/tools"

COPY *.csproj .

RUN dotnet restore 

COPY . .

# Run
RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 5123

ENTRYPOINT ["sh", "-c", "dotnet api.dll"]