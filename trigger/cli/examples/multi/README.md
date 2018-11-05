
# Multi-Command Example
This example shows how to configure the CLI trigger to run as a cli with multiple commands. Help and version commands are automatically generated for multi-command CLIs.

## Configuration
```json
{
 "triggers": [
     {
       "id": "cli",
       "type": "cli",
       "name": "simple",
       "description": "Simple CLI Utility",
       "settings": {
         "use":"<command>",
         "long":"A simple cli using flogo"
       },
       "handlers": [
         {
           "name":"test1",
           "settings": {
             "use":"[flags] [args]",
             "short": "test command",
             "long": "the test command",
             "flags": [
               "flag1||||the first value flag",
               "flag2||false||the first bool flag"
             ]
           },
           "action": {
             "type": "flow",
             "settings": {
               "flowURI": "res://flow:command1"
             },
             "input" :{
               "flags":"=$.flags",
               "args":"=$.args"
             }
           }
         },
         {
           "name":"test2",
           "settings": {
             "use":"[flags] [args]",
             "short": "test2 command",
             "long": "the test2 command",
             "flags": [
               "flag1||||the first value flag",
               "flag2||false||the first bool flag"
             ]
           },
           "action": {
             "type": "flow",
             "settings": {
               "flowURI": "res://flow:command2"
             },
             "input" :{
               "flags":"=$.flags",
               "args":"=$.args"
             }
           }
         }
       ]
     }
   ]
 }
```


### Help
General Help: `cli help`
```
A simple cli using flogo
Usage:
    cli <command>

Commands:
    test1        test command
    test2        test2 command
    help         help on command
    version      prints cli version
```

Command Help: `cli help test1`

```
the test command
Usage:
   cli test1 [flags] [args]

Flags: 
   -flag1 string        the first value flag
   -flag2               the first bool flag
```