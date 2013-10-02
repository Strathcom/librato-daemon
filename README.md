# librato-daemon

Python deamon that sends system information to librato metrics. Uses [psutil] 
internally to gather information about the system. Currently sends:

 * `system.cpu_percent`
 * `system.ram_percent`
 * `system.swap_percent`
 * `system.disk_percent`
 * `system.network_in` (counter)
 * `system.network_out` (counter)

## Installation

```
$ pip install libratod
```

or clone this repository and run:

```
librato-daemon/$ pip install .
```

## Running

Once installed, you can run `libratod` from  the command line:

```
$ libratod &
```

although the daemon will crash occasionally, so you may want to use [supervisor](http://supervisord.org/) to manage the process. An example setup might look like this:

```
[program:libratod]
command=libratod
environment=LIBRATO_EMAIL=<email-address>,LIBRATO_API_KEY=<api-key>,LIBRATO_INTERVAL=30
process_name=libratod
autostart=true
autorestart=true
startsecs=5
startretries=3
stopwaitsecs=10
stdout_logfile=/var/log/supervisor/%(program_name)s_stderr.log
stderr_logfile=/var/log/supervisor/%(program_name)s_stderr.log

```

Then start the program with:
```
$ sudo supervisorctl start libratod
```


## Configuration

Set or override any of the following in your environment before running `libratod`.

`LIBRATO_EMAIL` Your Librato email address (required).

`LIBRATO_API_KEY` Your Librato [API Key](https://metrics.librato.com/account#api_tokens)

`LIBRATO_INTERVAL` (default `60`) The interval at which metrics are sent off to 
Librato.

`LIBRATO_HOSTNAME` (defaults to the machine's hostname) The value to send as
the `source` to Librato.

## Contributing

Pull requests and feedback welcome. 


