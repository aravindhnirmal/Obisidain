[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

Each assertion is given a constraint name and is specified via a condition similar to the WHERE clause of an SQL query
  
CREATE ASSERTION  [ assertion_name ]
CHECK ( [ condition ] );


CREATE ASSERTION SALARY_CONSTRAINT
CHECK ( NOT EXISTS ( SELECT     *FROM  EMPLOYEE E, EMPLOYEE M,DEPARTMENT D
WHERE       E.Salary>M.Salary

 

AND E.Dno=D.Dnumber

AND D.Mgr_ssn=M.Ssn ) );
