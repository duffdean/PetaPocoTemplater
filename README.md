# PetaPocoTemplater

select '___client_training_courses' into @table; #table name
select concat('public class ',@table,'{') union
select concat('public ',tps.dest,' ',column_name,'{get;set;}') from  information_schema.columns c
join( #datatypes mapping
select 'char' as orign ,'string' as dest union all
select 'varchar' ,'string' union all
select 'longtext' ,'string' union all
select 'datetime' ,'DateTime?' union all
select 'text' ,'string' union all
select 'bit' ,'int?' union all
select 'bigint' ,'int?' union all
select 'int' ,'int?' union all
select 'double' ,'double?' union all
select 'decimal' ,'double?' union all
select 'date' ,'DateTime?' union all
select 'tinyint' ,'bool?'
) tps on c.data_type like tps.orign
where table_name=@table union
select '}';
