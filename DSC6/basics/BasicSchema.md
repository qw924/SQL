# Basic Schema Definition
```
create table department
	(dept name varchar (20),
		building varchar (15),
		budget numeric (12,2),
		primary key (dept name));

create table course
	(course id varchar (7),
		title varchar (50),
		dept name varchar (20),
		credits numeric (2,0),
		primary key (course id),
		foreign key (dept name) references department);

create table instructor
	(ID varchar (5),
		name varchar (20) not null,
		dept name varchar (20),
		salary numeric (8,2),
		primary key (ID),
		foreign key (dept name) references department);

create table section
	(course id varchar (8),
		sec id varchar (8),
		semester varchar (6),
		year numeric (4,0),
		building varchar (15),
		room number varchar (7),
		time slot id varchar (4),
		primary key (course id, sec id, semester, year),
		foreign key (course id) references course);

create table teaches
	(ID varchar (5),
		course id varchar (8),
		sec id varchar (8),
		semester varchar (6),
		year numeric (4,0),
		primary key (ID, course id, sec id, semester, year),
		foreign key (course id, sec id, semester, year) references section,
		foreign key (ID) references instructor);
```

```
create table r
	(A1 D1,
		A2 D2,
		...,
		An Dn,
		<integrity-constraint1>,
		...,
		<integrity-constraintk>,);
```

```
insert into instructor
	values (10211, ’Smith’, ’Biology’, 66000);
```

```
delete from student;
```

```
drop table r;
```
The alter table command to add attributes to an existing relation
```
alter table r add AD;
```

```
alter table r drop A;
```
