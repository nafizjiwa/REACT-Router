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

### Routing is defining how an app's different URLs correspond to different views or components.
##### Users can navigate between pages without a full page reload, providing seamless.</br>

#### Install React Router to Use It
##### Install the react-router-dom package</br>

      npm install --save react-router-dom@6

Add routing to a project by importing a common router such as `createBrowserRouter`</br>

      import { createBrowserRouter } from 'react-router-dom';

Initialize the router. Call createBrowserRouter</br>

      import { createBrowserRouter } from 'react-router-dom';
      const router = createBrowserRouter( /* application routes are defined here */ );

### Provide a Router 
##### Application views, called Routes (React components), need to be rendered.</br>
First, make router available at the root by importing React Router's `RouterProvider`(1)</br>
The router determines which routes to render when URL changes</br>
See below info about the path is passed down as a prop(2)</br>

    import { RouterProvider (1), createBrowserRouter } from 'react-router-dom';
    const router = createBrowserRouter( /* application routes are defined here */ );

    export default function App () {
      return (
        <RouterProvider router={ router } /> (2)
      );
    }

### Routing with `<Route>`
#### Now Define Routes to Render for different URL paths
###### *Routes are also called views or components*
2 ways to define routes: JSX or objects. Here we use JSX.</br>
To initialize 
First, `.createRoutesFromElements` converts JSX route elements into route objects </br>
Second, `.createBrowserRouter` accepts route objects to initalizes and create router objects which is passed into router provider.</br>

First import it.</br>

      import { RouterProvider, createBrowserRouter, createRoutesFromElements, Route } from `react-router-dom`

#### `<Route>` decides if a components needs rendering based on its URL path.</br>
<Route> Includes:
###### 1. A URL path to render
###### 2. An ELement prop of the component to render
`.createRoutesFromElements` 
      - configures <Route> to render a <PATH> component when the URL matches its path `/about`
      -Here render <About> when URL matches `/about`

       import About from './About.js';
       import { RouterProvider, createBrowserRouter, Route } from 'react-router-dom';
       const router = createBrowserRouter(createRoutesFromElements(
              <Route path='/about' element={ <About/> } />
       ));

      export default function App () {
        return (
            <RouterProvider router={ router } />
        );
      }


##### For components which render with every page view
   `1st Define a root-level component`
   `2nd then nest all other routes within the root-level component.`</br>

      /* imports ... */
      const router = createBrowserRouter(createRoutesFromElements(
        <Route path='/' element={ <Root/> }>
          // nested routes here will render along with this <Root/> component
        </Route>
      ));
##### When Navigating to one of the nested routes we Render that view along with all components within <Route>

#### Example of Defining Routes: Between `Root`'s Open and Close tags Use createBrowserRouter, createRoutesFromELements and Roote's <Route>

      const router = createBrowserRouter(createRoutesFromElements(
        <Route path="/" element={ <Root/> }>  {/* root route */}
          <Route path="mypath" element={ <MyComponent/> } />  {/* nested route */}
          <Route path="myotherpath" element={ <MyOtherComponent/> } />  {/* nested route */}
        </Route>
      ));



### Linking to Routes (Navigating within an app between pages )

Navigating within pages of an app causes pages to reload. </br>
So to prevent this React Router offers 2 anchors (whose default of page refresh are disabled).
1. Link
2. NavLink
   
Anchor Tag Syntax: A `to` prop (the redirect) and wrapped HTML for display (Here both redirect to /about view)

      <Link to="/about">About</Link>
      <NavLink to="/about">About</NavLink>

`/` refers to ablsolute paths meaning it navigates from the root directory.
First, import these components



  
