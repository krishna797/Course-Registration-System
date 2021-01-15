# Course-Registration-System

-----Database Tables----


----Drop table----

drop table department cascade constraints;
drop table program cascade constraints;
drop table course cascade constraints;
drop table prerequisit cascade constraints;
drop table building cascade constraints;
drop table room cascade constraints;
drop table d_instructor cascade constraints;
drop table c_load cascade constraints;
drop table c_teach cascade constraints;
drop table non_teaching cascade constraints;
drop table time_block cascade constraints;
drop table section cascade constraints;
drop table schedule cascade constraints;
drop table student cascade constraints;
drop table wait_list cascade constraints;
drop table s_registration cascade constraints;
drop table s_permit cascade constraints;



----Tables---



create table department
(
		did varchar(100),
		dname varchar(100),
		primary key (did)
);

insert into department values('IS', 'Information System');
insert into department values('CS', 'Computer Science');
insert into department values('DS', 'Data Science');
insert into department values('SE', 'Software Engineering');
insert into department values('ME','Mechanical Engineering');

create table program
(
	pid varchar(100),
	did varchar(100),
	pname varchar(100),
	ptype int,
	primary key(pid)
);
insert into program values('ISBS', 'IS', 'Bachelor Of Science in Information System', 1);
insert into program values('ISMS','IS' ,'Master Of Science in Information System', 2);
insert into program values('ISPhD', 'IS'  ,'PhD in Information System', 3);
insert into program values('CSBS','CS' ,'Bachelor Of Science in Computer Science', 1);
insert into program values('CSMS', 'CS' ,'Master Of Science in Computer Science', 2);
insert into program values('CSPhD', 'CS'  ,'PhD in Computer Science', 3);

create table course
(
	pid varchar(100),
	cid varchar(100),
	cname varchar(100),
	credits int,
	grading varchar(100),
	required int,
	roomtype int,
	section int,
	csize int,
	status int,
	primary key(cid),
	foreign key(pid) references program(pid),
	foreign key (pid) references program(pid)
	); 

insert into course values('ISMS', 'IS 620' , 'Advance Database Project', 3,3, 1, 0, 2, 50, 1);
insert into course values('ISMS', 'IS 601' , 'Information System', 3, 4 , 1, 0, 2, 50, 1);
insert into course values('ISMS', 'IS 650' , 'Artificial Intelligence', 3, 2 , 1, 0, 3, 20, 1);
insert into course values('ISMS', 'IS 636' , 'System Analysis and Design', 3,1 , 1, 1, 2, 15, 0);
insert into course values('ISMS', 'IS 603' , 'Decision technology', 3, 2 , 1, 1, 2, 15, 0);
insert into course values('ISMS', 'IS 765' , 'Project Management', 3, 2 , 0, 0, 2, 15, 0);
insert into course values('ISMS', 'IS 660' , 'Health Care', 3, 1 , 0, 0, 2, 15, 0);
insert into course values('ISMS', 'IS 611' , 'Big Data', 3, 2 , 1, 1, 2, 15, 0);

create table prerequisit
(
	cid varchar(100),
	prid varchar(100),
	prname varchar(100),
	primary key(prid),
 	foreign key(cid) references course(cid)
);
insert into prerequisit values('IS 620', 'IS 403', 'Database Management System');
insert into prerequisit values('IS 650', 'IS 649 ', 'Artificial Intelligence');
insert into prerequisit values('IS 636', 'IS 100', 'System Analysis and Design');
insert into prerequisit values('IS 603', 'IS 202',  'Decision technology');
insert into prerequisit values('IS 601', 'IS 330', 'Introduction to information system');

create table building
(
	bid varchar(100),
	bname varchar(100),
    primary key (bid)
);
insert into building values('IT', 'Information And Technology');
insert into building values('PH', 'Physics');
insert into building values('CH', 'Chemistry');
insert into building values('AR', 'Arts and Humanity');
insert into building values('MT', 'Mathematics');

create table room
(
    bid varchar(100),
    rid int,
	rname varchar(100),
	total_seats int,
	room_type int,
	primary key(rid),
	foreign key (bid) references building(bid)
);
insert into room values('IT',201,'IT201',50,0);
insert into room values('PH',202,'PH202',50,0);
insert into room values('CH',203,'CH203',50,0);
insert into room values('MT',206,'MT206',50,1);
insert into room values('MT',207,'MT207',50,1);

