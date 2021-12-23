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
  - [Task]()
    - [sttask.Task.name]()
    - [sttask.Task.update]()
    - [sttask.Task.paused]()
    - [sttask.Task.args]()
    - [sttask.Task.output]()
  - [Schedule]()
    - [sttask.Schedule.name]()
    - [sttask.Schedule.update]()
    - [sttask.Schedule.paused]()
    - [sttask.Schedule.args]()
    - [sttask.Schedule.time]()
  - [sttask.end: int]()
  - [sttask.pause: int]()
- [utils]()
  - [sttask.utils.convert(task, \*, schedule_time = 0)]()

<a name="sttask"></a>
## sttask
The main module
<a name="sttask.taskowner"></a>
### sttask.TaskOwner
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
