# Graylog
My collection of Graylog tips, tricks, warnings, cautions and lessons learned.

## Field Names

**Do Not Use:**
- `syslog_*`

> Recently when building some parsers I was receiving a log like this on a > "Plain Text/RAW" input.
>```
><27>Nov 29 15:05:42 blah blah blah msg msg msg
>```
>I was trying to parse out the number from between the left and right arrows, which is the Syslog Priority value and put it in a field named: `syslog_priority`. This wasn't working. After hours of futtsing with it, it was determined that the cause of the failures was when I started a field name with `syslog_`. I tested and tested and got the same results with each test: any time `syslog_` was in the field name the pipeline rule wouldn't work.
>
>**Assumption:** I'm sure this is because how *syslog* messages are recieved and processed under the hood, but I can not confirm that.