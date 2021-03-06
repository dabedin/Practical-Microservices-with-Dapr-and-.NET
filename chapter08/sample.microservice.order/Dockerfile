FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

COPY ["sample.microservice.common/sample.microservice.common.csproj", "sample.microservice.common/"]
COPY ["sample.microservice.dto.shipping/sample.microservice.dto.shipping.csproj", "sample.microservice.dto.shipping/"]
COPY ["sample.microservice.dto.customization/sample.microservice.dto.customization.csproj", "sample.microservice.dto.customization/"]
COPY ["sample.microservice.dto.reservation/sample.microservice.dto.reservation.csproj", "sample.microservice.dto.reservation/"]
COPY ["sample.microservice.dto.order/sample.microservice.dto.order.csproj", "sample.microservice.dto.order/"]
COPY ["sample.microservice.order/sample.microservice.order.csproj", "sample.microservice.order/"]
RUN dotnet restore "sample.microservice.common/sample.microservice.common.csproj"
RUN dotnet restore "sample.microservice.dto.shipping/sample.microservice.dto.shipping.csproj"
RUN dotnet restore "sample.microservice.dto.customization/sample.microservice.dto.customization.csproj"
RUN dotnet restore "sample.microservice.dto.reservation/sample.microservice.dto.reservation.csproj"
RUN dotnet restore "sample.microservice.dto.order/sample.microservice.dto.order.csproj"
RUN dotnet restore "sample.microservice.order/sample.microservice.order.csproj"
COPY . .
WORKDIR "/src/sample.microservice.order"
RUN dotnet publish "sample.microservice.order.csproj" -c Release -o /app/publish --no-restore

ARG BUILD_DATE
ARG BUILD_VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.version=$BUILD_VERSION
LABEL org.label-schema.description="Practical Microservices with Dapr and .NET sample, Order microservice"

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "sample.microservice.order.dll"]
