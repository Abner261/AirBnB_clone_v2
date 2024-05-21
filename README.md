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

![The console]()

### Web static

- learn HTML/CSS
- create the HTML of your application
- create template of each object

