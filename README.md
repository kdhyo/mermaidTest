# mermaidTest

## ERD
``` mermaid
erDiagram
    MOVIE ||--o{ MOVIE-TIMES : ""
    MOVIE {
        id id PK "영화"
        string title "영화제목"
        int runningTime "러닝타임"
    }
    THEATER ||--o{ MOVIE-TIMES : ""
    THEATER ||--|{ SEAT : ""
    THEATER {
        id id PK "상영관"
        int theaterNumber "상영관 번호"
        int seatCount "좌석수"
    }
    SEAT ||--o{ TICKET : ""
    SEAT {
        id id PK "좌석"
        id theaterId FK "상영관 ID"
        int column "열"
        int row "행"
    }
    MOVIE-TIMES ||--o{ TICKET : ""
    MOVIE-TIMES {
        id id PK "상영시간표"
        id movieId FK "영화 ID"
        id theaterId FK "상영관 ID"
        date date "상영 날짜"
        string round "회차"
        time startTime "시작 시간"
        time endTime "종료 시간"
    }
    TICKET {
        id id PK "티켓"
        id seatId FK "좌석 ID"
        id movieTimesId FK "상영시간표 ID"
        string ticketNumber "티켓 번호"
        string state "상태 - 구매가능/예약진행중/판매완료"
        int price "가격"
    }
    TICKET_PAYMENT_MAP }|--|| TICKET : ""
    TICKET_PAYMENT_MAP }|--|| PAYMENT : ""
    TICKET_PAYMENT_MAP {
        id id PK "티켓 결제 맵핑테이블"
        id ticketId FK "티켓 ID"
        id paymentId FK "결제 ID"
    }
    PAYMENT {
        id id PK "결제"
        id userId FK "유저ID"
        string type "결제 타입 - 예) 네이버페이, 카카오페이"
        string state "상태 - 완료/환불"
        string price "결제 금액"
        datetime regDt "결제일시"
    }
    USER ||--o{ PAYMENT : ""
    USER {
        id id "회원"
        string password "비밀번호"
        string grade "등급 - 고객/임직원"
        string email "이메일"
        string phone "휴대폰 번호"
        datetime regDt "가입일시"
        datetime modDt "수정일시"
        boolean isWithdraw "탈퇴여부"
        datetime withdrawDt "탈퇴일시"
    }
```
