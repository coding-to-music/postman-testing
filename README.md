# Install Postman for API testing on Ubuntu 20.04

https://learning.postman.com/docs/getting-started/installation-and-updates/#installing-postman-on-linux

You can install Postman on Linux by manually downloading it, using the Snap store link, or with the command snap install postman.

```java
sudo snap install postman
```

To install manually, download and unzip the app, for example into the opt directory. You will need sudo privileges.

To start the app from a launcher icon, create a desktop file, naming it Postman.desktop and saving it in the following location:

~/.local/share/applications/Postman.desktop

Enter the following content in the file, replacing opt if you extracted the file somewhere else, and save it:

```java
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=/opt/Postman/app/Postman %U
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
```

```java
mkdir -p ~/.local/share/applications/

touch ~/.local/share/applications/Postman.desktop
```

From StackOverflow
https://stackoverflow.com/questions/42996358/how-to-install-start-postman-native-v4-10-3-on-ubuntu-16-04-lts-64-bit/43723749#43723749

```java
sudo wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz
sudo tar -xzf postman.tar.gz -C /opt
sudo rm postman.tar.gz
sudo ln -s /opt/Postman/Postman /usr/bin/postman
```

https://www.postman.com/downloads/

```java

wget -o Postman-linux-x86_64-9.3.1.tar.gz https://dl.pstmn.io/download/latest/linux64/Postman-linux-x86_64-9.3.1.tar.gz

wget  https://dl.pstmn.io/download/latest/linux64/Postman-linux-x86_64-9.3.1.tar.gz

```

## Validate JSON

https://jsonformatter.curiousconcept.com/#

# Postman Tutorial 

https://www.guru99.com/postman-tutorial.html

We will use the following URL for all examples in this Postman tutorial

## Postman Workspace
https://web.postman.co/workspace/My-Workspace


## Working with GET Requests

https://jsonplaceholder.typicode.com/users		
In the workspace

- Set your HTTP request to GET.
- In the request URL field, input link
- Click Send
- You will see 200 OK Message
- There should be 10 user results in the body which indicates that your test has run successfully.

## Working with POST Requests

Post requests are different from Get request as there is data manipulation with the user adding data to the endpoint. Using the same data from the previous tutorial in Get request, let’s now add our own user.

### Step 1) 
Click a new tab to create a new request.

Working with POST Requests
### Step 2) 
In the new tab

Set your HTTP request to POST.
Input the same link in request url: https://jsonplaceholder.typicode.com/users
switch to the Body tab
Working with POST Requests

### Step 3) 
In Body,

Click raw
Select JSON

Working with POST Requests
### Step 4) 
Copy and paste just one user result from the previous get request like below. Ensure that the code has been copied correctly with paired curly braces and brackets. Change id to 11 and name to any desired name. You can also change other details like the address.

[
    {
        "id": 11,
        "name": "Krishna Rungta",
        "username": "Bret",
        "email": "Sincere@april.biz",
        "address": {
            "street": "Kulas Light",
            "suite": "Apt. 556",
            "city": "Gwenborough",
            "zipcode": "92998-3874",
            "geo": {
                "lat": "-37.3159",
                "lng": "81.1496"
            }
        },
        "phone": "1-770-736-8031 x56442",
        "website": "hildegard.org",
        "company": {
            "name": "Romaguera-Crona",
            "catchPhrase": "Multi-layered client-server neural-net",
            "bs": "harness real-time e-markets"
        }
    }
]
Working with POST Requests

`Note`: Online Post request should have the correct format to ensure that requested data will be created. It is a good practice to use Get first to check the JSON format of the request. You can use tools like https://jsonformatter.curiousconcept.com/

Working with POST Requests
### Step 5) 
Next,

Click Send.
Status: 201 Created should be displayed
Posted data are showing up in the body.


## How to Parameterize Requests
## How to Create Postman Tests
## How to Create Collections
## How to Run Collections using Collection Runner
## How to Run Collections using Newman




# How to Parameterize Requests
Data Parameterization is one of the most useful features of Postman. Instead of creating the same requests with different data, you can use variables with parameters. These data can be from a data file or an environment variable. Parameterization helps to avoid repetition of the same tests and iterations can be used for automation testing.

Parameters are created through the use of double curly brackets: {{sample}}. Let’s take a look at an example of using parameters in our previous request:

How to Parameterize Requests
Now let’s create a parameterize get request.

### Step 1)

Set your HTTP request to GET
Input this link: https://jsonplaceholder.typicode.com/users. Replace the first part of the link with a parameter such as {{url}}. Request url should now be {{url}}/users.
Click send.
There should be no response since we have not set the source of our parameter.

### How to Parameterize Requests
### Step 2) 
To use the parameter you need to set the environment

Click the eye icon
Click edit to set the variable to a global environment which can be used in all collections.
How to Parameterize Requests
### Step 3) 
In variable,

set the name to the url which is https://jsonplaceholder.typicode.com
click Save.
How to Parameterize Requests
### Step 4) 
Click close if you see the next screen

How to Parameterize Requests
### Step 5) 
Go back to your Get request then click send. There should now be results for your request.

How to Parameterize Requests
*Note: Always ensure that your parameters have a source such as an environment variable or data file to avoid errors.

# How to Create Postman Tests
Postman Tests are JavaScript codes added to requests that help you verify results such as successful or failed status, comparison of expected results, etc. It usually starts with pm.test. It can be compared to asserts, verify commands available in other tools.

Let’s do some basic API testing using Postman for our parameterize requests from the previous lesson.

### Step 1) 
Go to your GET user request from the previous tutorial.

