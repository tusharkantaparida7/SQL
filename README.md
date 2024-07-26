# SQL
SQL is a powerful tool used for managing and manipulating relational databases. When integrated with Git, a distributed version control system, it allows developers and data professionals to track changes in SQL scripts and database schema efficiently. 


--find 2nd highest annual_income ?--
select max(annual_income) from bank
where annual_income<(select max(annual_income) from bank)

--find 3rd highest annual_income ?--
select top 1 * from
(select  top 3 * from bank
order by annual_income desc) result
order by annual_income

--find 7th highest annual_income ?--
with RESULTS as
(select *, DENSE_RANK() over(order by annual_income desc) as x from bank)
select * from RESULTS
where RESULTS.x=7;

--Create a Table--
create table IPL
(
Team varchar(15),
Team_Name varchar(45)
);

--Insert Values in it--
insert into IPL values
('CSK','Chennai Super King'),
('DC','Delhi Capital'),
('GT','Gujrat Titans'),
('KKR','Kolkata Night Riders'),
('LSG','Lucknow Super Giants'),
('MI','Mumbai Indians'),
('PBKS','Punjab Kings'),
('RR','Rajasthan Royals'),
('RCB','Royal Challenger Banglore'),
('SRH','Sun Risers Hydearabad');

--Read the Table Data--
Select * from IPL

--Above table having 10 IPL teams, Write a sql query such that each team play with every other team just once--
With Matches as
(select ROW_NUMBER() over (order by Team_Name)as ID,Team, Team_Name from IPL I)
select t.Team_Name as Teams,o.Team_Name as Opponent from Matches t
Join
Matches o
on
t.id < o.id
order by t.Team_Name;

