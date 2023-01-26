****Step 1:** Create a gradle project**

Follow the steps outlined in [Creating a Gradle Project With IntelliJ](https://jeremysteeves01.github.io/qa-test-automation/2023/01/26/creating-a-gradle-project-with-intellij.html)
 
****Step 2:** Start Adding Dependencies To Your Gradle Project**

First things first, you’ll need to decide on a testing framework. By default IntelliJ provided you with the dependency for the JUnit testing framework in the build.gradle file. However, for this tutorial we are going to use TestNg instead.

Remove the JUnit dependency from the dependencies section of the build.gradle file, and replace it with the following:

<img width="602" alt="Screenshot 2023-01-26 at 9 36 15 AM" src="https://user-images.githubusercontent.com/76220477/214864418-bd21e4fa-4ece-4211-ad1d-6e85c04d1d8d.png">

Now, because IntelliJ was automatically set up to work with JUnit, we need to add an extra command to let IntelliJ know that we want it to use TestNG instead of JUnit. So, directly below the dependencies section add the following to your build.gradle file.

<img width="602" alt="Screenshot 2023-01-26 at 9 36 23 AM" src="https://user-images.githubusercontent.com/76220477/214864533-f4ed32ae-6944-418c-9d58-a901cbc933a2.png">

Since this is a tutorial about how to use RetroFit2 libraries to help test Rest APIs, we’ll go ahead and add the Retrofit2 dependencies to the build.gradle file. So your entire build.gradle file should now look something like this:

<img width="601" alt="Screenshot 2023-01-26 at 9 36 46 AM" src="https://user-images.githubusercontent.com/76220477/214864623-5f35979a-808c-4556-a68b-617f2aab9bce.png">

At this point we’ll stop adding dependencies, however we’ll be adding more later whenever we need them. 

****Step 3:** Architecting The Project**

Let’s start giving our project a little structure before we start adding any code.

On the left side of the screen you’ll notice that IntelliJ created a project folder called src, which contains two sub-folders Main and Test. Inside both of them, there is a JAVA directory. 

<img width="193" alt="Screenshot 2023-01-26 at 9 41 43 AM" src="https://user-images.githubusercontent.com/76220477/214864989-7711b881-766c-4c73-a072-79fade7801a0.png">

Starting with the main>java directory, go ahead and add the following packages:

<img width="263" alt="Screenshot 2023-01-26 at 9 41 52 AM" src="https://user-images.githubusercontent.com/76220477/214865072-ad8d37c2-0b51-414d-b636-5e5bed70e6d9.png">

****Step 4:** Building the Client Layer**


We still haven’t talked about what exactly we are testingl. We need some sort of Rest API to test, so we’ll use a free one available online at https://jsonplaceholder.typicode.com/ . 

On their website, under the “Resources” section, you can see that they outline the various resources that they support. For this tutorial we will focus on “users”.

<img width="604" alt="Screenshot 2023-01-26 at 9 42 24 AM" src="https://user-images.githubusercontent.com/76220477/214865227-59f95819-4a1a-4330-9b0f-ade4619286a5.png">

In our project, inside the Clients package, we would create a client for each of the resources (PostsClient, CommentClient, AlbumClient, PhotoClient, TodoClient and UserClient). But we’ll start with only creating a UsersClient.java file. Really all this is, is a class that we will name “UserClient”. So far the class is empty:

<img width="555" alt="Screenshot 2023-01-26 at 9 43 47 AM" src="https://user-images.githubusercontent.com/76220477/214866510-79e94cf0-229d-40ed-a7d2-934eb3a1eb40.png">

This is when we will finally start using Retrofit2 capabilities. Let’s start by adding a constructor to this class.

<img width="600" alt="Screenshot 2023-01-26 at 9 43 55 AM" src="https://user-images.githubusercontent.com/76220477/214866594-e9f385c8-fc3b-437a-b8f1-4ac89deb2d03.png">

Now, let’s add the following variables to the top of our class:

<img width="601" alt="Screenshot 2023-01-26 at 9 44 02 AM" src="https://user-images.githubusercontent.com/76220477/214866670-d4979950-35be-487b-b30c-33246b071203.png">

The red text in the code above means that the IntelliJ compiler does not know what Type of variable we are trying to declare. Let’s start with Retrofit. Since we’ve already added the Retrofit2 dependencies, all we need to do now is import the package into the UserClient class. We will do the same for OkHttpClient.

<img width="602" alt="Screenshot 2023-01-26 at 9 44 32 AM" src="https://user-images.githubusercontent.com/76220477/214866743-c566c8a5-fe1b-4e73-8ccb-8403a5f62aca.png">

UserService is still red because we haven’t actually created a class called UserService yet. Let’s do that now.

Inside the Services directory, create an interface called UserSerivce. The services will always be interfaces.

<img width="518" alt="Screenshot 2023-01-26 at 9 44 41 AM" src="https://user-images.githubusercontent.com/76220477/214866813-6486acb7-a598-46e1-a0d3-a7b5cef04888.png">

Go back to the UserClient class and import the UserService interface into it:

<img width="600" alt="Screenshot 2023-01-26 at 9 44 49 AM" src="https://user-images.githubusercontent.com/76220477/214866885-6d8f1f94-e32f-4e89-9563-64dd4aae2d0e.png">

Inside the class constructor, we can start adding the code that will be responsible for building and sending the Rest request.

<img width="599" alt="Screenshot 2023-01-26 at 9 44 57 AM" src="https://user-images.githubusercontent.com/76220477/214866979-5781e178-3be2-4a96-b9e2-e8742400de6e.png">

This time import the retrofit2 library:

<img width="604" alt="Screenshot 2023-01-26 at 9 45 10 AM" src="https://user-images.githubusercontent.com/76220477/214867129-8d459466-2c05-48e3-8db7-b103294dfa95.png">

The baseUrl is lit up in red because we haven’t yet defined a variable with that name. So let’s go ahead  and do that. Keeping in mind that every client will have a different baseUrl. The baseUrl is the portion of the resource url which never changes. So in our example the baseUrl is as follows:

<img width="602" alt="Screenshot 2023-01-26 at 9 45 17 AM" src="https://user-images.githubusercontent.com/76220477/214867210-f8a5db9a-9a2d-481e-9110-7e4ad5a2d5e1.png">

Everything in our UserClient class should now compile:

<img width="599" alt="Screenshot 2023-01-26 at 9 45 26 AM" src="https://user-images.githubusercontent.com/76220477/214867294-ae2811d3-80f4-4380-ab3e-e1b0577b1569.png">

<img width="598" alt="Screenshot 2023-01-26 at 9 45 32 AM" src="https://user-images.githubusercontent.com/76220477/214867408-1e7c1cca-a90e-4676-b78c-7ac6b126a7c9.png">

The only problem now is that our UserService class that we created earlier, is empty. So let’s go add some stuff to it.

****Step 5:** Building the Service Layer**

You’ll need to import the following into the UserService class:

<img width="603" alt="Screenshot 2023-01-26 at 9 45 40 AM" src="https://user-images.githubusercontent.com/76220477/214867511-d6104bec-4111-4547-a28f-71b1a2f0d7da.png">

Let’s say you wanted to send a request to get a list of all the users that exist in the system. To do that you will need to call the /Users endpoint. This is how you would do that using Retrofit2 libraries.

<img width="600" alt="Screenshot 2023-01-26 at 9 46 08 AM" src="https://user-images.githubusercontent.com/76220477/214867617-3466ae32-d419-4ab3-b279-068e5bbc4b88.png">

This line of code knows that we want to make a request to the system to retrieve a list of all the users in it. So it will make a ‘call’ to the server and the server will return a JSON response which will contain all the users. Retrofit2 will convert (deserialize) the JSON response into a list of type UserModel. 

We have not yet created a class called UserModel, which is why IntelliJ lights it up in red. We already know that the JSON payload for a single user looks like this:

<img width="603" alt="Screenshot 2023-01-26 at 9 46 16 AM" src="https://user-images.githubusercontent.com/76220477/214867685-5fcbaf8f-3f33-4301-9cc3-e90059e32174.png">

****Step 6:** Building the Models**

So what we need to do is create some objects/classes to model this JSON payload. That way we can convert to and from JSON into a strongly typed object. This is called Deserializating and Serializing.


In this example we want to deserialize the JSON response into a list of types UserModel.

Under the Models directory we will create a UserModel class that looks like this:

UserModel

<img width="602" alt="Screenshot 2023-01-26 at 9 46 25 AM" src="https://user-images.githubusercontent.com/76220477/214867800-b159839a-bf58-40b5-bbdd-2926c733dd5b.png">

There’s a lot of red going on here. Let’s start with Lombok. Lombok is a plugin which will automatically create the ‘getters’ and ‘setters’ for all the properties in the class. We need to first download the Lombok plugin.

Lombok Plugin

<img width="600" alt="Screenshot 2023-01-26 at 9 46 37 AM" src="https://user-images.githubusercontent.com/76220477/214867894-edfd333e-17af-4bfa-9638-079997c730d7.png">

Once you’ve successfully downloaded the Lombok plugin, you’ll need to add lombok to your list of dependencies in the build.gradle file

<img width="599" alt="Screenshot 2023-01-26 at 9 46 51 AM" src="https://user-images.githubusercontent.com/76220477/214867957-6644fa36-d4f0-469a-a386-a71c480644e4.png">

The only thing that should be left to do in order to make the code compile is to finish creating the Models. We still need to create the following models:
AddressModel

<img width="600" alt="Screenshot 2023-01-26 at 9 47 10 AM" src="https://user-images.githubusercontent.com/76220477/214868076-ecef7e6c-e904-43a4-90ee-09db6c93f268.png">

CompanyModel

<img width="599" alt="Screenshot 2023-01-26 at 9 47 28 AM" src="https://user-images.githubusercontent.com/76220477/214868152-6a1900b8-df0c-4b11-96ef-db80ca66bafd.png">


GeoModel

<img width="599" alt="Screenshot 2023-01-26 at 9 47 41 AM" src="https://user-images.githubusercontent.com/76220477/214868266-ae7b7ae6-8e84-497c-a65f-7a27d38ad3f0.png">













