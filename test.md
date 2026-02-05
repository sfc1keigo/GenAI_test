{\rtf1\ansi\ansicpg1252\cocoartf2822
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 # DB\uc0\u35373 \u35336 \u26360 \
\
- [\uc0\u12487 \u12540 \u12479 \u12505 \u12540 \u12473 \u24773 \u22577 ](#\u12487 \u12540 \u12479 \u12505 \u12540 \u12473 \u24773 \u22577 )\
- [\uc0\u12486 \u12540 \u12502 \u12523 \u23450 \u32681 ](#\u12486 \u12540 \u12502 \u12523 \u23450 \u32681 )\
  - [\uc0\u12518 \u12540 \u12470 \u12540 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 ](#\u12518 \u12540 \u12470 \u12540 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 )\
  - [\uc0\u23478 \u35336 \u31807 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 ](#\u23478 \u35336 \u31807 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 )\
- [ER \uc0\u22259 ](#er-\u22259 )\
\
# \uc0\u12487 \u12540 \u12479 \u12505 \u12540 \u12473 \u24773 \u22577 \
\
- **DB \uc0\u35542 \u29702 \u21517 **: \u23478 \u35336 \u31807 \u12487 \u12540 \u12479 \u12505 \u12540 \u12473 \
- **DB \uc0\u29289 \u29702 \u21517 **: kakeibo_db\
- **\uc0\u12507 \u12473 \u12488 \u21517 ** : kakeibo_db_host\
- **RDBMS \uc0\u12398 \u31278 \u39006 \u12392 \u12496 \u12540 \u12472 \u12519 \u12531 **: PostgreSQL 13\
\
# \uc0\u12486 \u12540 \u12502 \u12523 \u23450 \u32681 \
\
## \uc0\u12518 \u12540 \u12470 \u12540 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 \
\
- **\uc0\u35542 \u29702 \u21517 **: \u12518 \u12540 \u12470 \u12540 \u24773 \u22577 \
- **\uc0\u29289 \u29702 \u21517 **: users\
\
| \uc0\u12459 \u12521 \u12512 \u29289 \u29702 \u21517  | \u12459 \u12521 \u12512 \u35542 \u29702 \u21517    | \u12487 \u12540 \u12479 \u22411   | \u20961 \u20363                         | FK  | PK  | \u12518 \u12491 \u12540 \u12463 \u21046 \u32004  |\
| ------------ | -------------- | --------- | --------------------------- | --- | --- | ------------ |\
| user_id      | \uc0\u12518 \u12540 \u12470 \u12540  ID    | SERIAL    | 1                           |     | \u9675    | \u9675             |\
| username     | \uc0\u12518 \u12540 \u12470 \u12540 \u21517      | VARCHAR   | \u24773 \u22577 \u22826 \u37070                     |     |     | \u9675             |\
| email        | \uc0\u12513 \u12540 \u12523 \u12450 \u12489 \u12524 \u12473  | VARCHAR   | info_taro@example.dummy |     |     | \u9675             |\
| created_at   | \uc0\u20316 \u25104 \u26085 \u26178        | TIMESTAMP | 2023-01-01 00:00:00         |     |     |              |\
\
## \uc0\u23478 \u35336 \u31807 \u24773 \u22577 \u12486 \u12540 \u12502 \u12523 \
\
- **\uc0\u35542 \u29702 \u21517 **: \u23478 \u35336 \u31807 \u24773 \u22577 \
- **\uc0\u29289 \u29702 \u21517 **: kakeibo\
\
| \uc0\u12459 \u12521 \u12512 \u29289 \u29702 \u21517  | \u12459 \u12521 \u12512 \u35542 \u29702 \u21517  | \u12487 \u12540 \u12479 \u22411   | \u20961 \u20363                 | FK  | PK  | \u12518 \u12491 \u12540 \u12463 \u21046 \u32004  |\
| ------------ | ------------ | --------- | ------------------- | --- | --- | ------------ |\
| record_id    | \uc0\u35352 \u37682  ID      | SERIAL    | 1001                |     | \u9675    | \u9675             |\
| user_id      | \uc0\u12518 \u12540 \u12470 \u12540  ID  | INTEGER   | 1                   | \u9675    |     |              |\
| date         | \uc0\u26085 \u20184          | DATE      | 2023-10-01          |     |     |              |\
| type         | \uc0\u21454 \u20837 \u12539 \u25903 \u20986    | VARCHAR   | income              |     |     |              |\
| category     | \uc0\u12459 \u12486 \u12468 \u12522      | VARCHAR   | salary              |     |     |              |\
| amount       | \uc0\u37329 \u38989          | INTEGER   | 1000                |     |     |              |\
\
# ER \uc0\u22259 \
\
```mermaid\
erDiagram\
    USERS \{\
        SERIAL user_id PK\
        VARCHAR username\
        VARCHAR email\
        TIMESTAMP created_at\
    \}\
    KAKEIBO \{\
        SERIAL record_id PK\
        INTEGER user_id FK\
        DATE date\
        VARCHAR type\
        VARCHAR category\
        INTEGER amount\
    \}\
    USERS ||--o\{ KAKEIBO : "has"\
```\
\
}