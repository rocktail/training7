#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-nanoserver-1809 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-nanoserver-1809 AS build
WORKDIR /src
COPY ["WebApplicationTraining7/WebApplicationTraining7.csproj", "WebApplicationTraining7/"]
RUN dotnet restore "WebApplicationTraining7/WebApplicationTraining7.csproj"
COPY . .
WORKDIR "/src/WebApplicationTraining7"
RUN dotnet build "WebApplicationTraining7.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplicationTraining7.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplicationTraining7.dll"]