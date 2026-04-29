```mermaid

graph LR
    %% Actors
    Admin((관리자))
    Customer((은행 고객))
    BankDB[(은행 시스템 DB)]

    subgraph "온라인 뱅킹 시스템"
        %% Common Foundation Use Cases
        UC_Info(사용자 정보 조회)
        UC_Balance(잔액 조회)

        %% User Management (CRUD)
        UC_Reg(사용자 정보 등록)
        UC_Mod(사용자 정보 수정)
        UC_Del(사용자 정보 삭제)

        %% Financial Operations
        UC_Dep(입금)
        UC_With(출금)
        UC_Trans(계좌 이체)
    end

    %% 1. 등록/수정/삭제는 사용자 조회를 반드시 포함
    UC_Reg -.->|&lt;&lt;include&gt;&gt| UC_Info
    UC_Mod -.->|&lt;&lt;include&gt;&gt| UC_Info
    UC_Del -.->|&lt;&lt;include&gt;&gt| UC_Info

    %% 2 & 3. 금융 거래는 잔액조회 및 사용자 조회를 반드시 포함
    UC_Dep -.->|&lt;&lt;include&gt;&gt| UC_Balance
    UC_Dep -.->|&lt;&lt;include&gt;&gt| UC_Info
    
    UC_With -.->|&lt;&lt;include&gt;&gt| UC_Balance
    UC_With -.->|&lt;&lt;include&gt;&gt| UC_Info
    
    UC_Trans -.->|&lt;&lt;include&gt;&gt| UC_Balance
    UC_Trans -.->|&lt;&lt;include&gt;&gt| UC_Info

    %% 4. DB 연동 (금융 거래는 DB를 통해 확인/기록)
    UC_Dep --- BankDB
    UC_With --- BankDB
    UC_Trans --- BankDB
    UC_Balance --- BankDB
    UC_Info --- BankDB

    %% Actor Relationships
    Admin --> UC_Reg
    Admin --> UC_Mod
    Admin --> UC_Del

    Customer --> UC_Dep
    Customer --> UC_With
    Customer --> UC_Trans
    Customer --> UC_Balance

    %% Styling
    style BankDB fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style UC_Info fill:#fdfd96,stroke:#333
    style UC_Balance fill:#fdfd96,stroke:#333