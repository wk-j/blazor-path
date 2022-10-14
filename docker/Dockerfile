FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine as build

WORKDIR /app

COPY src/MyWeb/MyWeb.csproj src/MyWeb/

RUN dotnet restore src/MyWeb

COPY src/MyWeb src/MyWeb

RUN dotnet publish src/MyWeb \
    -r linux-musl-x64 \
    -c Release \
    -o /out

# runtime
FROM mcr.microsoft.com/dotnet/runtime:6.0-alpine
ENV TZ='Asia/Bangkok'
RUN apk add --no-cache tzdata
WORKDIR /app
COPY --from=build /out .
CMD dotnet MyWeb.dll
EXPOSE 80