create table d_instructor
(
     iid int,  
     iname varchar(100),
	 did varchar(100),
     itype varchar(100),
	 primary key(iid),
	 foreign key(did) references department(did)
);
insert into d_instructor values(1,'Chen','IS','full-time');
insert into d_instructor values(2,'Vandana Janeja','IS', 'part-time');
insert into d_instructor values(3,'Karabatis', 'IS','full-time');
insert into d_instructor values(4,'James Foulds','IS','full-time');
insert into d_instructor values(5,'John Hebler','IS','part-time');
insert into d_instructor values(6,'Karuna Joshi','IS','part-time');

create table c_load
(	
	cload_id int,
	iid int,
	iname varchar(100),
	year int,
	semester varchar(100),
	cid varchar(100),
	cname varchar(100),
	pid varchar(100),
	c_weight int,
	section int,
    assigned_no int,
	foreign key(pid) references program(pid),
	foreign key(iid) references d_instructor(iid),
	foreign key(cid) references course(cid)

);

Insert into c_load values(2,1,'Chen',2019,'Fall','IS 620','Advance Database Project','ISMS',null,2,1);
Insert into c_load values(2,5,'John Hebler',2019,'Fall','IS 636','System Analysis and Design','ISMS',null,2,1);
Insert into c_load values(1,3,'Karabatis',2019,'Fall','IS 601','Information System','ISMS',null,2,1);
Insert into c_load values(1,4,'James Foulds',2019,'Fall','IS 603','Decision technology','ISMS',null,2,1); 
Insert into c_load values(1,6,'Karuna Joshi',2019,'Fall','IS 611','Big Data','ISMS',null,2,1); 
Insert into c_load values(2,2,'Vandana Janeja',2019,'Fall',null,null,null,null,null,0);

create table c_teach
(
	iid int,
	iname varchar(100),
	cid varchar(100),
	cname varchar(100),
	section int,
	year int,
	semester varchar(100),
	foreign key(iid) references d_instructor(iid),
	foreign key(cid) references course(cid)
);   

insert into c_teach values(1,'Chen','IS 620', 'Advance Database Project' , 2 , 2019, 'Fall');
insert into c_teach values(1,'Chen','IS 650', 'Artificial Intelligence',1 ,2019, 'Fall');
insert into c_teach values(2,'Vandana Janeja', 'IS 650','Artificial Intelligence',2,2019, 'Fall');
insert into c_teach values(3,'Karabatis', 'IS 650','Artificial Intelligence',2,2019, 'Fall');
insert into c_teach values(3,'Karabatis', 'IS 601','Information System',2,2019, 'Fall');
insert into c_teach values(4,'James Foulds','IS 603', 'Decision Technology',2,2019, 'Fall');


create table non_teaching
(
	iid int,
	iname varchar(100),
	day1_not int,
	day2_not int,
	foreign key(iid) references d_instructor(iid)
);  

insert into non_teaching values(1 ,'Chen',2,5);
insert into non_teaching values(2 ,'Vandana Janeja',2,3);
insert into non_teaching values(5 ,'John Hebler',1,5);
insert into non_teaching values(3,'Karabatis',2,5);
insert into non_teaching values(4 ,'James Foulds',3,4);
insert into non_teaching values(6 ,'Karuna Joshi',3,4);

Create table time_block
(
	tblock_id int,
	length varchar(100),
	se_time varchar(100),
	day1 int,    
	day2 int,
	primary key(tblock_id)
);

Insert into time_block values(1001,'2.5 hours','4:30-7 p.m.' ,1,null);
Insert into time_block values(2001,'1 hour 15 minutes','1-2:15 p.m.',3,5);
Insert into time_block values(3001,'1 hour 15 minutes','3-4:15 p.m.',2,4);
Insert into time_block values(4001,'2.5 hours','7:10-9:40 p.m.' ,4,null);
Insert into time_block values(5001,'2.5 hours','7:10-9:40 p.m.',2,null);
Insert into time_block values(6001,'2.5 hours','7:10-9:40 p.m.',1,null);
Insert into time_block values(7001,'2.5 hours','7:10-9:40 p.m.',5,null);
Insert into time_block values(8001,'2.5 hours','7:10-9:40 p.m.',2,null);
Insert into time_block values(9001,'2.5 hours','7:10-9:40 p.m.',3,null);
Insert into time_block values(10001,'2.5 hours','4:30-7 p.m.',3,null);


