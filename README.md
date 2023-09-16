graph TD

    subgraph Frontend [React Web Apps]
        PatientApp(환자용 웹앱) --> APIGateway
        AdminApp(병원 관리자용 웹앱) --> APIGateway
    end

    subgraph Backend [Spring Boot Services]
        AuthService(인증 서비스)
        PatientService(환자 관리 서비스)
        DoctorService(의사 관리 서비스)
        ReservationService(예약 관리 서비스)
        NotificationService(알림 서비스)
    end

    subgraph APIGateway[Nest.js API Gateway]
        Gate1(라우터) --> AuthService
        Gate2(라우터) --> PatientService
        Gate3(라우터) --> DoctorService
        Gate4(라우터) --> ReservationService
    end

    ReservationService --> RabbitMQ[메시징 서비스 (RabbitMQ)]
    RabbitMQ --> NotificationService

    Database[데이터베이스] --- AuthService
    Database --- PatientService
    Database --- DoctorService
    Database --- ReservationService

    subgraph Messaging
        RabbitMQ
    end

