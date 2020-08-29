# Ticket-analysis
The Ticket Analysis visualization provides a breakdown of the different types of tickets being submitted to your help desk.
Ticket categories may include ticket type, priority level, assigned agent, and ticket source. 
This analysis is designed to uncover trends behind tickets being submitted to and measure
the Agent Performance KPI of help desk agents by tracking how they perform on key metrics, such as call handled,
first-call resolution, and customer sentiment. This KPI is used to identify which help desk agents are performing well,
and which ones are performing unsatisfactory. 


##########-->>CODE
data tkt;
set sasuser.ticket_all;
run;


data tkt_open1;
set sasuser.ticket_all;
if status="Open";
run;


proc sql;
select count(status) as count from sasuser.ticket_all;
quit;


proc sql;
create table a as select category ,count(*) as count from sasuser.ticket_all group by category;
quit;


proc gchart data =work.a;
vbar3d category/sumvar=count;
title "category vs count";
run;

proc sql;
create table B as  select AgentName,status, count(*) as count from work.Abc group by AgentName;
quit;

proc sql;
select AgentName,Status, count(*) as count1 from work.B group by AgentName, Status;
quit;


data sasuser.tkt_new;
set abc;
run;


data EY1 ;
set work.EY;
where agentname eq '' then agentname="vijay1";
run;

proc sql;
create table wef as select AgentName, count(*) as count from work.EY1 group by AgentName;
quit;  


PDF output using ODS statement-

ods pdf file="C:\Documents and Settings\sasadm\Desktop\tkt.pdf";
proc print data=work.Ey1;
proc sql;
select AgentName, count(*) as count from work.EY1 group by AgentName;
quit;  
run;
ods pdf close;



##########

SCRIPT-->>
I used to get a weekly/monthly/ file which contains data of tickets which is
raised to our concerned team to resolve.

I used to create reports and dashboard from the given data like-

Agent wise count of ticket.
category wise count of ticket.
total open/closed
open and closed time difference


LOAD ANALYSIS-

These reports helps to understand the ticket flow in our helpdesk and help us 
with allocating resources accordingly.


####

1.The ticket analysis visualisation provides a break down of the different type of 
  tickets being submitted to our helpdesk.

2.Ticket analysis was designed to uncover the trends behind tickets being submitted.


For Ex-
if a high no tickets are submitted are marked "TRAINING" it indicates that 
client needs training .

it helps in reducing the no of tickets that can be answered by other means such as
documentation.


AGENT PERFORMANCE-

Measuring the performance of helpdesk agents according to key matrices.

KPI-




ADHOC-

At the time of meeting with client they provide me the whole tickets
of the client till date and after that we analyse it and see the ticket trends.





Questions-
1. Find the number of Ticket raised Monthly/Yearly
2. Find the number of different types of tcikets
3. Number of tickets solved by each agents in a month
4. Calculate tcikets turnaround time for each cataegory
5. Number of open tickets in a months 
6. Largest turnarount time for each category
7. Least time taking tickets for eac category
8. Graphical represenation of different tickets for a year and month wise
9. Escalated tickets with types


 

