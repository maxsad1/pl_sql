1. Создаем таблицу

create table test_table
             (d_date date,
              n_num integer);

2. Добавляем данные

INSERT INTO test_table (d_date, n_num) VALUES (to_date('01/08/2006','DD/MM/YYYY'), 1);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-05-03', 2);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-05-03', 2);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-07-02', 2);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-07-02', 3);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-17', 4);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-08', 5);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-08', 6);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-14', 8);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-14', 7);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-25', 9);
INSERT INTO test_table (d_date, n_num) VALUES (DATE '2006-08-29', 9);
commit;

Результат (select * from test_table): 
D_DATE                N_NUM
2006-08-01T00:00:00Z	1
2006-05-03T00:00:00Z	2
2006-05-03T00:00:00Z	2
2006-07-02T00:00:00Z	2
2006-07-02T00:00:00Z	3
2006-08-17T00:00:00Z	4
2006-08-08T00:00:00Z	5
2006-08-08T00:00:00Z	6
2006-08-14T00:00:00Z	8
2006-08-14T00:00:00Z	7
2006-08-25T00:00:00Z	9
2006-08-29T00:00:00Z	9


1. Сделать суммирование по 3 датам

select
         to_char(d_date, 'DD.MM.YYYY') d_date
       , sum (n_num)                   n_num
from
         test_table
where
         d_date in ( DATE '2006-07-02'
                  ,  DATE '2006-08-08'
                  ,  DATE '2006-08-14')
group by
         to_char(d_date, 'DD.MM.YYYY'); 
         
Результат:
D_DATE	N_NUM
02.07.2006	5
08.08.2006	11
14.08.2006	15
         
 
 
2. Вывести значения если 2 = то 02, если нет, то 01 у всех значения между 2 или 5

select
         to_char(d_date, 'DD.MM.YYYY') d_date
       , case
                  when n_num = 2
                           then '02'
                           else '01'
         end n_num
from
         test_table
order by
         to_date (d_date,'DD-MM-YYYY');

Результат:


3. Сгенерировать даты от 01.08 до 31.08  и добавить их в выборку. Выести все даты за август

 select
        to_char(d.d, 'DD.MM.YYYY') d_date
      , d.n                        n_num
 from
        (
                  select
                            to_DATE ('2006-08-01', 'yyyy-mm-dd') + n.lev d
                          , nvl (t. n_num, 0)                            n
                  from
                            (
                                   select
                                          level - 1 lev
                                   from
                                          dual connect by level < 32
                            )
                            n
                            left join
                                      test_table t
                                      on
                                                t.d_date = to_DATE ('2006-08-01', 'yyyy-mm-dd') + n.lev
                  order by
                            1
        ) d ;

Результат:
D_DATE	N_NUM
01.08.2006	1
02.08.2006	0
03.08.2006	0
04.08.2006	0
05.08.2006	0
06.08.2006	0
07.08.2006	0
08.08.2006	6
08.08.2006	5
09.08.2006	0
10.08.2006	0
11.08.2006	0
12.08.2006	0
13.08.2006	0
14.08.2006	8
14.08.2006	7
15.08.2006	0
16.08.2006	0
17.08.2006	4
18.08.2006	0
19.08.2006	0
20.08.2006	0
21.08.2006	0
22.08.2006	0
23.08.2006	0
24.08.2006	0
25.08.2006	9
26.08.2006	0
27.08.2006	0
28.08.2006	0
29.08.2006	9
30.08.2006	0
31.08.2006	0

Проверял тут: http://sqlfiddle.com/#!4/4ecc5/146

