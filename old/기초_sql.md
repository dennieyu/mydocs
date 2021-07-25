
# 조인시 값이 없는 조인측에 "(+)"를 위치 시킨다.

```
SELECT DISTINCT(e.deptno), d.deptno
  FROM emp e, dept d
 WHERE e.deptno(+) = d.deptno;
 
DEPTNO  DEPTNO
------- --------
     10       10
     20       20
     30       30
              40
```

# ANSI/ISO SQL 표준인 RIGHT OUTER JOIN와 동일하다.
```
SELECT DISTINCT(e.deptno), d.deptno
  FROM emp e
 RIGHT OUTER JOIN dept d
    ON e.deptno = d.deptno;

DEPTNO  DEPTNO
------- --------
     10       10
     20       20
     30       30
              40
```

# 프로그래머스 group by (4/4) 문제
```
SELECT T1.HOUR, IFNULL(T2.COUNT, 0) 
  FROM (
    SELECT 0 AS HOUR, 0 AS COUNT
     UNION SELECT 1 AS HOUR, 0 AS COUNT
     UNION SELECT 2 AS HOUR, 0 AS COUNT
     UNION SELECT 3 AS HOUR, 0 AS COUNT
     UNION SELECT 4 AS HOUR, 0 AS COUNT
     UNION SELECT 5 AS HOUR, 0 AS COUNT
     UNION SELECT 6 AS HOUR, 0 AS COUNT
     UNION SELECT 7 AS HOUR, 0 AS COUNT
     UNION SELECT 8 AS HOUR, 0 AS COUNT
     UNION SELECT 9 AS HOUR, 0 AS COUNT
     UNION SELECT 10 AS HOUR, 0 AS COUNT
     UNION SELECT 11 AS HOUR, 0 AS COUNT
     UNION SELECT 12 AS HOUR, 0 AS COUNT
     UNION SELECT 13 AS HOUR, 0 AS COUNT
     UNION SELECT 14 AS HOUR, 0 AS COUNT
     UNION SELECT 15 AS HOUR, 0 AS COUNT
     UNION SELECT 16 AS HOUR, 0 AS COUNT
     UNION SELECT 17 AS HOUR, 0 AS COUNT
     UNION SELECT 18 AS HOUR, 0 AS COUNT
     UNION SELECT 19 AS HOUR, 0 AS COUNT
     UNION SELECT 20 AS HOUR, 0 AS COUNT
     UNION SELECT 21 AS HOUR, 0 AS COUNT
     UNION SELECT 22 AS HOUR, 0 AS COUNT
     UNION SELECT 23 AS HOUR, 0 AS COUNT
    ) T1
  LEFT JOIN (
    SELECT hour(DATETIME) AS HOUR, count(*) AS COUNT
      FROM ANIMAL_OUTS 
     GROUP BY hour(DATETIME)
    ) T2 
    ON T1.HOUR = T2.HOUR
```

# mybatis 에서 `foreach` 를 사용하여 다중 INSERT 시 `UNION` 을 이용해서 중복 제거
```
<foreach item="member" collection="memberList" separator="UNION">
(
	select 변수1, 변수2
)
</foreach>
```

# How to fix error converting data type
```
DATEADD(A.CREATE_TIME, CAST(#{appendTime, jdbcType=INTEGER} AS INT), 'SECOND'))
```

# CASE 문
```
(
    CASE
         WHEN (A.OPT = 1) THEN 'Y'
         ELSE 'N'
     END
) AS OPT_FLAG,
```

# 최신 약관
```
SELECT termsMaster.terms_type AS type, CASE WHEN map.terms_id IS null THEN 'N' ELSE 'Y' END AS check
  FROM (
	SELECT terms_type, max(id) as id
	  FROM loapp.tbl_co_terms_master
	 WHERE use_flag = 'Y'
	   AND user_type = 'GUEST'
	 GROUP BY terms_type
) termsMaster
  LEFT OUTER JOIN (SELECT terms_id FROM loapp.tbl_users_terms_map WHERE user_id = #{userId}) map
    ON termsMaster.id = map.terms_id
```

# SUM, ROUND, AVG, IF, IFNULL
```
sum(IF(AGENCY_WEBHOOK_FLAG = 'S' AND A2P_MSG_STATUS IN ('displayed', 'delivered'), 1, 0)) AS SUCCESS_CNT,
```
```
sum(IF(AGENCY_WEBHOOK_FLAG != 'S' OR A2P_MSG_STATUS NOT IN ('displayed', 'delivered'), 1, 0)) AS FAIL_CNT,
```
```
round(avg(IF(AGENCY_WEBHOOK_FLAG = 'S' AND A2P_MSG_STATUS IN ('displayed', 'delivered'), IFNULL(DURATION_WEBHOOK, 0), NULL))) AS DURATION,
```
```
round(avg(IF(AGENCY_WEBHOOK_FLAG = 'S' AND A2P_MSG_STATUS IN ('displayed', 'delivered') and RESULT_CODE = '00000', IFNULL(DURATION_E2E, 0), NULL))) AS DURATION_E2E,
```
