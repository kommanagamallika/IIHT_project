FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["User/User.csproj", "User/"]
RUN dotnet restore "User/User.csproj"
COPY . .
WORKDIR "/src/User"
RUN dotnet build "User.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "User.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "User.dll"]