###데이터베이스 MariaDB - 초안/언제든지 수정될 수 있음
```sql
###테이블
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  login_id varchar(20),
  login_password varchar(50),
  personal_id INTEGER,
  company_id integer
);


CREATE TABLE company (
  company_id INTEGER PRIMARY KEY,
  company_name varchar(20),
  company_category integer
);


CREATE TABLE personal (
  personal_id INTEGER PRIMARY KEY,
  personal_name varchar(20),
  personal_category integer
);


CREATE TABLE personal_detail (
  personal_detail_id INTEGER PRIMARY KEY,
  personal_id integer,
  personal_number integer,
  personal_email varchar(50),
  personal_phonenumber integer,
  location varchar(50)
);


CREATE TABLE company_detail (
  company_detail_id INTEGER PRIMARY KEY,
  company_id integer,
  company_email varchar(50),
  company_number integer,
  company_phonenumber integer,
  location varchar(50)
);


CREATE TABLE resumes (
  resume_id INTEGER PRIMARY KEY,
  personal_id integer,
  picture longtext,
  introduce longtext
);


CREATE TABLE personal_board (
  personal_board_id INTEGER PRIMARY KEY,
  personal_id integer,
  board_title varchar(50),
  board_content longtext
);

CREATE TABLE company_board (
  personal_board_id INTEGER PRIMARY KEY,
  company_id integer,
  board_title varchar(50),
  board_content longtext
);


CREATE TABLE subscirbe (
  subcirbe_id INTEGER PRIMARY KEY,
  company_id integer,
  personal_id integer
);

CREATE TABLE likes (
  like_id INTEGER PRIMARY KEY,
  personal_id integer,
  company_id integer
);


CREATE TABLE category (
  category_id INTEGER PRIMARY KEY,
  frontend tinyint,
  backend tinyint,
  devops tinyint,
  etc varchar(50)
);
```

### 관계설정
```sql
ALTER TABLE users ADD FOREIGN KEY (personal_id) REFERENCES personal(personal_id);
ALTER TABLE personal_detail ADD FOREIGN KEY (personal_id) REFERENCES personal (personal_id);
ALTER TABLE users ADD FOREIGN KEY (company_id) REFERENCES company (company_id);
ALTER TABLE resumes ADD FOREIGN KEY (personal_id) REFERENCES personal (personal_id);
ALTER TABLE company_detail ADD FOREIGN KEY (company_id) REFERENCES company (company_id);
ALTER TABLE likes ADD FOREIGN KEY (company_id) REFERENCES company (company_id);
ALTER TABLE likes ADD FOREIGN KEY (personal_id) REFERENCES personal (personal_id);
ALTER TABLE company_board ADD FOREIGN KEY (company_id) REFERENCES company (company_id);
ALTER TABLE personal_board ADD FOREIGN KEY (personal_id) REFERENCES personal (personal_id);
ALTER TABLE subscirbe ADD FOREIGN KEY (company_id) REFERENCES company (company_id);
ALTER TABLE subscirbe ADD FOREIGN KEY (personal_id) REFERENCES personal (personal_id);
ALTER TABLE personal ADD FOREIGN KEY (personal_category) REFERENCES category (category_id);
ALTER TABLE company ADD FOREIGN KEY (company_category) REFERENCES category (category_id);
```
