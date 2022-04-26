# mermaidTest

## ERD
``` mermaid
erDiagram
    MOVIE ||--o{ MOVIE_TIMES : ""
    MOVIE {
        id movie_id PK "영화 ID"
        string title "영화제목"
        int running_time "러닝타임"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    THEATER ||--o{ MOVIE_TIMES : ""
    THEATER ||--|{ SEAT : ""
    THEATER {
        id theater_id PK "상영관 ID"
        int theater_number "상영관 번호"
        int seat_count "좌석수"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    SEAT ||--o{ TICKET : ""
    SEAT {
        id seat_id PK "좌석 ID"
        id theater_id FK "상영관 ID"
        int column "열"
        int row "행"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    MOVIE_TIMES ||--o{ TICKET : ""
    MOVIE_TIMES {
        id movie_times_id PK "상영시간표 ID"
        id movie_id FK "영화 ID"
        id theater_id FK "상영관 ID"
        date date "상영 날짜"
        string round "회차"
        time start_time "시작 시간"
        time end_time "종료 시간"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    TICKET {
        id ticket_id PK "티켓 ID"
        id seat_id FK "좌석 ID"
        id movie_times_id FK "상영시간표 ID"
        string ticket_number "티켓 번호"
        string ticket_status "상태 - 구매가능/예약진행중/판매완료"
        int price "가격"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    TICKET_PAYMENT_MAP }|--|| TICKET : ""
    TICKET_PAYMENT_MAP }|--|| PAYMENT : ""
    TICKET_PAYMENT_MAP {
        id ticket_payment_map_id PK "티켓 결제 맵핑 ID"
        id ticket_id FK "티켓 ID"
        id payment_id FK "결제 ID"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    PAYMENT {
        id payment_id PK "결제 ID"
        id user_id FK "유저ID"
        string type "결제 타입 - 예) 네이버페이, 카카오페이"
        string payment_status "상태 - 완료/환불"
        string price "결제 금액"
        datetime created_dt "결제일시"
        datetime updated_dt "수정일시"
    }
    USER ||--o{ PAYMENT : ""
    USER {
        id user_id "회원"
        string password "비밀번호"
        string grade "등급 - 고객/임직원"
        string email "이메일"
        string phone "휴대폰 번호"
        boolean is_withdraw "탈퇴여부"
        datetime withdraw_dt "탈퇴일시"
        datetime created_dt "가입일시"
        datetime updated_dt "수정일시"
    }
```

### 이후 생각해야 하는 것들
- 쿠폰
- 영화정보 디테일(ex - 배급사, 나라, 분류 ...)
- 좌석 별 금액 다른 상황
