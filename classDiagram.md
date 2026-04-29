```mermaid

classDiagram
    %% 사용자 클래스
    class User {
        %% UML 표기법: 가시성 속성명: 타입
        -id: String
        -pw: String
        -name: String
        -phone: String
        -address: String
        
        %% 정적(Static) 메서드 ($ 기호 사용)
        %% UML 표기법: 가시성 메서드명(매개변수명: 타입): 반환타입
        +registerUser(id: String, pw: String, name: String, phone: String, address: String) void$
        +updateUser(id: String, pw: String, name: String, phone: String, address: String) void$
        +deleteUser(id: String) boolean$
        +searchUser(id: String) boolean$
    }

    %% 계좌 클래스
    class Account {
        -number: String
        -balance: double
        
        +deposit(id: String, amount: double) double
        +withdraw(id: String, amount: double) double
        +transfer(id: String, amount: double, toAccountNumber: String) double
        +computeBalance(id: String) double
    }

    User "1" <-- "1..*" Account : 사용조회