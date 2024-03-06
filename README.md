
sqlplus 관리자 권한으로 접속해서 <br/>
khk 라는 계정 생성<br/>
비밀번호 kh1234<br/>
<br/><br/>
ctrl + c = 명령어에서 하고있는 작업을 중단할 때 사용하는 단축키<br/>
exit = 현재 sql에서 컴퓨터로 돌아가고 싶을 때 사용하는 명령어<br/>
<br/><br/>
권한 명령어<br/>
grant  = 권한<br/>
connect = 사용자가 데이터베이스에 접속할 수 있는 권한, <br/>
resource = 데이터베이스에 생성하고 사용할 수 있는 권한, <br/>
dba = dbadmin 슈퍼권한<br/>
 to 아이디;<br/>
<br/><br/><br/>


create = 생성 <br/>
user = 생성하고자하는 목표<br/>
아이디명<br/>
identified by <br/>
비밀번호<br/>

alter = 수정<br/>
session<br/>
set = 수정하고자 하는 부분<br/>
"_oracle_script" = true;<br/>

<br/><br/>
sqlplus 접속<br/>
sys/oracle = oracle  사용자=관리자<br/>
as<br/>
<br/>
sysdba = 데이터베이스 생성과 삭제 권한<br/>
<br/><br/>
-- TB_GRADE 테이블 생성<br/>
CREATE TABLE TB_GRADE (
    GRADE_CODE VARCHAR2(10) PRIMARY KEY,
    GRADE_NAME VARCHAR2(20)
);
<br/><br/>
-- TB_AREA 테이블 생성
CREATE TABLE TB_AREA (
    AREA_CODE VARCHAR2(10) PRIMARY KEY,
    AREA_NAME VARCHAR2(20)
);
<br/><br/>
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
<br/><br/>
-- 데이터 삽입<br/>
-- TB_GRADE 테이블 데이터 삽입<br/>
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('10', '일반회원');<br/>
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('20', '우수회원');<br/>
INSERT INTO TB_GRADE (GRADE_CODE, GRADE_NAME) VALUES ('30', '특별회원');<br/>
<br/><br/>
-- TB_AREA 테이블 데이터 삽입
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('02', '서울');<br/>
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('031', '경기');<br/>
INSERT INTO TB_AREA (AREA_CODE, AREA_NAME) VALUES ('032', '인천');<br/>
<br/>
-- TB_MEMBER 테이블 데이터 삽입
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('hong01', 'pass01', '홍길동', '10', '02');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('leess99', 'pass02', '이순신', '10', '032');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('SS50000', 'pass03', '신사임당', '30', '031');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('1u93', 'pass04', '아이유', '30', '02');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('pcs1234', 'pass05', '박철수', '20', '031');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('you_is', 'pass06', '유재석', '10', '02');<br/>
INSERT INTO TB_MEMBER (MEMBERID, MEMBERPWD, MEMBER_NAME, GRADE, AREA_CODE) VALUES ('kyh9876', 'pass07', '김영희', '20', '031');<br/>

<br/><br/>

-- 모든 회원의 이름과 등급을 조회하기<br/>
SELECT MEMBER_NAME, GRADE_NAME<br/>
FROM TB_MEMBER m<br/>
JOIN TB_GRADE g ON m.GRADE = g.GRADE_CODE;<br/>
<br/><br/>
-- 등급이 일반회원인 회원을 조회<br/>
SELECT * FROM TB_MEMBER WHERE GRADE = '10';<br/>
<br/><br/>
-- 경기 지역에 거주하는 회원의 아이디와 이름을 조회하기<br/>
SELECT MEMBERID, MEMBER_NAME, AREA_CODE <br/>
FROM TB_MEMBER <br/>
WHERE AREA_CODE = '031';<br/>
<br/><br/>

-- select 문을 사용해서 회원의 이름만 조회할 것<br/>

-- 어디서 회원의 이름을 가져올 것인가!<br/>
-- -> TB_MEMBER 테이블에서 회원의 이름을 FROM을 사용해서 가져올 것<br/>
SELECT MEMBER_NAME<br/>
FROM TB_MEMBER <br/>
WHERE AREA_CODE = '20' AND MEMBER_NAME LIKE '%이%';<br/>
-- 등급이 우수회원이고 이름에 '이'가 포함되어야함<br/>
-- -> 어떻게 우수회원인지 확인하고<br/>
-- -> 이름에 이가 포함되는지는 어떻게 알 것인가 ?<br/>
-- -> MEMBER 테이블에서 우수회원은 20으로 적어놓음<br/>
-- -> '이' 라는 단어가 앞에 들어가는지 뒤에 들어가는지 <br/>
-- -> 상관없다면 '이'를 기준으로 앞 뒤에 %를 붙여 <br/>
-- -> 이가 포함되는 것을 확인<br/>

