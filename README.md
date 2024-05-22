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

* How To Use them](https://www.digitalocean.com/community/tutorials/how-to-use-args-and-kwargs-in-python-3)

How do you pass arguments to a function?

```sh
def my_fct(param_1, param_2):
    ...

my_fct("Best", "School")
```
