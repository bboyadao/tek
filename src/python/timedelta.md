There are so many errors caused by datetime. So I decided to write this article.

Determining the exact date and time with `timedelta`\
`timedelta` does not support years, right?\
That's why we have to do more calculations.\
Let's use Python's built-in package `calendar`.

```python
import calendar
from datetime import datetime

days = 366 if calendar.isleap(datetime.now().year) else 365
``` 
For some details: send a happy birthday email for next year, count down to event day, billing stuff, etc.\
Everything works fine if this year is not a leap year.\
What if I send a happy new year email on the day at the end of the year before?