<br/><br/>
-- 등급이 '일반회원'인 회원의 이름을 알파벳 순으로 정렬해서 조회하기<br/>
SELECT MEMBER_NAME<br/>
FROM TB_MEMBER <br/>
WHERE GRADE =10<br/>
ORDER BY MEMBER_NAME;<br/>
-- 등급이 '특별회원'이고 이름에 '신'이 포함된 <br/>
-- 회원의 아이디와 이름 조회하기<br/>
SELECT MEMBERID, MEMBER_NAME<br/>
FROM TB_MEMBER <br/>
WHERE GRADE ='30' AND MEMBER_NAME LIKE '%신%';<br/>
<br/><br/>
-- '서울' 지역에 거주하고 '일반회원' 등급 회원의 이름조회<br/>
SELECT  MEMBER_NAME --회원의 이름만 보기<br/>
FROM TB_MEMBER m<br/>
JOIN TB_AREA a ON m.AREA_CODE  = a.AREA_CODE <br/>
JOIN TB_GRADE g ON m.GRADE = g.GRADE_CODE <br/>
WHERE a.AREA_code ='서울' AND g.GRADE_NAME = '일반회원';<br/>
<br/><br/>
-- 특정 지역의 회원 수 조회<br/>
SELECT AREA_NAME, COUNT(*)<br/>
FROM TB_MEMBER m<br/>
JOIN TB_AREA a ON m.AREA_CODE = a.AREA_CODE <br/>
GROUP BY AREA_NAME ;<br/>
<br/>
/*
hong01
 * */
--특정 hong01 회원의 지역 정보 조회<br/>
SELECT  MEMBER_NAME, AREA_NAME<br/>
FROM TB_MEMBER <br/>
JOIN TB_AREA ON TB_MEMBER.AREA_CODE  = TB_AREA.AREA_CODE <br/>
WHERE  MEMBERID  = 'hong01';<br/>
-- 일반회원과 우수회원 수 비교<br/>
SELECT GRADE, COUNT(*)<br/>
FROM TB_MEMBER<br/>
GROUP BY GRADE;<br/>
<br/><br/>
--SS50000 회원의 등급과 이름 조회<br/>
SELECT MEMBER_NAME, GRADE_NAME<br/>
FROM TB_MEMBER  m<br/>
JOIN TB_GRADE g ON m.GRADE = g.GRADE_CODE <br/>
WHERE MEMBERID = 'SS50000';<br/>
<br/><br/>
-- select 서브쿼리 활용한 예제<br/>
--TB _MEMBER 테이블에서  GRADE 가 우수회원 이면서<br/>
--AREA_CODE 가 '031' 인 회원의 회원 이름 조회하기<br/>

SELECT MEMBER_NAME<br/>
FROM TB_MEMBER <br/>
WHERE GRADE = (<br/>
				SELECT GRADE_CODE <br/>
				FROM TB_GRADE <br/>
				WHERE GRADE_NAME = '우수회원')<br/>
AND AREA_CODE ='031';<br/>
<br/><br/>


--TB_MEMBER 테이블에서 GRADE가 '일반회원'이면서 AREA_CODE가 '02'가 아닌 회원의 회원 ID 조회하기.<br/>

SELECT MEMBERID<br/>
FROM TB_MEMBER <br/>
WHERE GRADE = (<br/>
	SELECT GRADE_CODE <br/>
	FROM TB_GRADE <br/>
	WHERE GRADE_NAME = '일반회원')<br/>
AND AREA_CODE != '02';<br/>

--TB_MEMBER 테이블에서 GRADE 가 '특별회원'이면서'
--AREA_CODE 가 '031' 이 아닌 회원들의 회원 이름 조회하기
SELECT MEMBER_NAME
FROM TB_MEMBER
WHERE GRADE = (
	SELECT GRADE_CODE 
	FROM TB_GRADE 
	WHERE GRADE_NAME='특별회원')
AND AREA_CODE != '031';

-- TB_MEMBER 테이블에서 
--AREA_CODE가 031이거나 032 인 회원들의 이름 조회
SELECT MEMBER_NAME
FROM TB_MEMBER 
WHERE AREA_CODE IN('031','032');


-- selct rownum을 활용한 예제
--ROWNUM 이란? select 해온 데이터에 번호를 붙이는 것
-- 번호를 붙여 원하는 만큼의 갯수만 가져오고 싶을 때 사용

--TB_MEMBER 회원들 중에서  ROWNUM 이 3 이하인 데이터 조회!
SELECT *
FROM TB_MEMBER
WHERE ROWNUM <= 3;

-- TB_MEMBER 테이블에서
--지역코드가 031 인 회원 중에서 
--처음 3명의 아이디와 이름 조회하기
SELECT MEMBERID, MEMBER_NAME
FROM TB_MEMBER 
WHERE AREA_CODE ='031' AND ROWNUM <=3;

--TB_MEMBER 이름순으로 상위 3개 멤버 조회하기
SELECT MEMBERID, MEMBER_NAME
FROM (
SELECT MEMBERID, MEMBER_NAME, ROWNUM AS RN
 FROM TB_MEMBER
 ORDER BY MEMBER_NAME) --AS 별칭
 WHERE RN <= 3;










