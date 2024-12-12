:::mermaid
    flowchart TB   

    %%Connections

    POSTerminals --> ApiGateway
    WebApp --> ApiGateway
    MobileApp --> ApiGateway

    ApiGateway --> TenantResolver

    TenantResolver --> AnalyticsService
    TenantResolver --> PaymentService
    TenantResolver --> OrderService
    TenantResolver --> AuthService
    TenantResolver --> MenuService

    AnalyticsService --> MainDatabase
    PaymentService --> MainDatabase
    OrderService --> MainDatabase
    AuthService --> MainDatabase
    MenuService --> MainDatabase

    OrderService --> RedisCache
    MenuService --> RedisCache
    MenuService --> FileStorage

    %% ----------------------------------------------
    subgraph Client Layer

    POSTerminals[Pos Terminals]

    WebApp[Web Application 
        -Management Portal-]

    MobileApp[Mobile App 
        -Staff and customers-]

    end

    %% ----------------------------------------------
    subgraph API Gateway 

    ApiGateway[API Gateway
        - Authentication
        - Rate Limiting
        - Routing]

    TenantResolver[Tenant Resolver
        - Tenant Identification
        - Route Distribuition]

    end

    %% ----------------------------------------------
    subgraph Core Services 

    AnalyticsService[Analytcs Service
        -Reporting
        -insights
        -Metrics]

    PaymentService[Payment Service
        -Processing
        -Invoicing
        -Splits]

    OrderService[Order Service
        -Order Management
        -Kitchen Display
        -Status Tracking]

    AuthService[Auth Service
        -JWT
        -Role Management
        -SSO]

    MenuService[Menu Service
        -Digital Menus
        -Categories
        -Pricing]
    end

    %% ----------------------------------------------
    subgraph Data Layer 

    MainDatabase[(Main Database
        w/Tenant Schemas)]

    RedisCache[(Redis cache
        -Session
        -Menu Cache)]

    FileStorage[(File Storage
        -Images
        -Documents)]
    end
:::