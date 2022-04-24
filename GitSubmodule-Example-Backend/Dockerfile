FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["GitSubmodule-Example-Backend/GitSubmodule-Example-Backend.csproj", "GitSubmodule-Example-Backend/"]
RUN dotnet restore "GitSubmodule-Example-Backend/GitSubmodule-Example-Backend.csproj"
COPY . .
WORKDIR "/src/GitSubmodule-Example-Backend"
RUN dotnet build "GitSubmodule-Example-Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GitSubmodule-Example-Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GitSubmodule-Example-Backend.dll"]