Switch to the tests tab. On the right side are snippet codes.
From the snippets section, click on “Status code: Code is 200”.
The pane is auto-populated

API testing
### Step 2) 
Now click Send. The test result should now be displayed.

API testing
### Step 3) 
Go back to the test tab and let’s add another test. This time we will compare the expected result to the actual result.

From the snippets section, click on “Response body:JSON value check”. We will be checking if Leanne Graham has the userid 1.

API testing
### Step 4)

Replace “Your Test Name” from the code with “Check if user with id1 is Leanne Graham” so that the test name specifies exactly what we want to test.
Replace jsonData.value with jsonData[0].name. To get the path, check the body in Get result earlier. Since Leanne Graham is userid 1, jsonData is in the first result which should start with 0. If you want to get the second result, use jsonData[1] and so on for succeeding results.
In to eql, input “Leanne Graham”
pm.test("Check if user with id1 is Leanne Graham", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData[0].name).to.eql("Leanne Graham");
});
API testing
### Step 5) 
Click send. There should now be two passed test results for your request.

API testing
*Note: There are different kind of tests that can be created in Postman. Try to explore the tool and see what tests will fit your needs.

How to Create Collections
Collections play an important role in organizing test suites. It can be imported and exported making it easy to share collections amongst the team. In this tutorial, we will learn how to create and execute a collection.

Let’s start in creating a collection:

### Step 1) 
Click on the New button at the top left corner of the page.

How to Create Collections
### Step 2) 
Select Collection. Create collection window should pop up.

How to Create Collections
### Step 3) 
Input the desired collection name and description then click create. A collection should now be created.

How to Create Collections
### Step 4) 
Go back to the previous Get request. Click Save

How to Create Collections
### Step 5)

Select Postman Test Collection.
Click Save to Postman Test Collection
How to Create Collections
### Step 6) 
Postman test collection should now contain one request.

How to Create Collections
### Step 7) 
Repeat steps 4-5 for the previous Post request so that collection will now have two requests.

How to Create Collections
How to Run Collections using Collection Runner
There are two ways to run a collection which is the Collection Runner and Newman. Let’s begin by executing the collection in Collection Runner.

### Step 1) 
Click on the Runner button found at the top of the page next to the Import button.

How to Run Collections using Collection Runner
### Step 2) 
Collection Runner page should appear such as below. Following is the description of various fields

How to Run Collections using Collection Runner
### Step 3) 
Run your Postman Test Collection by setting up the following:

Choose Postman test collection- Set iterations as 3
Set delay as 2500 ms
Click on Run Postman Test… button
How to Run Collections using Collection Runner
### Step 4) 
Run Results page should be displayed after clicking the Run button. Depending on the delay, you should see the tests as they execute.

Once tests have finished, you can see the test status if it is Passed or Failed and the results per iteration.
You see Pass status for the Get Requests
Since we did not have any tests for Post, there should be a message that the request did not have any tests.
How to Run Collections using Collection Runner
You can see how important it is that there are tests in your requests so that you can verify HTTP request status if successful and the data is created or retrieved.

## How to Run Collections using Newman
Another way to run a collection is via Newman. The main differences between Newman and Collection Runner are the following:

Newman is an add-on for Postman. You will need to install it separately from the Native App.
Newman uses the command line while Collection Runner has a GUI.
Newman can be used for continuous integration.
To install Newman and run our collection from it, do the following:

### Step 1) 
Install nodejs using this link: http://nodejs.org/download/

### Step 2) 
Open the command line and enter

```java
 npm install -g newman
```
Newman should now be installed on your computer.

### How to Run Collections using Newman
### Step 3) 
Once Newman has been installed, let’s go back to our Postman workspace.In the Collections box, click on the three dots. Options should now appear. Select Export.

How to Run Collections using Newman
### Step 4) 
Choose Export Collection as Collection v2.1 (Recommended) then click Export.

How to Run Collections using Newman
### Step 5) 
Select your desired location then click Save. It is advisable to create a specific folder for your Postman tests. A collection should now be exported to your chosen local directory.

### Step 6) 
We will also need to export our environment. Click on the eye icon beside the environment dropdown in Global, select Download as JSON. Select your desired location then click Save. It is advisable that the environment should be in the same folder as your collection.

How to Run Collections using Newman
### Step 7) 
Environment should now be exported to the same local directory as Collection.

### Step 8) 
Now go back to command line and change the directory to where you have saved the collection and environment.

```java
 cd C:\Users\Asus\Desktop\Postman Tutorial
```
### Step 9) 
Run your collection using this command:

```java
 newman run PostmanTestCollection.postman_collection.json -e Testing.postman_globals.json
```
Run results should now appear such as below.

How to Run Collections using Newman
For guide is a reference to some basic Newman codes for execution:

Run a collection only. This can be used if there is no environment or test data file dependency.
newman run <collection name>
Run a collection and environment. The -e indicator is for environment.
newman run <collection name> -e <environment name>
Run a collection with desired no. of iterations.
newman run <collection name> -n <no.of iterations>
Run with data file.
newman run <collection name> --data <file name>  -n <no.of iterations> -e <environment name>
Set delay time. This is important as tests may fail if it is run without delay due to requests being started without the previous request completing processing on the endpoint server.
newman run <collection name> -d <delay time>
Summary
API Testing using Postman: Postman is an application for testing APIs. Postman is one of the most popular tools used in API testing by sending requests to the webserver and getting the response back
Accessibility, Use of Collections, Collaboration, Continuous Integration, are some of the Key features to learn in Postman
It’s recommended you create an account in Postman, so your collections are available online
You can parameterize request in Postman
You can create Tests to verify a postman request
Collections can be run using Newman or Collection Runner

