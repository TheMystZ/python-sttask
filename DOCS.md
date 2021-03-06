# DOCUMENTATION FOR STTASK!

## Contents

- [sttask](#sttask)
  - [TaskOwner](#sttask.taskowner)
    - [sttask.TaskOwner.tasks: list](#sttask.taskowner.tasks)
    - [sttask.TaskOwner.scheduled: list](#sttask.taskowner.scheduled)
    - [sttask.TaskOwner.add(name: str, func, args: tuple = ()) -> int](#sttask.taskowner.add)
    - [sttask.TaskOwner.task_list() -> list](#sttask.taskowner.task_list)
    - [sttask.TaskOwner.schedule_list() -> list](#sttask.taskowner.schedule_list)
    - [sttask.TaskOwner.update() -> None](#sttask.taskowner.update)
    - [sttask.TaskOwner.grab_task(name: str) -> int](#sttask.taskowner.grab_task)
    - [sttask.TaskOwner.grab_schedule(name: str) -> int](#sttask.taskowner.grab_schedule)
    - [sttask.TaskOwner.schedule(name: str, func, time: int = 0, args: tuple = ()) -> int](#sttask.taskowner.schedule)
    - [sttask.TaskOwner.play(task: str) -> None](#sttask.taskowner.play)
    - [sttask.TaskOwner.pause(task: str) -> None](#sttask.taskowner.pause)
    - [sttask.TaskOwner.name_set(task: str, name: str) -> None](#sttask.taskowner.name_set)
    - [sttask.TaskOwner.update_set(task: str, func) -> None](#sttask.taskowner.update_set)
    - [sttask.TaskOwner.args_set(task: str, args: tuple) -> None](#sttask.taskowner.args_set)
    - [sttask.TaskOwner.grab_output(task: str)](#sttask.taskowner.grab_output)
    - [sttask.TaskOwner.pop_task(task: str) -> None](#sttask.taskowner.pop_task)
    - [sttask.TaskOwner.play_schedule(schedule: str) -> None](#sttask.taskowner.play_schedule)
    - [sttask.TaskOwner.pause_schedule(schedule: str) -> None](#sttask.taskowner.pause_schedule)
    - [sttask.TaskOwner.name_set_schedule(schedule: str, name: str) -> None](#sttask.taskowner.name_set_schedule)
    - [sttask.TaskOwner.update_set_schedule(schedule: str, func) -> None](#sttask.taskowner.update_set_schedule)
    - [sttask.TaskOwner.args_set_schedule(schedule: str, args: tuple) -> None](#sttask.taskowner.args_set_schedule)
    - [sttask.TaskOwner.pop_schedule(schedule: str) -> None](#sttask.taskowner.pop_schedule)
  - [Task](#sttask.task)
    - [sttask.Task.name](#sttask.task.name)
    - [sttask.Task.update](#sttask.task.update)
    - [sttask.Task.paused](#sttask.task.paused)
    - [sttask.Task.args](#sttask.task.args)
    - [sttask.Task.output](#sttask.task.output)
  - [Schedule](#sttask.schedule)
    - [sttask.Schedule.name](#sttask.schedule.name)
    - [sttask.Schedule.update](#sttask.schedule.update)
    - [sttask.Schedule.paused](#sttask.schedule.paused)
    - [sttask.Schedule.args](#sttask.schedule.args)
    - [sttask.Schedule.time](#sttask.schedule.time)
  - [sttask.end: int](#sttask.end)
  - [sttask.pause: int](#sttask.pause)
- [utils](#sttask.utils)
  - [sttask.utils.convert(task, \*, schedule_time: int = 0)](#sttask.utils.convert)

<a name="sttask"></a>
## sttask

|   Value   | Type | Default |
|:---------:|:----:|:-------:|
| TaskOwner | type | *class* |
|    Task   | type | *class* |
|  Schedule | type | *class* |
|    end    |  int |    1    |
|   pause   |  int |    2    |

The main module

<a name="sttask.taskowner"></a>
### sttask.TaskOwner

|        Value        |   Type   |   Default  |
|:-------------------:|:--------:|:----------:|
|        tasks        |   list   |     []     |
|      scheduled      |   list   |     []     |
|         add         | function | *function* |
|      task_list      | function | *function* |
|    schedule_list    | function | *function* |
|        update       | function | *function* |
|      grab_task      | function | *function* |
|    grab_schedule    | function | *function* |
|       schedule      | function | *function* |
|         play        | function | *function* |
|        pause        | function | *function* |
|       name_set      | function | *function* |
|      update_set     | function | *function* |
|       args_set      | function | *function* |
|     grab_output     | function | *function* |
|       pop_task      | function | *function* |
|    play_schedule    | function | *function* |
|    pause_schedule   | function | *function* |
|  name_set_schedule  | function | *function* |
| update_set_schedule | function | *function* |
|  args_set_schedule  | function | *function* |
|     pop_schedule    | function | *function* |

A class for storing and managing tasks.
    
<a name="sttask.taskowner.tasks"></a>
#### sttask.TaskOwner.tasks: list
A list of all the tasks currently in this instance of [sttask.TaskOwner](#sttask.taskowner).
Contains [sttask.Task](#sttask.task) objects.

<a name="sttask.taskowner.scheduled"></a>
#### sttask.TaskOwner.scheduled: list
A list of all the schedules currently in this instance of [sttask.TaskOwner](#sttask.taskowner).
Contains [sttask.Scheduled](#sttask.task) objects.

<a name="sttask.taskowner.add"></a>
#### sttask.TaskOwner.add(name: str, func, args: tuple = ()) -> int

| Argument | Type  | Default |
|----------|-------|---------|
|`name`    |`str`  |         |
|`func`    |       |         |
|`args`    |`tuple`|`()`     |

Created a task called `name` and sets it's update function to `func` and it's arguments to `args`.
Then appends the task to [self.tasks](#sttask.taskowner.tasks).\
Raises a `TypeError` if `name` is not of `str` type.\
Raises a `TypeError` if `args` is not of `tuple` type.\
Raises a `TypeError` if `func` is not callable.\
Returns the index of the [task](#sttask.task) in [self.tasks](#sttask.taskowner.tasks).

<a name="sttask.taskowner.task_list"></a>
#### sttask.TaskOwner.task_list() -> list

| Argument | Type  | Default |
|----------|-------|---------|
|          |       |         |

Returns a list of all the names of tasks in [self.tasks](#sttask.taskowner.tasks).
eg.
```python
>>> import sttask
>>> owner = sttask.TaskOwner()
>>> owner.add("task1", (lambda self, args: print("This is task1")))
0
>>> owner.add("task2", (lambda self, args: print("This is task2")))
1
>>> owner.add("task3", (lambda self, args: print("This is task3")))
2
>>> owner.update()
This is task1
This is task2
This is task3
>>> owner.task_list()
['task1', 'task2', 'task3']
```

<a name="sttask.taskowner.schedule_list"></a>
#### sttask.TaskOwner.schedule_list() -> list

| Argument | Type  | Default |
|----------|-------|---------|
|          |       |         |

Returns a list of all the names of schedules in [self.scheduled](#sttask.taskowner.scheduled).
eg.
```python
>>> import sttask
>>> owner = sttask.TaskOwner()
>>> owner.schedule("schedule1", (lambda self, args: print("This is schedule1")))
0
>>> owner.schedule("schedule2", (lambda self, args: print("This is schedule2")))
1
>>> owner.schedule("schedule3", (lambda self, args: print("This is schedule3")))
2
>>> owner.schedule_list()
['schedule1', 'schedule2', 'schedule3']
```

<a name="sttask.taskowner.update"></a>
#### sttask.TaskOwner.update() -> None

| Argument | Type  | Default |
|----------|-------|---------|
|          |       |         |

Update the tasks and schedules in this instance of [sttask.TaskOwner](#sttask.taskowner).
Takes away 1 from schedule.time for all in [self.scheduled](#sttask.taskowner.scheduled) if the schedule is not paused.
If a schedules time is 0, turn it into a task and put it in [self.tasks](#sttask.taskowner.tasks).
Runs the update function on every task in [self.tasks](#sttask.taskowner.tasks) if the task is not paused.

<a name="sttask.taskowner.grab_task"></a>
#### sttask.TaskOwner.grab_task(name: str) -> int

| Argument | Type  | Default |
|----------|-------|---------|
|`name`    |`str`  |         |

Returns the index of the [task](#sttask.task) in [self.tasks](#sttask.taskowner.tasks) with the name `name`.\
Raises a `TypeError` if `name` is not of `str` type.\
If the function cannot find the task, `-1` is returned.

<a name="sttask.taskowner.grab_schedule"></a>
#### sttask.TaskOwner.grab_schedule(name: str) -> int

| Argument | Type  | Default |
|----------|-------|---------|
|`name`    |`str`  |         |

Returns the index of the [schedule](#sttask.schedule) in [self.scheduled](#sttask.taskowner.scheduled) with the name `name`.\
Raises a `TypeError` if `name` is not of `str` type.\
If the function cannot find the schedule, `-1` is returned.

<a name="sttask.taskowner.schedule"></a>
#### sttask.TaskOwner.schedule(name: str, func, time: int = 0, args: tuple = ()) -> int

| Argument | Type  | Default |
|----------|-------|---------|
|`name`    |`str`  |         |
|`func`    |       |         |
|`time`    |`int`  |`0`      |
|`args`    |`tuple`|`()`     |

Created a schedule called `name` and sets it's update function to `func`, it's arguments to `args` and it's time to `time`.\
Then appends the schedule to [self.scheduled](#sttask.taskowner.scheduled).\
Raises a `TypeError` if `name` is not of `str` type.\
Raises a `TypeError` if `args` is not of `tuple` type.\
Raises a `TypeError` if `time` is not of `int` type.\
Raises a `TypeError` if `func` is not callable.\
Returns the index of the [schedule](#sttask.schedule) in [self.scheduled](#sttask.taskowner.scheduled).

<a name="sttask.taskowner.play"></a>
#### sttask.TaskOwner.play(task: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and sets it's paused value to 0.\
Raises a `TypeError` if `task` is not of `str` type.

<a name="sttask.taskowner.pause"></a>
#### sttask.TaskOwner.pause(task: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and sets it's paused value to 1.\
Raises a `TypeError` if `task` is not of `str` type.

<a name="sttask.taskowner.name_set"></a>
#### sttask.TaskOwner.name_set(task: str, name: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |
|`name`    |`str`  |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and sets it's name value to `name`.\
Raises a `TypeError` if `task` is not of `str` type.\
Raises a `TypeError` if `name` is not of `str` type.

<a name="sttask.taskowner.update_set"></a>
#### sttask.TaskOwner.update_set(task: str, func) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |
|`func`    |       |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and sets it's update function to `func`.\
Raises a `TypeError` if `task` is not of `str` type.\
Raises a `TypeError` if `func` is not callable.

<a name="sttask.taskowner.args_set"></a>
#### sttask.TaskOwner.args_set(task: str, func) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |
|`args`    |`tuple`|         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and sets it's arguments to `args`.\
Raises a `TypeError` if `task` is not of `str` type.\
Raises a `TypeError` if `args` is not of `tuple` type.

<a name="sttask.taskowner.grab_output"></a>
#### sttask.TaskOwner.grab_output(task: str)

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and returns it's output value.\
Raises a `TypeError` if `task` is not of `str` type.

<a name="sttask.taskowner.pop_task"></a>
#### sttask.TaskOwner.pop_task(task: str)

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |

Looks for a task of the name `task` in [self.tasks](#sttask.taskowner.tasks) and pops it from the list.\
Raises a `TypeError` if `task` is not of `str` type.

<a name="sttask.taskowner.play_schedule"></a>
#### sttask.TaskOwner.play_schedule(schedule: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`schedule`|`str`  |         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and sets it's paused value to 0.\
Raises a `TypeError` if `schedule` is not of `str` type.

<a name="sttask.taskowner.pause_schedule"></a>
#### sttask.TaskOwner.pause_schedule(schedule: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`schedule`|`str`  |         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and sets it's paused value to 1.\
Raises a `TypeError` if `schedule` is not of `str` type.

<a name="sttask.taskowner.name_set_schedule"></a>
#### sttask.TaskOwner.name_set_schedule(schedule: str, name: str) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`schedule`|`str`  |         |
|`name`    |`str`  |         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and sets it's name value to `name`.\
Raises a `TypeError` if `schedule` is not of `str` type.\
Raises a `TypeError` if `name` is not of `str` type.

<a name="sttask.taskowner.update_set_schedule"></a>
#### sttask.TaskOwner.update_set_schedule(schedule: str, func) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |
|`func`    |       |         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and sets it's update function to `func`.\
Raises a `TypeError` if `schedule` is not of `str` type.\
Raises a `TypeError` if `func` is not callable.

<a name="sttask.taskowner.args_set_schedule"></a>
#### sttask.TaskOwner.args_set_schedule(schedule: str, func) -> None

| Argument | Type  | Default |
|----------|-------|---------|
|`schedule`|`str`  |         |
|`args`    |`tuple`|         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and sets it's arguments to `args`.\
Raises a `TypeError` if `schedule` is not of `str` type.\
Raises a `TypeError` if `args` is not of `tuple` type.

<a name="sttask.taskowner.pop_schedule"></a>
#### sttask.TaskOwner.pop_schedule(schedule: str)

| Argument | Type  | Default |
|----------|-------|---------|
|`task`    |`str`  |         |

Looks for a task of the name `schedule` in [self.scheduled](#sttask.taskowner.scheduled) and pops it from the list.\
Raises a `TypeError` if `schedule` is not of `str` type.

<a name="sttask.task"></a>
### sttask.Task

|  Value |   Type   | Default |
|:------:|:--------:|:-------:|
|  name  |    str   | *input* |
| update | function | *input* |
| paused |    int   | *input* |
|  args  |   tuple  | *input* |
| output |          |         |

A class for storing infomation about tasks.

<a name="sttask.task.name"></a>
#### sttask.task.name: str

A string for storing the name of this task.

<a name="sttask.task.update"></a>
#### sttask.task.update(self: [sttask.Task](#sttask.task), args: tuple)

A function with no set action. Called whenever [sttask.TaskOwner.update](#sttask.taskowner.update) is called.\
`self` is the [Task](#sttask.task) object that this function belongs to.\
`args` is a tuple of all the arguments passed to this function.

<a name="sttask.task.paused"></a>
#### sttask.task.paused: int

An int for storing if the task is paused or not.\
If it is a true value the task is paused.\
If not, it's not paused.

<a name="sttask.task.args"></a>
#### sttask.task.args: tuple

A tuple for storing all the arguments passed to the [self.update](#sttask.task.update) function.

<a name="sttask.task.output"></a>
#### sttask.task.output

A variable with no set value, used as an output for [self.update](#sttask.task.update).

<a name="sttask.schedule"></a>
### sttask.Schedule

|  Value |   Type   | Default |
|:------:|:--------:|:-------:|
|  name  |    str   | *input* |
| update | function | *input* |
| paused |    int   | *input* |
|  args  |   tuple  | *input* |
|  time  |    int   | *input* |

A class for storing infomation about schedules.

<a name="sttask.schedule.name"></a>
#### sttask.schedule.name: str

A string for storing the name of this task.

<a name="sttask.schedule.update"></a>
#### sttask.schedule.update(self: [sttask.Task](#sttask.task), args: tuple)

A function with no set action. Called whenever [sttask.TaskOwner.update](#sttask.taskowner.update) is called.\
`self` is the [Task](#sttask.task) object that this function belongs to.\
`args` is a tuple of all the arguments passed to this function.

<a name="sttask.schedule.paused"></a>
#### sttask.schedule.paused: int

An int for storing if the task is paused or not.\
If it is a true value the task is paused.\
If not, it's not paused.

<a name="sttask.schedule.args"></a>
#### sttask.schedule.args: tuple

A tuple for storing all the arguments passed to the [self.update](#sttask.schedule.update) function.

<a name="sttask.schedule.time"></a>
#### sttask.schedule.output

An int that gets decremented whenever [sttask.TaskOwner.update](#sttask.taskowner.update) is called.\
When it reached 0, the [parent](sttask.schedule) gets turned into a [sttask.Task](#sttask.task)

<a name="sttask.end"></a>
## sttask.end: int

If a task returns this in [sttask.Task.update](#sttask.task.update), the task is deleted.

<a name="sttask.pause"></a>
## sttask.pause: int

If a task returns this in [sttask.Task.update](#sttask.task.update), the task is paused.

<a name="sttask.utils"></a>
# sttask.utils

|  Value  |   Type   |   Default  |
|:-------:|:--------:|:----------:|
| convert | function | *function* |

<a name="sttask.utils.convert"></a>
## sttask.utils.convert(task, *, schedule_time: int = 0)

| Argument      | Type | Default |
|---------------|------|---------|
|`task`         |      |         |
|`*`            |      |         |
|`schedule_time`|`int` |`0`      |

If `task` is of type [sttask.Task](#sttask.task) then convert it to an [sttask.Schedule](sttask.schedule) with the time of `schedule_time` and return it.
If `task` is of type [sttask.Schedule](sttask.schedule) then convert it to an [sttask.Task](#sttask.task).
If neither, raise a `TypeError`.
If `schedule_time` is not of `int` type, raise a `TypeError`.
