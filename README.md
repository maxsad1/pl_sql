create table test_table
             (d_date date,
              n_num integer);
              
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


d_date           n_num

01.05.2016       1
06.05.2016       2
15.07.2016       4
20.07.2016       2
24.08.2016       2
24.08.2016       5
28.08.2016       3
28.08.2016       4
26.08.2016       7
30.08.2016       9


1. Сделать суммирование по 3 датам
2. Вывести значения если 2 = то 1, если нет, то 0 у всех значения между 2 и 5
3. Сгенерировать даты от 01.08 до 31.08

data1      num1


