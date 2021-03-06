# STTASK python

### No more awaiting!

A module with a simple usage designed for game developing.

## Usage

```python
import sttask

print("This program will show waht STTASK can do.")

owner = sttask.TaskOwner()
print("Whenever 'owner.update()' is called, all tasks run.")
owner.update()

print("Nothing happened, as we need to add a task to it.")
owner.add("printhello", lambda self,args: print("Hello"))
owner.update()

# Hello

print("We just added a task called 'printhello', and then updated the owner. This made all the tasks run, causing 'Hello' to be printed.")
owner.add("printworld", lambda self,args: print("World"))
owner.update()

# Hello
# World

print("Now we added a task to print world, and updated, so both tasks ran.")
print("Lets remove a task!")
owner.pop_task("printhello")
owner.update()

# World

print("If we want to remove a task from within the same task, all we need to do is return 'sttask.end' from the task!")

def example_task(self,args):
	print("This task should delete its self if you input 'delete'")
	if input(">>> ")=="delete":
		return sttask.end

owner.pop_task("printworld")
owner.add("removeself",example_task)

while "removeself" in owner.task_list():
	owner.update()

print("Task is now deleted!")
print(owner.tasks)

# >>> not delete
# >>> dont delete
# >>> delete
# Task is now deleted!
# []
```

- [Docs](https://python-sttask.readthedocs.io/en/latest/)
- [Github](https://github.com/TheMystZ/python-sttask)
- [Bug tracker](https://github.com/TheMystZ/python-sttask/issues)
