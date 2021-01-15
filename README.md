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




---Feature 1---


Drop sequence autocourseid;
CREATE SEQUENCE autocourseid
  MINVALUE 1
  START WITH 1
  INCREMENT BY 1
  NOCACHE;
CREATE OR REPLACE PROCEDURE insertcourse(
	   dpid IN course.pid%TYPE,
	   dcid IN course.cid%TYPE,
	   dcname in course.cname%TYPE,
           dcredits in course.credits%TYPE,
           dgrading in course.grading%TYPE,
           drequired in course.required%TYPE,
           droomtype in course.roomtype%TYPE,
           dsection in course.section%TYPE,
           dcsize in course.csize%TYPE,
           dstatus in course.status%TYPE)
IS
c number(2):=0;
BEGIN
select count(*) into c from course where cname=dcname;  ----fetch course data----
if c > 0 then
update  course set  pid=dpid, cname=dcname, credits=dcredits, grading=dgrading , required=drequired, roomtype=droomtype, section=dsection, csize=dcsize, status=dstatus where cid=dcid;
COMMIT;
else
insert into course values(dpid, autocourseid.nextval , dcname, dcredits, dgrading , drequired, droomtype, dsection, dcsize, dstatus);   ----insert value in table---
dbms_output.put_line('new courseid is '||autocourseid.currval); 
---print new value---
COMMIT;
end if;
END;
/


-----execution---
Begin   -----will give answer in the positive----
insertcourse('ISMS', 'IS 620' , 'Advance Database Project', 3,3, 1, 0, 2, 50, 1);
end;
/
Begin       ------will give answer in the negatice----
insertcourse('CSMS', 'cs620' , 'Advance Database Project4', 3,3, 1, 0, 2, 50, 1);
end;/


---Feature 2---

-----first create sequence for instructor autogenrate  table----
Drop sequence autoinstid;
CREATE SEQUENCE autoinstid
  MINVALUE 1
  START WITH 7
  INCREMENT BY 1
  NOCACHE;

----- procedure----
CREATE OR REPLACE PROCEDURE insertinstructor(
	   diid IN d_instructor.iid%TYPE,
           diname IN d_instructor.iname%TYPE,
           ditype in d_instructor.itype%TYPE,
           ddid IN d_instructor.did%TYPE
           )
IS
c number(2):=0;
BEGIN
select count(*) into c from d_instructor where iname=diname and itype=ditype and did=ddid;   ----fetch value in the instructor table---
if c > 0 then
dbms_output.put_line('Insructor already exist'); ---print the inst existsed---
else
insert into d_instructor values(autoinstid.nextval,diname,ddid,ditype);
dbms_output.put_line('Insructor ID IS '||autoinstid.currval);  
----insert new value and print that---
COMMIT;
end if;
END;
/

-----Execution----
set serveroutput on;
begin			-----will give positive answer----
insertinstructor(1,'Chen','full-time','IS');
end;
/
Begin     -----will give negative answer----
insertinstructor(7,'James','full-time','IS');
end;
/




---Feature 3---


CREATE OR REPLACE PROCEDURE insert_c_teach(
	   diid IN c_teach.iid%TYPE,
           dcid IN c_teach.cid%TYPE,
           dsection IN c_teach.section%TYPE,
           dyear IN c_teach.year%TYPE,
  333         dsem in c_teach.semester%TYPE,
           day1 in non_teaching.day1_not%TYPE,
           day2 in non_teaching.day2_not%TYPE
6          )
IS
c1 number(2):=0;
c2 number(2):=0;
c3 number(2):=0;
c4 number(2):=0;
BEGIN
select count(*) into c3 from d_instructor where iid=diid;
select count(*) into c1 from c_load where cid=dcid and iid=diid;
select count(*) into c2 from c_teach where cid=dcid and iid=diid ;
select count(*) into c4 from non_teaching where iid=diid and day1_not is not null and day2_not is not null;
if c3>0 then
begin
if c1<3c2 then
dbms_output.put_line('Course load should be greater then course teach '||diid);
------print the statement---
else
insert into c_teach(iid,cid,year,semester,section) values(diid,dcid,dyear,dsem,dsection);
----insert the value in c_teach table---
COMMIT;
end if;
if c4=0 then 
insert into non_teaching(iid,day1_not,day2_not) values(1,day1,day2);
---insert the value in non_teaching table---
COMMIT;
else
dbms_output.put_line('the number of blackout days is over two');
end if;
end;
else
dbms_output.put_line('invalid instructor id');
end if;
END;
/




