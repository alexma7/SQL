Инструкция
========================
Содержание
-------------------------
1. [Установка](https://github.com/alexma7/SQL/wiki/INSERT,-DELETE,-UPDATE,-CREATE,-%D0%B2%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B0,-%D1%83%D0%B4%D0%B0%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5,-%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5)
2. [Создание первого проекта](#Создание-первого-проекта)
3. [тест](test)
4. [INSERT](#INSERT) 
5. [lin](#1.1-My)

## ПЕРЕНЕСТИ
```SQL
--Изменить кодировку столбца, что бы не выскакивала ошибка
ALTER TABLE trash.dbo.class20220804
ALTER COLUMN lvl5 VARCHAR(250) COLLATE SQL_Latin1_General_CP1251_CI_AS
```


## INSERT2
, DELETE, UPDATE, CREATE, вставка, удаление, обновление
```SQL
INSERT INTO dbo.Points (PointValue) 
VALUES (CONVERT(Point, '3,4')); // Вместо VALUES можно вставить SELECT

UPDATE baza_telpr_21090627
SET Codr = @codInto
WHERE Cod = @codFrom

//апдейт при сравнении двух итоговых таблиц, 	
UPDATE SprShowSammary 
SET SprShowSammary.nameResult = ssu.nameResult
FROM #SprShowUpdate ssu
WHERE  SprShowSammary.idShopSammary = ssu.idShopSammary 
   AND SprShowSammary.idResult = ssu.idResult 

--Версия с LEFT JOIN 
UPDATE t2
SET t2.email = t1.email, t2.podr = t1.email 
FROM #tbl1 t1
    LEFT JOIN  t2
	ON t1.idUser = t2.idUser


DELETE FROM baza
WHERE Cod = @cod

--Обновление через JOIN
UPDATE  tbl2
SET tbl2.column = 1
FROM table1 tbl1
   LEFT JOIN table2 TC ON tbl2.id = tbl1.id


--Создание таблицы
CREATE TABLE #temp_tbl (
    id INT,
    name NVARCHAR(2000)
);
```

# INSERT
 CURSOR, WHILE, курсор
```SQL
--Описываем и открываем курсор
DECLARE MyCursor CURSOR FOR
--Вставляем в курсор номера из таблицы SprParentMobil, что бы произвести их перечисление в последующих операциях
SELECT IdParentMobil FROM SprParentMobil WHERE actual = 1
--Открываем курсор, в котором находятся номера из предыдущего запроса
OPEN MyCursor
--Вставляем данные из курсора в переменную, для дальнейшего использования
FETCH FROM MyCursor INTO @idParentMobil

-- Получаем количество актуальных idParentMobil, которые необходимо выгружать
SET @i = (SELECT COUNT(*) FROM SprParentMobil WHERE actual = 1 )  

WHILE @i>0
BEGIN
	--Выполняем код с полученным значением от курсора
	--КОД
	--После использования значения из курсора, нам необходимо получить следующее, для этого используется следующая строка
	FETCH NEXT FROM MyCursor INTO @idParentMobil;
	SET @i = @i-1
END
--Закрываем курсор
CLOSE MyCursor; 
--Уничтожаем его
DEALLOCATE MyCursor;
```



# 1.1-My
```SQL
--Описываем и открываем курсор
DECLARE MyCursor CURSOR FOR
--Вставляем в курсор номера из таблицы SprParentMobil, что бы произвести их перечисление в последующих операциях
SELECT IdPare
```
