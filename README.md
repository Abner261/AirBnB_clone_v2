## 0x03. AirBnB clone - Deploy static

### Concepts

* _For this project, we expect you to look at these concepts:_

### [1] CI/CD

* The lean/agile methodology (See: [Twelve Principles of Agile Software](https://agilemanifesto.org/principles.html)) is now widely used by the industry and one of its key principles is to iterate as fast as possible. If you apply this to software engineering, it means that you should:

	- code
	- ship your code
	- measure the impact
	- learn from it
	- fix or improve it
	- start over

* As fast as possible and with small iterations in days or even hours (whereas it used to be weeks or even months). One big advantage is that if product development is going the wrong direction, fast iteration will allow to quickly detect this, and avoid wasting time

* From a technical point of view, quicker iterations mean fewer lines of code being pushed at every deploy, which allows easy performance impact measurement and easy troubleshooting if something goes wrong (better to debug a small code change than weeks of new code)

![DevOps Tools](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/829c6ab908afc76f29bc74f9545103fa0764e89e/DevOps-Tools.png)

Applied to software engineering, [CI/CD](https://digital.ai/catalyst-blog/walk-before-you-run-understanding-ci-in-cd/) (Continuous Integration/Continuous Deployment) is a principle that allows individuals or teams to have a lean/agile way of working.

This translates to a “shipping pipeline” which is often built with multiple tools such as:

* Shipping the code:
	- Capistrano, Fabric
* Encapsulating the code
	- Docker, Packer
* Testing the code
	- Jenkins, CircleCi, Travis
* Measuring the code
	- Datadog, Newrelic, Wavefront

### [2] AirBnB clone

![AirBnB clone](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/9947875dc19f0a1303899f904a8322b19f493b59/AirBnB%20clone.png)

I know you were waiting for it: it’s here!

The AirBnB clone project starts now until… the end of the first year. The goal of the project is to deploy on your server a simple copy of the [AirBnB website](https://www.airbnb.com/https://www.airbnb.com/)

You won’t implement all the features, only some of them to cover all fundamental concepts of the higher level programming track.

* After 4 months, you will have a complete web application composed by:

	- A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)
	- A website (the front-end) that shows the final product to everybody: static and dynamic
	- A database or files that store data (data = objects)
	- An API that provides a communication interface between the front-end and your data (retrieve, create, delete, update them)

### Final product

![Final product](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/f23c4d89260f5865091279c6afc43a4a014f4f7b/Final%20product.png)

![Final product](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/743b9f3a60c56cf540c6cec13cf43e52533a1ee9/Final%20product.jpeg)

### Concepts to learn

- [Unittest](https://docs.python.org/3.4/library/unittest.html#module-unittest) - and please work all together on tests cases
- **Python packages** concept page
- Serialization/Deserialization
- `*args, **kwargs`
- `datetime`
- More coming soon!

### Steps

You won’t build this application all at once, but step by step.

Each step will link to a concept:

* **The console**

	- create your data model
	- manage (create, update, destroy, etc) objects via a console / command interpreter
	- store and persist objects to a file (JSON file)

The first piece is to manipulate a powerful storage system. This storage engine will give us an abstraction between “My object” and “How they are stored and persisted”. This means: from your console code (the command interpreter itself) and from the front-end and RestAPI you will build later, you won’t have to pay attention (take care) of how your objects are stored.

This abstraction will also allow you to change the type of storage easily without updating all of your codebase.

The console will be a tool to validate this storage engine

![The console](https://github.com/Abner261/AirBnB_clone_v2/blob/master/The%20console.png?raw=true)

### Web static

- learn HTML/CSS
- create the HTML of your application
- create template of each object

![Web static](https://github.com/Abner261/AirBnB_clone_v2/blob/master/Web%20static.png?raw=true)

### MySQL storage

- replace the file storage by a Database storage
- map your models to a table in database by using an O.R.M.

![MySQL storage](https://github.com/Abner261/AirBnB_clone_v2/blob/master/MySQL%20storage.png?raw=true)

### Web framework - templating

- create your first web server in Python
- make your static HTML file dynamic by using objects stored in a file or database

![Web framework ](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/ceff4f064c2500ef00c5b4bfd214f33e066b170b/Web%20framework.png)

### RESTful API

- expose all your objects stored via a JSON web interface
- manipulate your objects via a RESTful API

![RESTful API](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/e1608eb7fa780d7d02f79a3ef27c57389ddec8c1/RESTful%20API.png)

### Web dynamic

- learn JQuery
- load objects from the client side by using your own RESTful API

![Web dynamic](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/b8da3b358e3280e3bf621b77cacfdd743f571d36/Web%20dynamic.png)

### Files and Directories

* `models` directory will contain all classes used for the entire project. A class, called “model” in a OOP project is the representation of an object/instance.
* `tests` directory will contain all unit tests.
* `console.py` file is the entry point of our command interpreter.
* `models/base_model.py` file is the base class of all our models. It contains common elements:
	- attributes: `id`, `created_at` and `updated_at`
	- methods: `save()` and `to_json()`
- `models/engine` directory will contain all storage classes (using the same prototype). For the moment you will have only one: `file_storage.py`

### Storage

Persistency is really important for a web application. It means: every time your program is executed, it starts with all objects previously created from another execution. Without persistency, all the work done in a previous execution won’t be saved and will be gone.

In this project, you will manipulate 2 types of storage: file and database. For the moment, you will focus on file.

Why separate “storage management” from “model”? It’s to make your models modular and independent. With this architecture, you can easily replace your storage system without re-coding everything everywhere.

* You will always use class attributes for any object. Why not instance attributes? For 3 reasons:

	- Provide easy class description: everybody will be able to see quickly what a model should contain (which attributes, etc…)
	- Provide default value of any attribute
	- In the future, provide the same model behavior for file storage or database storage

### How can I store my instances?

That’s a good question. So let’s take a look at this code:

```sh
class Student():
    def __init__(self, name):
        self.name = name

students = []
s = Student("John")
students.append(s)
```

Here, I’m creating a student and store it in a list. But after this program execution, my Student instance doesn’t exist anymore.

```sh
class Student():
    def __init__(self, name):
        self.name = name

students = reload() # recreate the list of Student objects from a file
s = Student("John")
students.append(s)
save(students) # save all Student objects to a file
```

Nice!

But how it works?

* First, let’s look at `save(students)`:

	- Can I write each `Student` object to a file => NO, it will be the memory representation of the object. For another program execution, this memory representation can’t be reloaded.
	- Can I write each `Student.name` to a file => YES, but imagine you have other attributes to describe Student? It would start to be become too complex.

The best solution is to convert this list of Student objects to a JSON representation.

Why JSON? Because it’s a standard representation of object. It allows us to share this data with other developers, be human readable, but mainly to be understood by another language/program.

* Example:

	- My Python program creates `Student` objects and saves them to a JSON file
	- Another Javascript program can read this JSON file and manipulate its own `Student` class/representation

And the `reload()`? now you know the file is a JSON file representing all `Student` objects. So `reload()` has to read the file, parse the JSON string, and re-create `Student` objects based on this data-structure.

### File storage == JSON serialization

* For this first step, you have to write in a file all your objects/instances created/updated in your command interpreter and restore them when you start it. You can’t store and restore a Python instance of a class as “Bytes”, the only way is to convert it to a serializable data structure:

	- convert an instance to Python built in serializable data structure (list, dict, number and string) - for us it will be the method `my_instance.to_json()` to retrieve a dictionary
	- convert this data structure to a string (JSON format, but it can be YAML, XML, CSV…) - for us it will be a `my_string = JSON.dumps(my_dict)`
	- write this string to a file on disk

And the process of deserialization?

* The same but in the other way:

	- read a string from a file on disk
	- convert this string to a data structure. This string is a JSON representation, so it’s easy to convert - for us it will be a `my_dict = JSON.loads(my_string)`
	- convert this data structure to instance - for us it will be a `my_instance = MyObject(my_dict)`

### `*args, **kwargs`

* [How To Use them](https://www.digitalocean.com/community/tutorials/how-to-use-args-and-kwargs-in-python-3)

How do you pass arguments to a function?

```sh
def my_fct(param_1, param_2):
    ...

my_fct("Best", "School")
```

But with this function definition, you must call `my_fct` with 2 parameters, no more, no less.

Can it be dynamic? Yes you can:

```sh
def my_fct(*args, **kwargs):
    ...

my_fct("Best", "School")
```

* What? What’s `*args` and `**kwargs?`

	- `*args` is a Tuple that contains all arguments
	- `*kwargs` is a dictionary that contains all arguments by key/value

A dictionary? But why?

So, to make it clear, `*args` is the list of anonymous arguments, no name, just an order. `**kwargs` is the dictionary with all named arguments.

Examples:

```sh
def my_fct(*args, **kwargs):
    print("{} - {}".format(args, kwargs))

my_fct() # () - {}
my_fct("Best") # ('Best',) - {}
my_fct("Best", 89) # ('Best', 89) - {}
my_fct(name="Best") # () - {'name': 'Best'}
my_fct(name="Best", number=89) # () - {'name': 'Best', 'number': 89}
my_fct("School", 12, name="Best", number=89) # ('School', 12) - {'name': 'Best', 'number': 89}
```

Perfect? Of course you can mix both, but the order should be first all anonymous arguments, and after named arguments.

Last example:

```sh
def my_fct(*args, **kwargs):
    print("{} - {}".format(args, kwargs))

a_dict = { 'name': "Best", 'age': 89 }

my_fct(a_dict) # ({'age': 89, 'name': 'Best'},) - {}
my_fct(*a_dict) # ('age', 'name') - {}
my_fct(**a_dict) # () - {'age': 89, 'name': 'Best'}
```

You can play with these 2 arguments to clearly understand where and how your variables are stored.

### `datetime`

`datetime` is a Python module to manipulate date, time etc…

In this example, you create an instance of `datetime` with the current date and time:

```sh
from datetime import datetime

date_now = datetime.now()
print(type(date_now)) # <class 'datetime.datetime'>
print(date_now) # 2017-06-08 20:42:42.170922
```

`date_now` is an object, so you can manipulate it:

```sh
from datetime import timedelta

date_tomorrow = date_now + timedelta(days=1)
print(date_tomorrow) # 2017-06-09 20:42:42.170922
```

… you can also store it:

```sh
a_dict = { 'my_date': date_now }
print(type(a_dict['my_date'])) # <class 'datetime.datetime'>
print(a_dict) # {'my_date': datetime.datetime(2017, 6, 8, 20, 42, 42, 170922)}
```

What? What’s this format when a `datetime` instance is in a datastructure??? It’s unreadable.

How to make it readable: [strftime](https://strftime.org/)

```sh
print(date_now.strftime("%A")) # Thursday
print(date_now.strftime("%A %d %B %Y at %H:%M:%S")) # Thursday 08 June 2017 at 20:42:42
```

### Data diagram

![Data diagram](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/dc5f76657e708ea023ccc87de0abc84852a3a98a/Data%20diagram.jpg)

### Background Context

Ever since you completed project [0x0F. Load balancer](https://intranet.alxswe.com/projects/275) of the SysAdmin track, you’ve had 2 web servers + 1 load balancer but nothing to distribute with them.

It’s time to make your work public!

In this first deployment project, you will be deploying your `web_static` work. You will use `Fabric` (for Python3). Fabric is a Python library and command-line tool for streamlining the use of SSH for application deployment or systems administration tasks. It provides a basic suite of operations for executing local or remote shell commands (normally or via `sudo`) and uploading/downloading files, as well as auxiliary functionality such as prompting the running user for input, or aborting execution. This concept is important: execute commands locally or remotely. Locally means in your laptop (physical laptop or inside your Vagrant), and Remotely means on your server(s). Fabric is taking care of all network connections (SSH, SCP etc.), it’s an easy tool for transferring, executing, etc. commands from locale to a remote server.

![AirBnB_clone_v2](https://raw.githubusercontent.com/Abner261/AirBnB_clone_v2/196e202380816b3ebb65f11a96faced204d97224/aribnb_diagram_0.jpg)

### Resources

* **Read or watch:**

	- [How to use Fabric](https://www.digitalocean.com/community/tutorials/how-to-use-fabric-to-automate-administration-tasks-and-deployments)
	- [How to use Fabric in Python](https://www.pythonforbeginners.com/systems-programming/how-to-use-fabric-in-python)
	- [Fabric and command line options](https://docs.fabfile.org/en/1.13/usage/fab.html)
	- [CI/CD concept page](https://intranet.alxswe.com/concepts/43)
	- [Nginx configuration for beginners](https://nginx.org/en/docs/beginners_guide.html)
	- [Difference between root and alias on NGINX](https://blog.heitorsilva.com/en/nginx/diferenca-entre-root-e-alias-do-nginx/)
	- [Fabric for Python 3](https://github.com/mathiasertl/fabric)
	- [Fabric Documentation](https://www.fabfile.org/)

* **Learning Objectives**

	- At the end of this project, you are expected to be able to [explain to anyone](https://fs.blog/feynman-learning-technique/), **without the help of Google:**

* **General**

	- What is Fabric
	- How to deploy code to a server easily
	- What is a `tgz` archive
	- How to execute Fabric command locally
	- How to execute Fabric command remotely
	- How to transfer files with Fabric
	- How to manage Nginx configuration
	- What is the difference between `root` and `alias` in a Nginx configuration

### Requirements

* **Python Scripts**

	- Allowed editors: `vi`, `vim`, `emacs`
	- All your files will be interpreted/compiled on Ubuntu 20.04 LTS using `python3` (version 3.4.0)
	- All your files should end with a new line
	- The first line of all your files should be exactly `#!/usr/bin/python3`
	- A `README.md` file at the root of the folder of the project is mandatory
	- Your code should use the `PEP 8` style (version `1.7.*`)
	- Your Fabric file must work with `Fabric 3` version `1.14.post1` (installation instruction below)
	- All your files must be executable
	- The length of your files will be tested using `wc`
	- All your functions (inside and outside a class) should have documentation (`python3 -c 'print(__import__("my_module").my_function.__doc__)'` and `python3 -c 'print(__import__("my_module").MyClass.my_function.__doc__)'`)
	- A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class or method (the length of it will be verified)

* **Bash Scripts**

	- Allowed editors: `vi`, `vim`, `emacs`
	- All your files will be interpreted on Ubuntu 20.04 LTS
	- All your files should end with a new line
	- A `README.md` file at the root of the folder of the project is mandatory
	- All your Bash script files must be executable
	- Your Bash script must pass `Shellcheck` (version `0.3.3-1~ubuntu20.04.1` via `apt-get`) without any errors
	- The first line of all your Bash scripts should be exactly `#!/usr/bin/env bash`
	- The second line of all your Bash scripts should be a comment explaining what is the script doing

## More Info

### Install Fabric for Python 3 - version 1.14.post1

```sh
$ pip3 uninstall Fabric
$ sudo apt-get install libffi-dev
$ sudo apt-get install libssl-dev
$ sudo apt-get install build-essential
$ sudo apt-get install python3.4-dev
$ sudo apt-get install libpython3-dev
$ pip3 install pyparsing
$ pip3 install appdirs
$ pip3 install setuptools==40.1.0
$ pip3 install cryptography==2.8
$ pip3 install bcrypt==3.1.7
$ pip3 install PyNaCl==1.3.0
$ pip3 install Fabric3==1.14.post1
```
