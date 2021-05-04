# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

* [`puppet_run_scheduler`](#puppet_run_scheduler): A short summary of the purpose of this class
* [`puppet_run_scheduler::posix`](#puppet_run_schedulerposix): puppet_run_scheduler::posix
* [`puppet_run_scheduler::windows`](#puppet_run_schedulerwindows): puppet_run_scheduler::windows

### Functions

* [`puppet_run_scheduler::minutes`](#puppet_run_schedulerminutes)

### Data types

* [`Puppet_run_scheduler::Run_interval`](#puppet_run_schedulerrun_interval)

## Classes

### <a name="puppet_run_scheduler"></a>`puppet_run_scheduler`

puppet_run_scheduler

A description of what this class does

#### Examples

##### Using a default 30m run interval, you can simply include the class

```puppet
include puppet_run_scheduler
```

##### Parameters exist that can be used to fine-tune exactly how the runs are scheduled

```puppet
class { 'puppet_run_scheduler':
  run_interval => '4h',
  splaylimit   => '1h',
  start_time   => '16:00',
}
```

#### Parameters

The following parameters are available in the `puppet_run_scheduler` class:

* [`ensure`](#ensure)
* [`run_interval`](#run_interval)
* [`start_time`](#start_time)
* [`splaylimit`](#splaylimit)
* [`posix_puppet_executable`](#posix_puppet_executable)
* [`windows_puppet_executable`](#windows_puppet_executable)

##### <a name="ensure"></a>`ensure`

Data type: `Enum['present', 'absent']`

Whethor or not to schedule the running of puppet. "absent" only exists to
provide clean-up or rollback options in case the class is applied somewhere
it shouldn't have been.

Default value: `'present'`

##### <a name="run_interval"></a>`run_interval`

Data type: `Puppet_run_scheduler::Run_interval`

What frequency Puppet should run at. This value cannot be any period; there
is an enumerated list of acceptable values.
Valid values: 15m, 30m, 1h, 2h, 3h, 4h, 6h, 8h, 12h, 24h

Default value: `'30m'`

##### <a name="start_time"></a>`start_time`

Data type: `Pattern[/[0-2]\d:\d\d/]`

A specific time in the form of HH:MM that a Puppet run should start (
subject to the `splaylimit` parameter). This is useful for organizations
with long run intervals and specific maintenance windows. For example,
given a `run_interval` of 4h and a `splaylimit` of 30m, administrators can
use `start_time` to ensure that Puppet runs occur during the first 30
minutes of a known maintenance window.

Default value: `'00:00'`

##### <a name="splaylimit"></a>`splaylimit`

Data type: `Puppet_run_scheduler::Run_interval`

Same format as `run_interval`. How long a period of time to spread runs out
over. By default runs will be fully spread out over the entire
`run_interval`, but it is possible to have a shorter `splaylimit`.

Default value: `$run_interval`

##### <a name="posix_puppet_executable"></a>`posix_puppet_executable`

Data type: `Stdlib::Absolutepath`

The fully qualified path to the Puppet executable to run on Posix systems.
All of the Puppet command-line arguments appropriate for perfoming a
one-time run will be passed to this executable.

Default value: `'/opt/puppetlabs/bin/puppet'`

##### <a name="windows_puppet_executable"></a>`windows_puppet_executable`

Data type: `Stdlib::Absolutepath`

The fully qualified path to the Puppet executable to run on Windows
systems. All of the Puppet command-line arguments appropriate for perfoming
a one-time run will be passed to this executable.

Default value: `'C:\\Program Files\\Puppet Labs\\Puppet\\bin\\puppet.bat'`

### <a name="puppet_run_schedulerposix"></a>`puppet_run_scheduler::posix`

puppet_run_scheduler::posix

#### Parameters

The following parameters are available in the `puppet_run_scheduler::posix` class:

* [`puppet_executable`](#puppet_executable)

##### <a name="puppet_executable"></a>`puppet_executable`

Data type: `Stdlib::Absolutepath`

The fully qualified path to the Puppet executable to run on Posix systems.
All of the Puppet command-line arguments appropriate for perfoming a
one-time run will be passed to this executable.

Default value: `$puppet_run_scheduler::posix_puppet_executable`

### <a name="puppet_run_schedulerwindows"></a>`puppet_run_scheduler::windows`

puppet_run_scheduler::windows

#### Parameters

The following parameters are available in the `puppet_run_scheduler::windows` class:

* [`scheduled_task_user`](#scheduled_task_user)
* [`puppet_executable`](#puppet_executable)
* [`manage_lastrun_acls`](#manage_lastrun_acls)
* [`scheduled_task_password`](#scheduled_task_password)

##### <a name="scheduled_task_user"></a>`scheduled_task_user`

Data type: `String[1]`

The user to run the Puppet run scheduled task as.

Default value: `'system'`

##### <a name="puppet_executable"></a>`puppet_executable`

Data type: `Stdlib::Absolutepath`

The fully qualified path to the Puppet executable to run on Windows
systems. All of the Puppet command-line arguments appropriate for perfoming
a one-time run will be passed to this executable.

Default value: `$puppet_run_scheduler::windows_puppet_executable`

##### <a name="manage_lastrun_acls"></a>`manage_lastrun_acls`

Data type: `Boolean`

Whether or not to manage acl entries on Puppet lastrun files, to work
around [PUP-9238](https://tickets.puppetlabs.com/browse/PUP-9238).

Default value: ``true``

##### <a name="scheduled_task_password"></a>`scheduled_task_password`

Data type: `Optional[Variant[String[1], Sensitive[String[1]]]]`

The password for the user to run the Puppet run scheduled task as. Only
used if specifying a user other than "system" via `scheduled_task_user`.

Default value: ``undef``

## Functions

### <a name="puppet_run_schedulerminutes"></a>`puppet_run_scheduler::minutes`

Type: Puppet Language

The puppet_run_scheduler::minutes function.

#### `puppet_run_scheduler::minutes(Puppet_run_scheduler::Run_interval $value)`

The puppet_run_scheduler::minutes function.

Returns: `Any`

##### `value`

Data type: `Puppet_run_scheduler::Run_interval`



## Data types

### <a name="puppet_run_schedulerrun_interval"></a>`Puppet_run_scheduler::Run_interval`

The Puppet_run_scheduler::Run_interval data type.

Alias of

```puppet
Enum['15m', '30m', '1h', '2h', '3h', '4h', '6h', '8h', '12h', '24h']
```
