# Ticket-analysis
The Ticket Analysis visualization provides a breakdown of the different types of tickets being submitted to your help desk.
Ticket categories may include ticket type, priority level, assigned agent, and ticket source. 
This analysis is designed to uncover trends behind tickets being submitted to and measure
the Agent Performance KPI of help desk agents by tracking how they perform on key metrics, such as call handled,
first-call resolution, and customer sentiment. This KPI is used to identify which help desk agents are performing well,
and which ones are performing unsatisfactory. 


####
CODE-


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




PDF-


ods pdf file="C:\Documents and Settings\sasadm\Desktop\tkt.pdf";
proc print data=work.Ey1;
proc sql;
select AgentName, count(*) as count from work.EY1 group by AgentName;
quit;  
run;
ods pdf close;



