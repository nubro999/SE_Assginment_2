classDiagram
    %% 사용자(액터)
    class User
    class Member
    class Admin

    %% UI 및 서비스 계층
    class RegisterUI
    class RegisterService
    class LoginForm
    class AuthService
    class BicycleRegisterUI
    class BicycleService
    class BicycleListUI
    class RentalInfoUI

    %% 도메인 객체
    class Bicycle
    class Rental

    %% 관계 정의
    User <|-- Member
    User <|-- Admin

    %% 회원가입
    User --> RegisterUI : 회원가입 요청
    RegisterUI --> RegisterService : 가입 요청 전달
    RegisterService --> Member : 회원 등록

    %% 로그인/로그아웃
    User --> LoginForm : 로그인/로그아웃 요청
    LoginForm --> AuthService : 인증 요청
    AuthService --> User : 인증결과 반환

    %% 자전거 등록
    User --> BicycleRegisterUI : 자전거 등록 요청
    BicycleRegisterUI --> BicycleService : 등록 요청 전달
    BicycleService --> Bicycle : 자전거 등록

    %% 자전거 대여
    Admin --> BicycleListUI : 자전거 목록 요청
    BicycleListUI --> Bicycle : 자전거 목록 조회
    Admin --> Bicycle : 대여 요청

    %% 대여 정보 조회
    Member --> RentalInfoUI : 대여 정보 조회
    RentalInfoUI --> Rental : 대여 정보 조회

    %% 대여 관계 (Member와 Rental)
    Member "1" -- "0..*" Rental : rents >
    Bicycle "1" -- "0..*" Rental : isRentedIn >
