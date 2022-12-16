# Scaling Web applications

When scaling websites we need to make sure that the backends are scalable because frontends are fundamentally scalable and as such the frontend never really comes into the picture.

# **The Backend**
The backend is the unseen portion responsible for storing and organizing data, and ensuring everything on the client-side actually works. The backend code runs on the server and it also includes the database. As such, in any application, this is a core and fundamental part. 
The client is a small computer that has a small computation to do but the server is the one which is bombarded by tens of thousands simultaneously.

## **Scaling**
For scaling any web application, the backend architecture needs to be well thought out. The backend has to scale horizontally, by adding a new capacity that should be a new server. The backend can not scale vertically because of physical limitations. Vertical scaling involves physical factors like hardware processing power and RAM.

#### **Horizontal Scaling**
Scaling horizontally involves creating/assigning more servers and assigning them to more clients. So the number of clients to a server comes down, and that is all that matters. That ratio value is what is needed to be controlled for effective scaling of applications.

#### **Stateless Code**
The fact that you have to maintain that ratio gives you a few constraints to play with. And one of the constraints is that your code has to be stateless. This means that the application layer of your backend(business layer) the one that your clients interact with is running on the backend as (i.e Java, Node, Python,...etc ) any process can not contain state. 
By state it means, i.e you are doing some sort of authentication, and you are storing connected clients or clients which were the last active in an array inside of your code,  this will be a problem because if you do horizontal scaling the server would create a fresh copy, and given how scaling works, the servers are assigned randomly to clients depending on what the load is currently. And if you assign the wrong client to the server, every single time your client would just have a lot of time in terms of authenticating properly. i.e if you are using some sort of authentication and matching it with a key value inside the local state, that's wrong. You have to move your state somewhere central.--
The central part could be an actual database i.e MongoDB/MySQL, and once you have done that you have to make sure that the horizontal scalability is present.

#### **Managed Services** 
Horizontal scalability is easier in some cases if you're using i.e Lambda at AWS. They can automatically scale till the limit you have is utilized and it can automatically shrink as well. You will only pay the cost while the code is executing and it can also be done manually. And with that, your application layer is scalable, thanks to horizontal scaling and stateless code.
For cases where you have to move the central dependency, you can use a distributed database. Distributed databases expose your database over an http server and they manage the internal scaling, read and write on their own.

With the databases you can scale the computing all over the world. Even though you can lose out on things like consistency and performance. In this, you can use managed databases like MongoDB Atlas. Managed databases offer elastic cache and many other awesome features which you can control through the GUI.
