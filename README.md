-- TB_GRADE 테이블 생성
CREATE TABLE TB_GRADE (
    GRADE_CODE VARCHAR2(10) PRIMARY KEY,
    GRADE_NAME VARCHAR2(20)
);

-- TB_AREA 테이블 생성
CREATE TABLE TB_AREA (
    AREA_CODE VARCHAR2(10) PRIMARY KEY,
    AREA_NAME VARCHAR2(20)
);

-- TB_MEMBER 테이블 생성
CREATE TABLE TB_MEMBER (
    MEMBERID VARCHAR2(20) PRIMARY KEY,
    MEMBERPWD VARCHAR2(20),
    MEMBER_NAME VARCHAR2(50),
    GRADE VARCHAR2(10),
    AREA_CODE VARCHAR2(10),
    FOREIGN KEY (GRADE) REFERENCES TB_GRADE(GRADE_CODE),
    FOREIGN KEY (AREA_CODE) REFERENCES TB_AREA(AREA_CODE)
);

-- 데이터 삽입
-- TB_GRADE 테이블 데이터 삽입
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('10', '일반회원');
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('20', '우수회원');
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('30', '특별회원');

-- TB_AREA 테이블 데이터 삽입
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('02', '서울');
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('031', '경기');
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('032', '인천');

-- TB_MEMBER 테이블 데이터 삽입
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('hong01', 'pass01', '홍길동', '10', '02');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('leess99', 'pass02', '이순신', '10', '032');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('SS50000', 'pass03', '신사임당', '30', '031');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('1u93', 'pass04', '아이유', '30', '02');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('pcs1234', 'pass05', '박철수', '20', '031');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('you_is', 'pass06', '유재석', '10', '02');
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('kyh9876', 'pass07', '김영희', '20', '031');


