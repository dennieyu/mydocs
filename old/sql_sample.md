
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
