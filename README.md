# mermaidTest

## ERD
``` mermaid
erDiagram
    MOVIE ||--o{ MOVIE_TIMES : ""
    MOVIE {
        bigint movie_id PK "영화 ID"
        varchar title "영화제목"
        int running_time "러닝타임"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    THEATER ||--o{ MOVIE_TIMES : ""
    THEATER ||--|{ SEAT : ""
    THEATER {
        bigint theater_id PK "상영관 ID"
        int theater_number "상영관 번호"
        int seat_count "좌석수"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    SEAT ||--o{ TICKET : ""
    SEAT {
        bigint seat_id PK "좌석 ID"
        bigint theater_id FK "상영관 ID"
        int column "열"
        int row "행"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    MOVIE_TIMES ||--o{ TICKET : ""
    MOVIE_TIMES {
        bigint movie_times_id PK "상영시간표 ID"
        bigint movie_id FK "영화 ID"
        bigint theater_id FK "상영관 ID"
        date date "상영 날짜"
        int round "회차"
        time start_time "시작 시간"
        time end_time "종료 시간"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    TICKET {
        bigint ticket_id PK "티켓 ID"
        bigint seat_id FK "좌석 ID"
        bigint movie_times_id FK "상영시간표 ID"
        bigint payment_id FK "결제 ID"
        varchar ticket_status "상태 - 구매가능/예약진행중/판매완료"
        int ticket_price "가격"
        datetime created_dt "등록일시"
        datetime updated_dt "수정일시"
    }
    TICKET }|--|| PAYMENT : ""
    PAYMENT {
        bigint payment_id PK "결제 ID"
        bigint user_id FK "유저ID"
        varchar type "결제 타입 - 예) 네이버페이, 카카오페이"
        varchar payment_status "상태 - 완료/환불/실패"
        varchar failed_reason "실패사유 - 컬럼명을 알아보기 쉬운가?"
        varchar payment_number "예매번호"
        int total_price "결제 금액"
        datetime created_dt "결제일시"
        datetime updated_dt "수정일시"
    }
    USER ||--o{ PAYMENT : ""
    USER {
        bigint user_id "회원"
        varchar password "비밀번호"
        varchar grade "등급 - 고객/임직원"
        varchar email "이메일"
        varchar phone "휴대폰 번호"
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