---execution----
Begin			----execution will insert the new values---
Exec insert_c_teach(1,'IS 620',1,2019,'Fall','Monday','Friday');
end;
/





---Feature 4---

CREATE OR REPLACE PROCEDURE show_course(
	       dyear IN c_teach.year%TYPE,
           dsem in c_teach.semester%TYPE,
           dpid IN course.pid%TYPE)
as
c number(2):=0;
rcname course.cname%TYPE;
rcredits course.credits%TYPE;
rgradins course.grading%TYPE;
rschedule schedule.sch_id%TYPE;
rsection  c_teach.section%TYPE;
riname    c_teach.iname%TYPE;
rrid      schedule.rid%TYPE;
rday1     time_block.day1%TYPE; 
rday2     time_block.day2%TYPE;
rse_time  time_block.se_time%TYPE;
rstatus schedule.status%TYPE;
cursor c1 is select course.cname,course.credits,course.grading,sch_id,c_teach.section,c_teach.iname,schedule.rid,time_block.day1,time_block.day2,se_time,schedule.status from program ,course,c_teach,schedule,time_block where program.pid=course.pid and course.cid=c_teach.cid and schedule.cid=course.cid and schedule.tblock_id=time_block.tblock_id and c_teach.year=dyear and c_teach.semester=dsem and course.pid=dpid order by course.cid,course.section;
BEGIN
select count(*) into c from program where pid=dpid; ----fetch the values of program table----
if c > 0 then
OPEN c1; 
LOOP
        FETCH c1 INTO rcname, rcredits,rgradins,rschedule,rsection,riname,rrid,rday1,rday2,rse_time,rstatus;
        EXIT WHEN c1%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('coursename '||rcname||' credits '||rcredits||' grading '||rgradins||' schedule id '||rschedule||' section '||rsection||' instructor name '||riname||' classroom '||rrid||' day1 '||rday1||
        ' day2 '||rday2||' schedule time '||rse_time||' status '||rstatus);
end loop;
close c1;
else
dbms_output.put_line('invalid program id');
end if;
END;
/

----execution-----
begin
--dbms_output.put_line('record is'); ---show INVALId output---
show_course(2019,'Fall','ISMS3');
end;
/

begin
--dbms_output.put_line('record is');	---show VALId output---
show_course(2019,'Fall','ISMS');
end;
/







----Feature 5---

CREATE OR REPLACE PROCEDURE show_course(
	       dyear IN c_teach.year%TYPE,
           dsem in c_teach.semester%TYPE)
as
rtotal schedule.status%TYPE;
riid schedule.iid%TYPE;
cursor c1 is select count(*),schedule.iid from c_teach,schedule where c_teach.iid=schedule.iid and schedule.year=dyear and schedule.semester=dsem group by schedule.iid,section having count(section)=1;
BEGIN
OPEN c1; 
LOOP
        FETCH c1 INTO rtotal,riid;
        EXIT WHEN c1%NOTFOUND;
        update c_load set assigned_no=rtotal where iid=riid; ----will update the table-
        DBMS_OUTPUT.PUT_LINE('total  '||rtotal||' instuctorid '||riid);
end loop;
close c1;
END;
/



----execution----
Begin			----execution will give the positive ans---
dbms_output.put_line('record is');
show_course(2019,'Fall');
end;
/




---Feature 10----

