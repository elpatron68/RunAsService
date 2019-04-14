# RunAsService
RunAsService is a command line tool that allows you to setup a regular  console application to run as a service.

This tool requires that .NET Framework 2.0 be already installed on your computer.
If you do not have .NET Framework 2.0 this tool will display a message and not run.
You probably already have the .NET Framework 2.0 but if you don't you can download 
it here: Microsoft Download Center

IMPORTANT: Any services you install using this tool will
require that this tool remain on that computer in the same
location in order for those services to continue functioning. Therefore
before installing any services you should make sure this tool is
somewhere where it can remain permanently. If you do end up moving
this tool use the 'fixservices' action to fix the existing services.
(details on how to use 'fixservices' can be found below)

## Usage

`RunAsService`

Typing just the name of the tool without specifying any parameters 
or specifying incorrect parameters will bring you to the help screen.

### Install Service

`RunAsService install [Name] [Display Name] PathToExecutable`
        
#### Name

The name of the service, if none is specified the name 
will default to the name of the executable.

You might choose to give it a different name than 
the executable to keep some kind of existing convention, 
make it friendlier or make it easier to use commands like 
`net start` and `net stop`
    
#### Display Name

This is how the service name will be displayed in the windows 
services list. If no display name is specified it will default 
to Name, if Name is not specified, it will default to the name 
of the executable.

Generally the display name is longer and more descriptive 
than the name and gives the user a better idea of what 
the service is and/or does.

#### PathToExecutable

The location of the application you want to run as a service. 

Note, the tool will check if this executable exists, if it 
doesn't find it will not install it.

#### Arguments

Anything behind PathToExecutable will be treated as command 
line arguments handed to the executable.


### Uninstall Service

`RunAsService uninstall Name`
 
#### Name

The name of the service you would like to uninstall.

### Fix Service

`RunAsService fixservices`

Use this action when you've moved the RunAsService executable. 

Services installed using RunAsService require that RunAsService 
remain on the computer and at the same location if 
you move it the services will stop working, use this 
action to fix that.

## EXAMPLES


### Install Myapp as a service called "Myapp"

`RunAsService install "c:\my apps\Myapp.exe"`
    
### Install Myapp as a service called "My Service"

`RunAsService install "My Service" "c:\my apps\Myapp.exe"`

### Install Myapp as named service (with command line arguments handed to MyApp)

`RunAsService install "My Service" "c:\my apps\Myapp.exe" "-arg1 value -arg2 1"`


### Installs Myapp as a named service with description

Installs Myapp internally called "My Service" when using commands like `net start` and `net stop` and shows up as "My Super Cool Service" in Window's services list.

`RunAsService install "My Service" "My Super Cool Service" "c:\my apps\Myapp.exe"`

### Uninstalls the service
        
`RunAsService uninstall "My Service"`

### Fix Services

Use this action if you move this tool. This is because services
installed using this tool rely on this tool remaining on that 
computer and at the same location. If you do not call 'fixservices' 
after moving this tool the existing services installed using this tool will stop functioning.

`RunAsService fixservices`

## NOTES

You can use Windows built in commands to start and stop your services. For example you can use:

`net start "My Service"`
        
and

`net stop "My Service"`
    
Where "My Service" would be replaced with the name of your service.
