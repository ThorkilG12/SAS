## Show it in a Relational Database ##
```SQL
DROP TABLE if EXISTS famtree;
CREATE TEMP TABLE famtree AS (
SELECT * FROM (
            SELECT * FROM (SELECT 'a' AS parent, 'h' AS child) a
  UNION ALL SELECT * FROM (SELECT 'a' AS parent, 'c' AS child) a
  UNION ALL SELECT * FROM (SELECT 'b' AS parent, 'd' AS child) a
  UNION ALL SELECT * FROM (SELECT 'b' AS parent, 'e' AS child) a
  UNION ALL SELECT * FROM (SELECT 'b' AS parent, 'f' AS child) a
  UNION ALL SELECT * FROM (SELECT 'c' AS parent, 'g' AS child) a
  UNION ALL SELECT * FROM (SELECT 'c' AS parent, 'h' AS child) a
  UNION ALL SELECT * FROM (SELECT 'd' AS parent, 'i' AS child) a
  UNION ALL SELECT * FROM (SELECT 'd' AS parent, 'j' AS child) a
  UNION ALL SELECT * FROM (SELECT 'g' AS parent, 'k' AS child) a
) a
);
SELECT * 
  FROM famtree
;
WITH recursive ancestor (child, parent, l) as ( 
	SELECT parent, CAST(NULL AS VARCHAR(1)), 0
	FROM famtree
	WHERE parent NOT IN (SELECT child FROM famtree) 
	UNION ALL 
	SELECT f.child
		   , CAST((CASE WHEN a.l = 0 THEN a.child ELSE a.parent END) AS VARCHAR(1))
	       , (a.l + 1)
	FROM famtree f JOIN ancestor a ON f.parent = a.child
)
SELECT distinct parent, child, l FROM ancestor 
WHERE parent IS NOT NULL order by child;
```
In SAS it looks like this:
```SAS
data famtree;
  input parent $ child $;
  put parent= child=;
cards;
a h
a c
b d
b e
b f
c g
c h
d i
d j
g k
;
* below a solution where it's hardcoded that we have two levels ;
PROC SQL;
CREATE TABLE level_1 as
  SELECT parent, child, 1 as level
  FROM famtree
  WHERE parent not in (SELECT child FROM famtree);
CREATE TABLE level_2 as
  SELECT level_1.parent, famtree.child, 2 as level
  FROM level_1 INNER JOIN famtree
  ON famtree.parent= level_1.child;
quit;
data ancestor;
  set level_1 level_2;
run;
proc sort data=ancestor;
  by child;
proc print data=ancestor;
  title Child k is missing - Only 9 obs.;
run;
%macro ftmacro;
  %local level nlevel;
  %let level=1; 
  proc sql; 
    CREATE table level_1 as
    SELECT parent, child, 1 as level
    FROM famtree
    WHERE famtree.parent not in ( select child from famtree)
  ;
  %do %while(&SQLOBS > 0);
    %let nlevel = %eval(&level + 1);
    CREATE table level_&nlevel as
    SELECT level_&level..parent, famtree.child, &nlevel as level
    FROM famtree INNER JOIN level_&level
    ON famtree.parent=level_&level..child;
    %let level = &nlevel;
  %end;
  data final;
    set 
    %do ii = 1 %to %eval(&level - 1);
      level_&ii
    %end;
    ;
  run; 
%mend;
%ftmacro; 
proc print data=ancestor;
  title This is dynamic - all leves and 10 obs.;
run;
```
--oOo--
