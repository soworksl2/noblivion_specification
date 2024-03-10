The todo item is a bunch of components some required and others no, that are separated by at least 1 blank spaces. e.g.

```
[component] [component];
```

or

```
[component]
[component];
```

it can even be mixed

```
[component] [component]
[component];
```

at the end, it should be ended with a ';'

before the ';' can contain a children block that will contains items as child of the specified todo, that block start with '{' and end with '}'. e.g.

```
[component] [component] {...};
```

or

```
[component] [component] {
    ...
};
```

notice that the content inside the children block no need to be indented.

# The Todo Label

The Todo label should be embraced with the '#' symbol and a space between the symbol and the label. e.g.

```
[data] [data] [data] # this is the label of my todo # [data] [data];
```

ignore the '[data]' for now it represent possible data that will be specified forward.

right now to keep the things simple the '#' symbol is not allowed in the label but it could change in the future if necessary.

the text of the label will be exactly the same of the text inside the '# ... #'. there is not scaped characters or somethig like that.

the label is mandatory in a Todo Item.

# mark as completed

there are multiple way to mark a task as completed.

The first method is to add a lowercase 'x' as the first component of the Todo. e.g.

```
x [data] [data] # some task to do # [data] [data];
```

if the Todo item does not have an x at start it will be interpreted as not completed.

the problem with this method is that all the Todo Items will be unordered if edited manually. and the incompleted Todo would be merged with the completed ones.

the second method comes to fix that. and it consists of split the file with at least 3 '-' or more. the top part represent uncompleted Todos items and the bot part the completed ones. e.g.

```
# a todo not completed yet #;
---
# a completed todo #;
```

technically, the file should contain a line with nothing more than blank spaces or '-' and it needs at least 3 '-' to be considered the divisor. e.g.

```
#one todo#;
  - -    -
#another todo#;
```

that way if you wanna mark manually a todo as complete and want to keep an order you simple need to delete the todo from the top and paste it in the bottom.

in the bottom part no matters if the 'x' is specified at the start of the todo or not it will ever be interpreted as completed. both method could be used together.

if the bottom part or the 3 '-' has been not specified, it should be interpreted as if a default one exist at the end of the file with 0 todos items.

# short description

the short description is an optional component of the Todo item, it is specified between two pairs of the '\`' symbol. e.g.

```
# my beautiful todo # `this is my beautiful todo`;
`the description first` #what a weird todo#;
```

it can be multiline like:

```
#give example of multiline description# `something
beautiful`;

---

#completed todo here#
`the descrition can start here also
and contain multilines`;

#todo todo todo#
    `indented todo description also
    isn't it cool`;
```

in the case of multilines description is recomended start in the line below, that way the indentation can be supressed.

```
#another example#
    `hello my nice
    friend.`;

#a generic todo example#
    `this is not indented but
     the second line will start with a space`;
```

the text of each description respectively will be.

```
hello my nice
friend.

this is not indented but
 the second line will start with a space
```

NOTE: this component should be eliminated of the specification because the label itself can act as a description. should be rethinked.

# tags and properties

a tag or properties are like the metadata of the todo item it should be inside '(' and ')' and have a key, an optional value specifier and an optional value.

the key is any alphanumeric and '\_' combination that does not start with '\_'. the value specifier can be one of ('=', =#, =:, =;) and the value depends on the value specifier. e.g.

```
#make this or that# (my_life);
#homework of math# (priority=#2);
#A Normal todo#;
```

the first todo have a tag named 'my life' without any value, the second one has a tag named 'priority' with a number value of 2 and the last one does not have any tag.

inside the parenthesis you can specify multiples tags and values separated by commas or simple start another pairs of parenthesis. e.g.

```
#give some nice example# (my_project, priority=#1);
#play some games# (rest) (priority=#2);
```

if the same tags appears in the same todo item the last one override the first, from left to right, if the last does not have value and the first does the value of the first is deleted.

this rule is broken for some built-in tags that will be covered later. in those cases instead of override the last value will be appended to the first one. if the last one does not have a value then all values will be deleted. the separator is ';'. e.g.

```
#pay insurance# (_reminder=;2024-4-15; 2024-4-16);
#pay insurance 2# (_reminder=;2024-4-15) (_reminder=;2024-4-16);
#pay insurance 3# (_reminder=;2024-4-15) (_reminder);
```

here the first todo will have a tag named '\_reminder' (the '\_' is allowed here because reminder is a built-in tag) with a value of '2024-4-15; 2024-4-16', the same for the second todo, but the last one will not have a value.

## value specifiers

the only value specifiers that can contain multiple values is the '=;'.

the '=' value specifiers means text and can handle any text with spaces included except the character ',' because it is used to separate tags.

the '=#' means number and it can handle any number including decimals, if other thing is specified then the todo tag is invalid and it is not saved.

the '=:' means datatime it can handle a simple date time with the format specified in this specification.

the '=;' means datetime function it can handle multiples datetime functions or simple datetimes separated with ';'. e.g.

```
#implement references# (_rm=;2024-3-15:1m; 2024-3-26);
```

see datetimes and datetimes functions format in this specification.

## Built-in tags

the built-in tags are:

\_cre or \_creation (=:) specify the creation datetime of the todo item.

\_due (=:) specify the due datetime of the todo item.

\_rm or \_reminder (=;) specify datetimes to reminder the todo item. it appends on repeat

\_nrm or \_noreminder (=;) specify datetimes to exclude to the reminder.

\_adj or \_adjunt (=) specify a text with a reference format separated with ; of files to adjunts, it append on repeat.