create or replace PROCEDURE specialPermission (student_id IN number, schedule_id IN varchar2) IS 
PERMISSION_TYPE number; 
   STUDENT_ID_FOUND number;
   schedule_id_found number;
   course_id varchar2(32767);
   rstatus int;
   spermit int;
   studentid int;
   scheduleid varchar(100);
BEGIN 
	select count(*) INTO student_id_found from  student  where sid =student_id;
	select count(*) INTO schedule_id_found from  SCHEDULE  where sch_id =schedule_id;
select distinct c.cid,r_status,sc.sch_id,s.sid into course_id,permission_type,scheduleid,studentid  from student s,schedule sc,course c ,program p,s_registration sr
where sc.cid=c.cid and s.pid=p.pid and p.pid=c.pid and sr.cid=c.cid and schedule_id=sc.sch_id and student_id=s.sid; 
IF student_id_found !=0 or schedule_id_found!=0 THEN 
	INSERT INTO S_PERMIT (SID, SCH_ID, CID, PERMISSION_TYPE) VALUES (student_id , schedule_id , course_id , PERMISSION_TYPE);
ELSe
dbms_output.put_line('Invalid Inputs');
    commit;
   END IF; 
   exception
when no_data_found then
dbms_output.put_line('Invalid Inputs');
END;
/

----execution---
set serveroutput on; 
BEGIN  ---valid output for permission changed to 2 for these inputs
   specialPermission(2, 'SCH004'); 
END; 
/

set serveroutput on; 
BEGIN  ---output when no data  found 
   specialPermission(26, 'SCH001'); 
END;
/ 

set serveroutput on;
---No data found exception
begin
specialPermission(6,'SCH002');
end ;
/

select * from s_permit;





---Feature 11---

create or replace function prerequisi_check(schedule_id in varchar2,student_id in number) return number is
prereqname varchar2(1000);
student_id_found number;
schedule_id_found varchar2(3000);
course_id varchar2(5667);
v_out number;
begin
select count(*) INTO student_id_found from  student  where sid =student_id;
	select count(*) INto schedule_id_found from  SCHEDULE  where sch_id =schedule_id;
select CID INTO course_id from SCHEDULE where sch_id=schedule_id;
select distinct pr.cid into prereqname from student s,schedule sc,prerequisit pr,course c ,program p
where sc.cid=c.cid and s.pid=p.pid and pr.cid=c.cid and  schedule_id=sc.sch_id and p.pid=c.pid and student_id=s.sid ;
if schedule_id_found !=0 and /*schedule_id_found=schedule_id and student_id_found=student_id and */prereqname= course_id then
v_out:=1;
return v_out;
else
v_out:=0;
return v_out;
end if;
exception
when no_data_found then
--dbms_output.put_line('No data found exception');
v_out:=0;
return v_out;
end;
/


-----Execution----

set serveroutput on;  ---valid output
declare 
v_out number;
begin
v_out:=prerequisi_check('SCH003',4);
dbms_output.put_line(v_out);
end;
/

set serveroutput on; --invalid output
declare 
v_out number;
begin
v_out:=prerequisi_check('SCH003',1);
dbms_output.put_line(v_out);
End;
/






---------Feature 13----

