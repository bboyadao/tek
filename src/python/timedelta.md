There are so many error caused by datetime. So I decided to write this article. 

Determine exact date and time with `timedelta`\
`timedelta` does not support year right?\
that why we have to do more calculate\
Let's use python built-in package `calendar`.

```python
import calendar
from datetime import datetime

days = 366 if calendar.isleap(datetime.now().year) else 365
``` 
For some details: send email hapy birthday for next year, count down event day, billing stuff, etc...
Everything works fine if this year not leap.\
What if I send an email happy new year on the day at the end of the year before?