create table section
(
	section_id int,
     csize int,
	cid varchar(100),
	status int,
	primary key(section_id),
	foreign key(cid) references course(cid)
);  

insert into section values(476 ,50,'IS 620',1);
insert into section values(479 ,15,'IS 636',0);
insert into section values(474 ,15,'IS 603',0);
insert into section values(472 ,50,'IS 601',0);
insert into section values(471 ,15,'IS 611',0);

create table schedule(
	sch_id varchar(100),
	sid int,
	cid varchar(100),
	section_id int,
	iid int,
	year int,
	semester varchar(100),
	section int,
	capacity int,
	tblock_id int,
	day int,
	rid int,
	waiting_capacity int,
	status int,
	primary key(sch_id),
	foreign key(cid) references course(cid),
	foreign key(sid) references student(sid),
	foreign key(rid) references room(rid),
	foreign key(iid) references d_instructor(iid),
	foreign key(section_id) references section(section_id),
	foreign key(tblock_id) references time_block(tblock_id));  
insert into schedule values('SCH001',1,'IS 620',476,1,2019,'Fall',2,45,1001,1,101,15,1);
insert into schedule values('SCH002',2,'IS 636',479,5,2019,'Fall',2,45,1001,2,210,15,0);
insert into schedule values('SCH003',3,'IS 603',474,4,2019,'Fall',2,45,5001,2,111,15,0);
insert into schedule values('SCH004',4,'IS 601',472,3,2019,'Fall',2,45,5001,4,308,15,0);
insert into schedule values('SCH005',5,'IS 611',471,6,2019,'Fall',2,45,6001,1,308,15,0);

create table student
(
	sid int,
	sname varchar(100),
	pid varchar(100),
	pname varchar(100),
	primary key(sid),
	foreign key(pid) references program(pid));  
insert into student values(1,'Simran', 'ISBS', 'Bachelor Of Science in Information System');
insert into student values(2,'Krishna', 'ISMS','Master Of Science in Information System');
insert into student values(3,'Tanvi', 'ISMS', 'Master Of Science in Information System');
insert into student values(4,'Indrajeet', 'ISMS','Master Of Science in Information System' );
insert into student values(5,'Aman', 'CSMS','Master Of Science in Computer Science' );


Create table wait_list
(
	sid int,
	sch_id varchar(100),
    csize int,
	position int,
	rid int,
	cid varchar(100),
	primary key(position),
	foreign key(sid) references student(sid),
	foreign key(rid) references room(rid),
	foreign key(cid) references course(cid),
	foreign key(sch_id) references schedule(sch_id)
);
insert into wait_list values(1,'SCH001',50,3,201,'IS 620');
insert into wait_list values(2,'SCH002',50,2,202,'IS 601');
insert into wait_list values(1,'SCH003',15,1,203,'IS 603');
insert into wait_list values(4,'SCH004',4,20,206,'IS 650');
insert into wait_list values(5,'SCH005',5,15,207,'IS 636');

create table s_registration
(
	sid int,
	cid varchar(100),
	r_status int,
	sch_id varchar(100),
	foreign key(cid) references course(cid),
	foreign key(sch_id) references schedule(sch_id),
	foreign key(sid) references student(sid)
);
insert into s_registration values (1,'IS 620',1,'SCH001');
insert into s_registration values (2,'IS 601',0,'SCH002');
insert into s_registration values (3,'IS 603',2,'SCH003');
insert into s_registration values (3,'IS 650',0,'SCH004');
insert into s_registration values (5,'IS 636',1,'SCH005');

create table s_permit
(
	sid int,
	sch_id varchar(100),
	cid varchar(100),
	permission_type varchar(100),
	foreign key(cid) references course(cid),
	foreign key(sid) references student(sid),
	foreign key(sch_id) references schedule(sch_id)
);
insert into s_permit values (1,'SCH001','IS 603',1);
insert into s_permit values (2,'SCH002','IS 650',1);
insert into s_permit values (1,'SCH003','IS 636',2);
insert into s_permit values (3,'SCH004','IS 601',1);
insert into s_permit values (2,'SCH005','IS 611',1);


---Create sequences---
----feature 1---

CREATE SEQUENCE autocourseid
  MINVALUE 1
  START WITH 1
  INCREMENT BY 1
  NOCACHE;

---feature2---

CREATE SEQUENCE autoinstid
  MINVALUE 1
  START WITH 7
  INCREMENT BY 1
  NOCACHE
----feature 6 ----

create sequence sdlid start with 7 increment by 1;