create or replace procedure drop_course(student_id in int,schedule_id in varchar)
is
rstatus int;
cour_id varchar(100);
wlpos int;
wlstid int;
wl_pos int;
wl_count int;
sch_size int;
sctn_size int;
begin
select  distinct sch.cid,reg.r_status into cour_id, rstatus from student st,s_registration reg,schedule sch
where st.sid=reg.sid and reg.cid=sch.cid and st.sid=student_id and sch.sch_id=schedule_id;
if rstatus!=0 and rstatus!=1 then
dbms_output.put_line('the student is not registered with that course');
elsif rstatus=0 then
select distinct position into wlpos from wait_list where sid=student_id and sch_id=schedule_id;
delete from wait_list where sid=student_id and sch_id=schedule_id;
dbms_output.put_line('student record is deleted from wait_list table');
update s_registration set r_status=2 where sid=student_id and
cid in (select cid from schedule where sch_id=schedule_id);
dbms_output.put_line('status is updated to dropped for student');
update wait_list set position=position-1
where position >wlpos and sch_id=schedule_id;
elsif rstatus=1 then
select distinct sid into wlstid from wait_list where sch_id=schedule_id and position in
(select min(position) from wait_list where	sch_id=schedule_id );
update s_registration set r_status=1 where sid=wlstid and
cid in (select cid from schedule where sch_id=schedule_id);
dbms_output.put_line('student is enrolled');
select distinct position into wl_pos from wait_list where sid=wlstid and sch_id=schedule_id;
delete from wait_list where sid=wlstid and sch_id=schedule_id;
dbms_output.put_line('student deleted from wait_list table from enrolled to course');
update wait_list set position=position-1
where position >wl_pos and sch_id=schedule_id;
end if;
select count(*) into wl_count from
wait_list wl,schedule sch,student st
where  wl.sch_id= sch.sch_id and wl.sid=st.sid and sch.sch_id=schedule_id;
if wl_count=0 then
select distinct capacity into sch_size from schedule sch, section sec
where sch.section_id=sec.section_id and  sch_id=schedule_id;
select distinct csize into sctn_size from schedule sch, section sec
where sch.section_id=sec.section_id and sch_id=schedule_id;
if sch_size>sctn_size then
update course set status=1 where cid in (select cid from schedule where sch_id=schedule_id);
dbms_output.put_line('course is now open');
end if;
end if;
exception 
when no_data_found then
dbms_output.put_line('Data Exception error');
end;
/

----execution----
set serveroutput on;
exec drop_course(1,'SCH001');   
exec drop_course(2,'SCH004');		-----invalid output---
exec drop_course(5,'SCH002');
exec drop_course(3,'SCH003');

select * from wait_list;
select * from s_registration;



---Feature 15---

create or replace procedure feature15 (d_id in varchar, yr in number, sem in varchar)
is
cursor c1 is select c.section,c.cid,c.cname,sch.section_id,count(r_status) as stu_enr_wl 
              from schedule sch,course c,program p,department d,wait_list wl,s_registration r
              where sch.cid=c.cid and p.pid=c.pid and p.did=d.did and sch.sch_id=wl.sch_id and 
              sch.sch_id=r.sch_id and r.sch_id=wl.sch_id and year=yr and semester=sem and 
			  r.r_status in (1,0)and d.did=d_id group by c.section,c.cid,c.cname,sch.sid;
total_courses int;
total_stu int;
no_sec course.section%type;
c_id course.cid%type; 
c_name course.cname%type;
se_id schedule.section_id%type;
no_stu_enrl_wl int;
v_count int;
begin
 select count(*) into v_count from department where did=d_id;
  if v_count=0 then
   dbms_output.put_line('Invalid department ID');
  else 
 select count(r.sid)into total_stu from schedule sch,course c,program p,department d,s_registration r,wait_list wl
   where sch.cid=c.cid and p.pid=c.pid and p.did=d.did  and  sch.sch_id=wl.sch_id and r.sid=wl.sid and
    sch.sch_id=r.sch_id and r.r_status =1 and sch.year=yr and sch.semester=sem and d.did=d_id having count(*)>=1;
	dbms_output.put_line('Total number of students enrolled to at least one course for year : '||yr||' and semester : '||sem||' is '||total_stu);
      open c1;
	   select count(c.cid) as total_cour into total_courses from course c,program p,department d,schedule sch
       where c.pid=p.pid and d.did=p.did and sch.cid=c.cid and year=yr and semester=sem;
        loop 
		 fetch c1 into no_sec,c_id,c_name,se_id,no_stu_enrl_wl;
		 exit when c1%notfound;
		  dbms_output.put_line('Total number of courses is : '||total_courses|| ', course ID is :'||c_id||'course name is :'||c_name||
		  ', section ID is : '||se_id||', number students in enrolled or waitlist status is :'||no_stu_enrl_wl);
		end loop;
	end if;
end;
/	

----execution---
show errors;

exec feature15('IS',2019,'fall');
