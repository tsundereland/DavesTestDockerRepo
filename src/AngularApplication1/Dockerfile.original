#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443



FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y nodejs \
    npm                       # note this one

RUN file="$(ls)" && echo $file
COPY ["AngularApplication1/AngularApplication1.csproj", "AngularApplication1/"]
#RUN dotnet restore "AngularApplication1/AngularApplication1.csproj"
#COPY . .
#WORKDIR "/src/AngularApplication1"
#RUN dotnet build "AngularApplication1.csproj" -c Release -o /app/build

#FROM build AS publish
#RUN dotnet publish "AngularApplication1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AngularApplication1.dll"]