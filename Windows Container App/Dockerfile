#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat 

FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY ["Windows Container App/*.csproj", "./Windows Container App/"]
COPY ["Windows Container App/*.config" ,"./Windows Container App/"]
RUN nuget restore

# copy everything else and build app
COPY ["Windows Container App/.", "./Windows Container App/"]
WORKDIR "/app/Windows Container App"
RUN msbuild /p:Configuration=Release -r:False


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.7.2-windowsservercore-ltsc2019 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build ["/app/Windows Container App/.", "./"]
