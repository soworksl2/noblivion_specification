# datetimes

datetimes has the following formats:

first of all the structure ever will be (year-month-day hour:minutes:seconds [PM | AM]). but there are a lot of variations.

the year ever should be written comple, the month and day can or not contain a starting '0'. e.g.

```
2024-7-5
2024-07-05
```

the hour will be ever 24 hour format unless that 'AM' or 'PM' is specified at the end. in that case the hour is 12 hour format. e.g.

```
13:05
01:05 PM
```

the case does not matter in 'PM' or 'AM'. and trailing '0's are not mandatory.

in a datetime if a time is not present it will be implicitly '00:00:00'. At least for now it does not have a timezone. so, it will ever be in the local time zone.

the time cannot be specified alones, it needs at least the day being specified first.

in a todo item, if some part of the date does not appear, it will get it from the (\_cre) tag. e.g.

```
(_cre=:2024-5-12) #dates in todo# (_rm=:15 9AM)
```

the actual value of the remainder will be interpreted as '2024-5-15 9:00:00 AM'

some examples to make this part clear are here:

```
2025-1-1
1-1         //first of january, the year is implicit and depends on _cre
1           //day 1, the month and year are implicit
2026        //Invalid, if you wanna specified the year, you have to follow the order year-month-day

1 9         //day 1 at 9 AM, the year and month are implicit.
1 13        //day 1 at 1 PM
1 2PM       //day 1 at 2 PM
1 2 PM      //the same
1 13:15     //day 1 at 1:15 PM
1 1:15:55PM //The same above, but as 12 hour format and with seconds
```

# datetime functions

the datetime functions are an structure that match over multiple dates simultaneosly. that is util for create todos or events that repeat over time.

it has 3 parts each one separated with a ':', they are:

'start:step:stop'

the start part and the stop part are simple datetimes and follows the same rules specified above.

if the start is not specified it will be the \_cre tag if stop is not specified it will be the last possible value for the part that was not specified part. for example if you do not specify a stop at all, it will be until the end, if you do not specify the hour it will be 23, so on.

the step part is a spantime that are written with a number and a time specifier. they are.

ss -> seconds
mm -> minutes
hh -> hour
d -> day
m -> month
y -> year

there are also some specifiers that means the next time it happens for example 'ws' stand for '*w*eek *s*unday' and means the next sunday. they are:

wm -> monday
wtu -> tuesday
ww -> wednesday
wth -> thursday
wf -> friday
wsa -> saturday
wsu -> sunday

fm -> the next first day of month. if already in the first day of the month or later, go to the first day of the next month.
lm -> the last day of the month. equals to fm

jan -> first day of month of january
feb -> first day of month of february
mar -> first day of month of march
apr -> first day of month of april
may -> first day of month of may
jun -> first day of month of june
jul -> first day of month of july
aug -> first day of month of august
sep -> first day of month of september
oct -> first day of month of october
nov -> first day of month of november
dec -> first day of month of december

they should be specified as the end of the step.

you can imagine the step as a finger moving the steps specified and marking the datetime. when there are no more steps specified it start moving with the specified steps again from the start until the stop is reached.

a '.' at the end of a time specifier can be interpreted as only move the finger but do not mark anything.

a ',' at the end can be interpreted as move the finger and mark the datetime under the finger but then return to the position you was before.

some examples using datetime functions:

```
:1d:        //it means every day starting from _cre datetime.
:2m:        //each two months
:1wsa1wsu:  //each saturday and sundays.
:1wsu1wsa:  //each saturday and sunday, but the first saturday will be ignored.
:1m1wsa,:   //each month in saturday
:2wsa:      //each two saturday, or 1 saturday yes 1 saturday no.
15:1m:      //each 15 of each month.
```

also in the step part you can add a '[...]' at the end and inside put another datetime function. but this one instead of mark the datetime will unmark the marked ones. e.g.

```
:1d[1wsa1wsu]:  //weekdays, without saturday or sunday.
```
