FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Mentor/Mentor.csproj", "Mentor/"]
RUN dotnet restore "Mentor/Mentor.csproj"
COPY . .
WORKDIR "/src/Mentor"
RUN dotnet build "Mentor.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Mentor.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Mentor.dll"]