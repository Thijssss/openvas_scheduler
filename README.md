Description:
OpenVAS task scheduler script for gvm-pyshell (part of the gvm-tools package)
This script is used to start tasks which haven't run in over a month.
Use the gvm get_tasks() method to read in XML information about all the tasks.

Release date:
17-04-2018

Version:
1.11

Authors:
Thijs Stuurman <thijs.stuurman@internedservices.nl>

Required packages:
python3-urwid python3-dateutil

Run example (works great inside a screen session):
gvm-pyshell tls --hostname 127.0.0.1 --port 9390 --gmp-username admin \
--gmp-password xxx ./scheduler.gmp

Limitations:
The scheduler will not assign tasks to other (slave) scanners. In the authors
case the (slave) scanner assignment per task is done beforehand on network
reachability.

Changelog:
v1.11: Fixed a bug caused by having more tasks running than the max
v1.10: Added a filter to not schedule tasks with NOSCHED in their name
v1.00: Initial Release

Additional information:
 - loopTimerSeconds = 60
   Seconds to wait untill checking task information to try and run new tasks if
   resources are available
 - maxTasksPerSlave = 2
    Number of tasks a (slave) scanner may run concurrently; 2 seems to work out
    ok in practice
 - "monthOld = datetime.today() + relativedelta(months=-1)"
    The code line which decides if a task should run. This can be adjusted to
    your own needs. (daily? weekly?...)
 - see daysEnabled, hourStart and hourStop to customize task starting constraints

Future work:
 - Make better use of urwid to create a nicer GUI
   (progress bars, better layout...)
 - Use task last_report start and end information to calculate estimated runtime
   of the task and to-run tasks
 - Clean up code
