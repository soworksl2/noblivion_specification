first of all the top directory should be marked as a noblivion directory putting a '.noblivion' file in there. in that folder you can put any files you want.

the '.noblivion' file will contain the options and preferences for any client that use this specification. the file should be a TOML file. each client should be in its own namespace.

the 'core' namespace is reserved for future standar option or preferences.

# files for todos
a file behave as a collection of todo, but it should end with the '.tds' extension that stand for *T*o*D*o*S* you can also create those file inside of subdirectories recursively.

# references

a reference can be marked starting with an '@' and the content enclosed in '[' and ']'. e.g.

```
#reference tutorial# (_adj=@[pics/wedding_day.jpeg]);
#another reference# (my_custom_tag=a text with a tag @[files/wiki.txt]);
```

the file will be searched in the top directory where the '.noblivion' file is located.

you can specify an url instead putting a '+' before opening the brackets. e.g.

```
#a link# (_adj=@+[linkedin.com/in/jimy-aguasviva-781b32200/]);
```
