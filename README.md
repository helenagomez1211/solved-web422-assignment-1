Download Link: https://assignmentchef.com/product/solved-web422-assignment-1
<br>



This first assignment will help students obtain the sample data loaded in MongoDB Atlas for the WEB422 course as well as to create (and publish) a simple Web API to work with the data.

Specification:

<strong><u>Step 1:</u></strong> Loading the “Sample Data” in MongoDB Atlas

The first step for this assignment is to create a new “Project” in your existing MongoDB Atlas account  (if you have deleted your account from last semester, please revisit the documentation here from WEB322 – <a href="https://web322.ca/notes/week08">https://web322.ca/notes/week08</a><a href="https://web322.ca/notes/week08">)</a>.

Assuming that you have an account in MongoDB Atlas, please follow the instructions located below (from the WEB422 website) to create a new “Project”, “Cluster” and “Load the Sample Dataset”.




MongoDB Sample Data Instructions – <a href="https://web422.ca/notes/mongodb-sample-data">https://web422.ca/notes/mongodb</a><a href="https://web422.ca/notes/mongodb-sample-data">–</a><a href="https://web422.ca/notes/mongodb-sample-data">sample</a><a href="https://web422.ca/notes/mongodb-sample-data">–</a><a href="https://web422.ca/notes/mongodb-sample-data">data</a>

<strong><u>Step 2</u></strong><strong>:</strong> Building a Web API

Once you have completed the guide (Step 1), and have the data loaded in a new Project within your MongoDB Atlas account, we must build and publish a Web API to enable code on the client-side to work with the data.

To get started:

<ul>

 <li>First create a folder (ie: “salesAPI”) for your project somewhere on your machine. Next, download the Assignment 1 boilerplate files from here:</li>

</ul>

<a href="https://ict.senecacollege.ca/~patrick.crawford/shared/summer-2020/web422/A1/A1.zip">https://ict.senecacollege.ca/~patrick.crawford/shared/summer</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/summer-2020/web422/A1/A1.zip">–</a><a href="https://ict.senecacollege.ca/~patrick.crawford/shared/summer-2020/web422/A1/A1.zip">2020/web422/A1/A1.zip</a>

<ul>

 <li>Once A1.zip has been downloaded, extract the files and add them to your newly created “salesAPI” folder.</li>

 <li>Open this folder in Visual Studio Code (which should now contain server.js and the “modules” folder) and perform the usual tasks for creating a web server from scratch in Visual Studio Code (ie: “<strong>npm init</strong>“, followed by the “npm install” tasks for this project, such as “express”, “cors” and “body-parser”).</li>

 <li>Finally, initialize an empty Git repository for this folder using the command “git init”</li>

</ul>

Viewing / Modifying Existing Files:

<h1>modules/data-service.js</h1>

This file (located in the “modules” directory) does not need to be modified at all.  It exists to provide the 6 functions required by our Web API for this particular (sales) dataset, ie:

<ul>

 <li><strong>initialize()</strong>: Establish a connection with the MongoDB server and initialize the “Sale” model with the “sales” collection</li>

 <li><strong>addNewSale</strong>(<strong>data</strong>): Create a new sale in the collection using the object passed in the “data” parameter</li>

 <li><strong>getAllSales</strong>(<strong>page</strong>, <strong>perPage</strong>): Return an array of all sales for a specific page (sorted by <strong>saleDate</strong>), given the number of items per page. For <em>example</em>, if <strong>page</strong> is <strong>2</strong> and <strong>perPage</strong> is <strong>5</strong>, then this function would return a sorted list of sales (by <strong>saleDate</strong>), containing items <strong>6 – 10.  </strong>This will help us to deal with the large amount of data in this dataset and make paging easier to implement in the UI later.</li>

 <li><strong>getSaleById(Id)</strong>: Return a single sale object whose “_id” value matches the “Id” parameter</li>

 <li><strong>updateSaleById(data</strong>,<strong>Id)</strong>: Overwrite an existing sale whose “_id” value matches the “Id” parameter, using the object passed in the “data” parameter.</li>

 <li><strong>deleteSaleById(Id)</strong>: Delete an existing sale whose “_id” value matches the “Id” parameter</li>

</ul>

<strong> </strong>

<h1>modules/salesSchema.js</h1>

<strong> </strong>

This file (located in the “modules” directory) does not need to be modified at all.  It exists to provide the schema for this particular (sales) dataset

<strong> </strong>

<h1>server.js</h1>

<strong> </strong>

Here is where the bulk of the work needs to be done.  We must update it to add the 6 required routes (listed below) as well as to provide our dataService module with a valid MongoDB connection string.




<h1>Obtain the connection string</h1>

<ul>

 <li>Ensure that you’re looking at the overview for your newly created Cluster (within your newly created Project) that contains the sample data.</li>

</ul>







<ul>

 <li>Next, click the “CONNECT” button and grab the connection string using the “Connect Your Application” button. <strong>NOTE: </strong>If you have not yet created a user for this database, or whitelisted the ip: 0.0.0.0/0, please proceed to do this first.</li>

 <li>Once you have your connection string, it should look <em>something like this</em>:</li>

</ul>

<strong>mongodb+srv://userName:&lt;password&gt;@cluster0-abc0d.mongodb.net/test?retryWrites=true&amp;w=majority</strong>

<ul>

 <li>Next, replace the entire string &lt;password&gt; with your password for this cluster (do not include the &lt; &amp; &gt; characters)</li>

 <li>Finally, replace the text <strong>test</strong> with the database name: <strong>sample_supplies</strong> and add the updated connection string to line 6 of your server.js file (as a parameter to your dataService() function call)</li>

</ul>




<h1>Add the routes</h1>

<strong> </strong>

The next piece that needs to be completed before we have a functioning Web API is to actually define the routes (listed Below).  <strong>Note</strong>: All routes must return JSON formatted data.  If plain text is to be returned, it must be sent in an object with property “message”, ie: {message: “new sale successfully added”}.  Do not forget to return an error message if there was a problem.

<strong> </strong>

<ul>

 <li><strong>POST /api/sales </strong></li>

</ul>

This route uses the body of the request to add a new “Sale” document to the collection and return a success / fail message to the client.

<ul>

 <li><strong>GET /api/sales </strong></li>

</ul>

This route must accept the numeric query parameters “page” and “perPage”, ie:

/api/sales?page=1&amp;perPage=5.  It will use these values to return all “Sales” objects for a specific “page” to the client.

<ul>

 <li><strong>GET /api/sales </strong></li>

</ul>

This route must accept a numeric route parameter that represents the _id of the desired sale object, ie: /api/sales/5bd761dcae323e45a93ccfe8.  It will use this parameter to return a specific “Sale” object to the client.

<ul>

 <li><strong>PUT /api/sales </strong></li>

</ul>

This route must accept a numeric route parameter that represents the _id of the desired sale object, ie: /api/sales/5bd761dcae323e45a93ccfe8 as well as read the contents of the request body.  It will use these values to update a specific “Sale” document in the collection and return a success / fail message to the client.

<ul>

 <li><strong>DELETE /api/sales </strong></li>

</ul>

This route must accept a numeric route parameter that represents the _id of the desired sale object, ie: /api/sales/5bd761dcae323e45a93ccfe8.  It will use this value to delete a specific “Sale” document from the collection and return a success / fail message to the client.




<strong><u>Step 3</u></strong><strong>:</strong> Pushing to Heroku

Once you are satisfied with your application, deploy it to Heroku:

<ul>

 <li>Ensure that you have checked in your latest code using <strong>git </strong>(from within Visual Studio Code)</li>

 <li>Open the integrated terminal in Visual Studio Code</li>

 <li>Log in to your Heroku account using the command <strong>heroku login</strong></li>

 <li>Create a new app on Heroku using the command <strong>heroku create</strong></li>

 <li>Push your code to Heroku using the command <strong>git push heroku master</strong></li>

</ul>

<strong>IMPORTANT NOTE: </strong>Since we are using an “<strong>unverified” free </strong>account on Heroku, we are limited to only <strong>5 apps</strong>, so if you have created 5 apps already, you must delete one (or verify your account with a credit card).