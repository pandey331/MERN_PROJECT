# MERN_PROJECT

mport express from "express";
import bodyParser from "body-parser";
import mongoose from "mongoose";
import cors from "cors";
import dotenv from "dotenv";
import multer from "multer";
import helmet from "helmet";
import morgan from "morgan";
import path from "path";
import { fileURLToPath } from "url";

/*CONFIGURATION*/

const __filename = fileURLToPath(import.meta.url);
const __dirname=path.dirname(__filename);
dotenv.config();
const app=express();
app.use(express.json());
app.use(helmet());
app.use(helmet.crossOriginResourcePolicy({policy:"cross-origin"}));
app.use(morgan("common"));
app.use(bodyParser.json({limit: "30mb" , extended:true}));
app.use(bodyParser.urlencoded({limit: "30mb" , extended:true}));
app.use(cors());
app.use("/assests" , express.static(path.join(__dirname, 'public/assets')));

EXPLAINATION:-

1.express:
express is a popular Node.js web application framework. It simplifies the process of building web applications and APIs by providing a set of robust features and utilities for handling HTTP requests, routing, and more.
body-parser:

2.body-parser is a middleware for Express.js that parses the incoming request body and makes it available as an object in the req.body property. It is commonly used for parsing JSON or form data sent in POST requests.

3.mongoose:
mongoose is an Object-Data Modeling (ODM) library for MongoDB and Node.js. It provides a structured way to interact with MongoDB databases and define data models with schemas.

4.cors (Cross-Origin Resource Sharing):
cors is a middleware that enables or controls Cross-Origin Resource Sharing for your Express.js application. It helps in handling HTTP requests from different origins and allows you to specify which origins are permitted to access your resources.
dotenv:

5.dotenv is a module that loads environment variables from a .env file into the Node.js environment. It is commonly used to store configuration variables like API keys or database connection strings securely.

6.multer:
multer is a middleware for handling multipart/form-data, which is typically used for uploading files in HTTP requests. It allows you to easily process and store uploaded files on your server.

7.helmet:
helmet is a security middleware for Express.js applications. It helps to set various HTTP headers that enhance security by protecting against common web vulnerabilities like XSS (Cross-Site Scripting) and CSRF (Cross-Site Request Forgery).
morgan:

8.morgan is a middleware for logging HTTP requests in your Express.js application. It provides information about each incoming request, such as the request method, URL, status code, and response time.

9.path:
path is a built-in Node.js module that provides utilities for working with file and directory paths. In your code, it's used to manipulate and construct file paths.
fileURLToPath:

10.fileURLToPath is a function provided by the url module in Node.js. It is used to convert a file URL (in the form of a file: URL) to a file path. This is commonly used when working with ES Modules.
These packages and configurations help set up your Express.js application with various features, including handling requests, parsing data, securing it, logging, and serving static assets.
**************************************************************************************************************************
const storage =multer.diskStorage({
    destination: function(req,file,cb){
        cb(null,"public/assets");
    },
});
const upload=multer({storage});

/*MONGOOSE SETUP*/

const PORT = process.env.PORT || 6001;
mongoose
 .connect(process.env.MONGO_URL,{
    useNewUrlParser: true,
    useUnifiedTopology: true,
})
.then(() => {
    app.listen(PORT,()=> console.log(`Server Port: ${PORT}`));
})
.catch((error) => console.log(`${error} did not connect` ));

EXPALINATION:
Certainly! The code you provided is setting up multer for handling file uploads and connecting to a MongoDB database using Mongoose. Let's break down each part:

const storage = multer.diskStorage({ destination, filename }):

This code is configuring multer's storage engine using diskStorage. The destination function determines where the uploaded files will be stored on the server. In this case, it specifies that uploaded files should be saved in the "public/assets" directory.

const upload = multer({ storage }):

Here, you are creating an instance of multer called upload and passing the storage configuration you defined earlier. This upload instance can be used as middleware to handle file uploads in your Express application.

//Mongoose Setup//

This section of the code sets up the connection to a MongoDB database using the Mongoose library.
const PORT = process.env.PORT || 6001;:
This line specifies the port on which your Express server will listen. It uses the process.env.PORT environment variable if it exists; otherwise, it defaults to port 6001.

mongoose.connect(process.env.MONGO_URL, { useNewUrlParser: true, useUnifiedTopology: true }):
This line establishes a connection to the MongoDB database specified by the MONGO_URL environment variable. It uses the useNewUrlParser and useUnifiedTopology options to configure the connection settings. These options are recommended for modern versions of Mongoose and MongoDB.

.then(() => { ... }) and .catch((error) => { ... }):
These methods are used to handle the promise returned by the mongoose.connect function.
If the database connection is established successfully, the server is started, and a message is logged to the console.
If there is an error connecting to the database, an error message is logged to the console.
Overall, this code sets up the necessary configurations for handling file uploads with multer and establishes a connection to a MongoDB database using Mongoose. It also ensures that the Express server listens on the specified port, allowing your application to serve HTTP requests and interact with the database.
