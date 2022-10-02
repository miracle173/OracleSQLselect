# OracleSQLselect
Tutorial for Oracle Select Queries
## Oarcle Documentation ##
Oracle&registered; Database  
SQL Language Reference  
21c  
F31301-10  
July 2022  




## Analytic Functions ##


[Link](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/Analytic-Functions.html#GUID-527832F7-63C0-4445-8C16-307FA5084056) to documentation: *7 Functions / Analytic Functions*

> Analytic functions are the last set of operations performed in a query except for the final ORDER BY clause. All joins and all WHERE, GROUP BY, and HAVING clauses are completed before the analytic functions are processed. Therefore, analytic functions can appear only in the select list or ORDER BY clause.

The table is divided in partitions by the ``partitioned by`` clause. 

    /*
    for i in range (1,5):
        for j in range (1,6):
            if i==1: 
                print('insert into tab1( col1, col2,col3 ) values(',10*i+j,',',i,',',100*i+i,');')
            elif i==2:
                print('insert into tab1( col1, col2,col3 ) values(',10*i+j,',',i,',',100*i+j**2,');')
            elif i==3:
                print('insert into tab1( col1, col2,col3 ) values(',10*i+j,',',i,',',(100*i+j),');')
            elif i==4:
                print('insert into tab1( col1, col2,col3 ) values(',10*i+j,',',i,',',100*i+j//2,');')
            else:
                raise ValueError('invalid value of i')  
    */

    create table tab1 (col1 number, col2 number, col3 number);

    insert into tab1( col1, col2,col3 ) values( 11 , 1 , 101 );
    insert into tab1( col1, col2,col3 ) values( 12 , 1 , 101 );
    insert into tab1( col1, col2,col3 ) values( 13 , 1 , 101 );
    insert into tab1( col1, col2,col3 ) values( 14 , 1 , 101 );
    insert into tab1( col1, col2,col3 ) values( 15 , 1 , 101 );
    insert into tab1( col1, col2,col3 ) values( 21 , 2 , 201 );
    insert into tab1( col1, col2,col3 ) values( 22 , 2 , 204 );
    insert into tab1( col1, col2,col3 ) values( 23 , 2 , 209 );
    insert into tab1( col1, col2,col3 ) values( 24 , 2 , 216 );
    insert into tab1( col1, col2,col3 ) values( 25 , 2 , 225 );
    insert into tab1( col1, col2,col3 ) values( 31 , 3 , 301 );
    insert into tab1( col1, col2,col3 ) values( 32 , 3 , 302 );
    insert into tab1( col1, col2,col3 ) values( 33 , 3 , 303 );
    insert into tab1( col1, col2,col3 ) values( 34 , 3 , 304 );
    insert into tab1( col1, col2,col3 ) values( 35 , 3 , 305 );
    insert into tab1( col1, col2,col3 ) values( 41 , 4 , 400 );
    insert into tab1( col1, col2,col3 ) values( 42 , 4 , 401 );
    insert into tab1( col1, col2,col3 ) values( 43 , 4 , 401 );
    insert into tab1( col1, col2,col3 ) values( 44 , 4 , 402 );
    insert into tab1( col1, col2,col3 ) values( 45 , 4 , 402 );

    select col1, col2, col3
    from tab1
    order by 1,2,3;

    select sum(col1), sum(col2), sum(col3)
    from tab1;

    select sum(col1), sum(col2), sum(col3)
    from tab1;

    select  sum(distinct col1), sum(distinct col2), sum(distinct col3)
    from tab1;


    select col1, sum(col2)
    from tab1
    group by col1;

    select sum(col2) over (partition by col1) val
    from tab1;

    select col1,col2,sum(col3) over (partition by col2 order by col3) val
    from tab1;

    select col1,col2,
        sum(col3) over (
            partition by col2 
            order by col3
            range between unbounded preceding and current row
        ) val
    from tab1;

    # nondeterministic
    select col1,col2,  
        sum(col3) over (
            partition by col2 
            order by col3
            rows  between unbounded preceding and current row
        ) val
    from tab1;

    select col1,col2,
        sum(col3) over (
            partition by col2 
            order by col3
            range between unbounded preceding and unbounded following
        ) val
    from tab1;

    select col1,col2,
        sum(col3) over (
            partition by col2 
            order by col3
            range between 1 preceding  and 1 following
        ) val
    from tab1;

    select col1,col2,
        sum(col3) over (
            partition by col2 
            order by col3
            rows between 1 preceding  and 1 following
        ) val
    from tab1;


    select col1, col2, col3
    from tab1
    order by 1,2,3;

| COL1 | COL2 | COL3 |
| ----:|----:|----:|
| 11 | 1 | 101 |
| 12 | 1 | 101 |
| 13 | 1 | 101 |
| 14 | 1 | 101 |
| 15 | 1 | 101 |
| 21 | 2 | 201 |
| 22 | 2 | 204 |
| 23 | 2 | 209 |
| 24 | 2 | 216 |
| 25 | 2 | 225 |
| 31 | 3 | 301 |
| 32 | 3 | 302 |
| 33 | 3 | 303 |
| 34 | 3 | 304 |
| 35 | 3 | 305 |
| 41 | 4 | 400 |
| 42 | 4 | 401 |
| 43 | 4 | 401 |
| 44 | 4 | 402 |
| 45 | 4 | 402 |
