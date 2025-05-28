# REACT-Router

![image](https://github.com/user-attachments/assets/35ed8189-c85e-4486-add6-e48e3b5903c0)


#### First, Understanding URL's
Every URL is essentially a request for some resource and each component of the URL serves to specify which resource is desired.</br>

#### URL Components
1. The scheme (eg. HTTP, HTTPS, mailto, etc), specifies what protocol is used to access the resource.
2. The domain (eg. codecademy.com), specifies the website that hosts the resource.
3. The path (eg. /articles), identifies the page displayed to the user.
4. The query string (eg. ?search=node), after a ‘?’ and assigns values to (search or filter) parameters.

Depending on the application requests coming into a server are handled differently.</br> 
REACT APPLICATIONS use REACT ROUTER for front end routing solution.</br>

#### Routing in web applications is defining how different URLs correspond to different views or components in an app.
This allows users navigate between pages without a full page reload, providing seamless.</br>

#### To use React Router Install it
Install react-router-dom package

      npm install --save react-router-dom@6

Add routing to a project by importing a common router such as `createBrowserRouter`

  import { createBrowserRouter } from 'react-router-dom';

Initialize the router. Call createBrowserRouter

  import { createBrowserRouter } from 'react-router-dom';
  const router = createBrowserRouter( /* application routes are defined here */ );

#### Different views of an application are called Routes (or React components) which need to be rendered.
First to render make router available at the root with React Router's `RouterProvider`

  import { RouterProvider, createBrowserRouter } from 'react-router-dom';
  const router = createBrowserRouter( /* application routes are defined here */ );

  export default function App () {
    return (
      <RouterProvider router={ router } />
    );
  }

#### Define Route components
  
