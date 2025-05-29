# REACT-ROUTER
#### For front-end or client side routing.
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

## Routing is defining how an app's different URLs correspond to different views or components.
##### Users can navigate between pages without a full page reload, providing seamless.</br>

#### Install React Router to Use It
##### Install the react-router-dom package</br>

      npm install --save react-router-dom@6

Create a router with `createBrowserRouter`</br>

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

### ROUTING WITH `<Route>`
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



### LINKING TO ROUTES (Navigating within an app's pages )

Navigating between pages of an app causes pages to reload. </br>
React Router offers 2 anchors to prevent reloading (anchor's default of refresh page is disabled).
1. Link
2. NavLink
   
Anchor Tag Syntax: A `to` prop (the redirect) and `wrapped HTML` (Here both redirects to the /about view)

     /* First, Components are imported ... */
     import { ..., Link, NavLink } from 'react-router-dom';
     <Link to="/about">About</Link> (to = href)
     <NavLink to="/about">About</NavLink>

`/` refers to ablsolute paths meaning it navigates from the root directory.
#### How is `NavLink` Different?

     <NavLink to="path">Click Me</NavLink>

When URL path = `to` prop the `.active` style class is added to the link</br>
##### This impacts Styling: </br>
CSS styles can be defined for an .active class name.</br>
Functions can be passed to className or style to customize styling</br>
*Example

    <NavLink 
      to="about" 
      className={ ({ isActive }) => isActive? 'activeNavLink' : 'inactiveNavLink'}
    > About </NavLink>

***Above a function is passed to className prop this applies a class dependent on if NavLink is active or not active.

### DYNAMIC ROUTES
Static route paths match single a path `/about`</br>
Dynamic route paths match pattern `/about/:someTitle` </br>
React Router renders their components using the `URL parameters`</br>
URL parameters follow a colon `:NameOfPlacehoder`</br>

      const route = createBrowserRouter(createRoutesFromElement(
        <Route path='/articles/:titlePlaceholder' element={ <Article /> }/>
      ))
Here path property `/articles/:titlePlaceholder` contains URL parameter :titlePlaceholder</br>
So when the user navigates to pages similar to `/articles/:titlePlaceholder:`</br>

      /articles/react, or
      /articles/html-or-css
The `<Article>` component gets rendered</br>

To Create a dynamic route, 
Render a Route component with a path prop that includes a `dynamic segment` = `:URLParameter or placeHolder`

      <Route path='path/:dynamicSegment' element={ <MyComponent/> }/>

#### To Render Dynamic routes the Value of URL Parameters is needed to display the component
The useParam() hook can access this value 
--> returns an object with URL Parameters names to values

      --> When a user visits /articles/objects Article is rendered.
      import { Link, useParams } from 'react-router-dom';

      export default function Article() {
  
        let { title } = useParams();
        // title will be equal to the string 'objects' returned by useParams
         // Destructuring extracts the value of URL param storing in title
         // The title will be rendered/displayed in the <h1>
        return (
          <article>
            <h1>{title}</h1>
          </article>
       );
      }
### NESTED ROUTES

A route (Child) within a route (Parent).
The child Route path is relative to the parent Route's path.

      /* imports ... */
      const router = createBrowserRouter(createRoutesFromElement(
        <Route path='/about' element={ <About/> }> {/* About renders if path starts with /about */}
              <Route path='secret' element={ <Secret/> }>  />  
              {/* we can exclude /about from this path since it is relative to its parent */}
        </Route> 
      ));

When the path matches /about the `<About >` component is rendered</br>
When the path matches /about/secret the `<Secret >` and `<About >` components are rendered.

### `<Navigate>` (or Redirect)
Unlike Link or NavLink, which require user interaction, Navigate automatically redirects users when certain conditions are met to the location specified by the `to` prop.</br>
All are declarative redirections.</br>

      import { Navigate } from 'react-router-dom';

      const UserProfile = ({ loggedIn }) => {
        if (!loggedIn) {
          return (
            <Navigate to='/' />
          )
        }
        return (
          // ... user profile content here
        )  
      }
##### The UserProfile component renders if loggedIn prop is false Navigate is returned and then rendered sending user to `/` page.</br>

### `useNavigate()`
This hook updates the browswer location imperatively by returning a navigate function.</br>
`const navigate = useNavigate();`</br>
#### To trigger a redirect
      import { useNavigate } from `react-router-dom`;

      export const ExampleForm = () => {
        const navigate = useNavigate()
        const handleSubmit = e => {
          e.preventDefault();
          navigate('/')
        }
        return (
          <form onSubmit={handleSubmit}>
            {/* form elements */ }
          </form>
        )
      }
#### Navigate through history stack with a back button
The funciton navigate(insert integer here) allows positve integers for forward and negative for backward in history</br>

      import { useNavigate } from `react-router-dom`

      export const BackButton = () => {
        const navigate = useNavigate()
        return (
          <button onClick={() => navigate(-1)}>
            Go Back
          </button>
        )
      }
### `QUERY PARAMETERS`
Syntax: In URL --> `?parameterName=value`.</br>
useSearchParams() hook is used to access query parameters of a path or alter the path</br>
SInce a hook --> returns object and a function. `[ searchParams. setSearchParams ] = useSearchParams()`;</br>
const sortOrder = searchParams.get('query parameter to search'); queryParams object has a get method which retrieves the query parameters value.</br>
##### So site we want to Visit: `"/list?order=DESC"`</br>
To get a query parameters value use searchParams: `const sortOrder = searchParams.get('order')`</br>
To update a query parameter use setSearchParams: onClick = {
() => setSearchParams( { order: 'ASC'} )}</br>
When clicked the the component is rendered and search parmameter updated to 'ASC'</br>
##### Navigate to Different site  `"/list?order=ASC"`

      import { useNavigate, createSearchParams } from 'react-router-dom';
      // get navigate function
      const navigate = useNavigate();

      //Define an object where the key is is the query parameter name and value is query parameter value
      const searchQueryParams = {
        order: 'ASC'
      }
      // use createSearchParams which takes an object and transforms it to a query string of the form order=ASC
      const searchQueryString = createSearchParams(searchQueryParams);
      //call navigate: 
      //pass in an object with
            //1. Pathname indicating that path to navigate & 2. Search indicating the query parameters to append to path
      navigate({
        pathname:'/list',
        search: `?${searchQueryString}`
      })
















  
