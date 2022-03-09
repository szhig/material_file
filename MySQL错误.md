## MySQL错误

1.cannot add foreign key constraint



2.1452-Cannot add or update a child row a foreign key constraint fals (start.city tsql-eb4.40 ; CONSTRAINT'Kk fk k user id FOREIGN KEY ( userid)REFERENCES userT (id`)

原因：在添加外键时有默认值，但在外键所在的表并没有该值

解决：更改外键的值