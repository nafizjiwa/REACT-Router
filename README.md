# REACT-ROUTER
#### For front-end or client side routing.
![image](https://github.com/user-attachments/assets/35ed8189-c85e-4486-add6-e48e3b5903c0)


#### First, Understanding URL's
- The URL is a request for resource and </br>
- Each URL component specifies which resource is desired.

#### URL Components
1. The scheme (eg. HTTP, HTTPS, mailto, etc), what protocol used to get resource.
2. The domain (eg. infotoggle.com), the website with the resource.
3. The path (eg. /docs/guides), the page displayed to the user.
4. The query string (eg. ?search=node), after a ‘?’ are parameter values to search or filter.

#### REACT HOOKS RETURN --> 1. AN OBJECT AND 2. A FUNCTION

- REACT APPLICATIONS use REACT ROUTER for front end ROUTING.</br>
- A Router is needed to work with React Router</br>

## Routing is defining how an app's different URLs correspond to different views or components.
##### Users can navigate between pages without a full page reload so its seamless.</br>

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

First, make router available to the app by importing React Router's `RouterProvider`(1)</br>
The router determines which routes to render at differen URL's</br>
See below info about the path is passed down as a prop(2)</br>

    import { RouterProvider (1), createBrowserRouter } from 'react-router-dom';
    const router = createBrowserRouter( 
                /* application routes are defined here */ );

    export default function App () {
      return (
        <RouterProvider router={ router } /> (2)
      );
    }

### ROUTING WITH `<Route>`
#### Now Define Routes to Render for different URL paths
###### *Routes are also called views or components*
2 ways to define routes: JSX or objects. Here we use JSX.</br>
Convert from `route Element --> route object --> initialized router`</br>
To initialize </br>
First, `.createRoutesFromElements(route element)` converts JSX route elements into route objects </br>
Second, `.createBrowserRouter(route object)` accepts route objects and creates a router object.</br>
Third, <RouteProvider route={Router} /> router passed to Route Provider</br>

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


##### For components that need to render with every page view
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

When property `to`= URL path the link has an `.active` style class added to it.</br>

##### This impacts Styling: </br>
We can define CSS styles for this .active class name to highlight the viewed content.</br>
Functions can be passed to className or style to customize styling of the NavLink</br>
*Example

    <NavLink 
      to="about" 
      className={ ({ isActive }) => isActive? 'activeNavLink' : 'inactiveNavLink'}
      //Different styling applied when active 'activeNavLink class' or not active
    > About </NavLink>

NavLink className props can accept a function that receives an object (destructure this object to just a property </br>called isActive). The function body should return the string 'nav-link nav-link-active' if isActive is true</br>
and 'nav-link' if false.</br>
NavLink‘s className prop can accept a function that receives a NavLink-related object which includes an isActive property. The isActive property can be used to modify the className string used

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
The useParam() hook can access these URL Parameter values </br>
--> it returns an object of key:value pairs with URL Parameters names to values</br>
A Route Pattern `/posts/:postId` Matches this `/posts/123` --> params returns --> Key: Value `params.postId="123"`</br>

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

### `<Navigate> COMPONENT` (or Redirect)
Unlike Link or NavLink, which require user interaction, Navigate automatically redirects users when certain conditions are met to the location specified by the `to` prop.</br>
All are declarative redirections.</br>
Remember navigate function can be called with a string path or an integer value </br>
      // navigate('/somepathSTRING');  // navigates to /somepath </br>
      // navigate('-2');  // navigates two paths previous</br>

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

### `useNavigate() HOOK`
A hook used to imperatively navigate between pages in a React app </br>
Returns a navigate function --> `const navigate = useNavigate();`</br>

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
            // get the navigate function
      const navigate = useNavigate();

      //Define an object:
      const searchQueryParams = {
              order: 'ASC'
              The object is a key: value pair
              Query Parameter Name: Query Parameter "Value"
            }
      // use createSearchParams it akes an object --> transforms to query string (form order=ASC)
      const searchQueryString = createSearchParams(searchQueryParams);
      //Then call navigate: 
      //Pass in object with
            //1. Pathname: which path to navigate AND
            //2. Search:  the query parameters to append to path 
                  navigate({
                    pathname:'/list',
                    search: `?${searchQueryString}`
                  })


TO CREATE ROUTES:

1. SETUP REACT ROUTES</br>
      install react router --> npm install --save react-router-dom@6</br>
      Check, If installed shows in dependency list</br>
      Import React Router's RouterProvider to communicate with application</br>
      import { RouterProvider } = from 'react-router-dom';</br>
      Use React Router in App return statement --> <RouterProvider router= {routes here}</br>
      The value of the attribute router equals the routes stored in a constant which is a JSX object.</br>
      const nameOfConstant = { JSX Ojbect }</br>
      
2. CREATE ROUTES
      React Router functions and components convert JSX Objects to route objects
            `RouteProvider, createRoutesFromElements, createBrowserRouter, Route`
      FIRST, initialize variable where routes are stored.
      For content on a page like nav bars which are always displayed regardless of the
      path the user is on we need a "root" route to the path "/" which renders the element 
      Root component.
      Initialize a Route called ==> const routeElement = <Route path='/somepath' element{<MyComponent />} />
      Route element can't be inputed in RouterProvider(need a route object).
   
         First creaate Route object use createRoutesFromElements(routeElement) --> route object
               const routes = createRoutesFromElements(<Route path='/somepath' element={<MyComponent />} />)
         Second create a router, the route object from createRoutesFromElements input into createBrowserRouter
               const router = createBrowserRouter(
                        createRoutesFromElements(<Route path="/somepath" element={ <MyComponent /> }/>) );

3. CREATE AN INDEX ROUTE OR NESTED ROUTES   
   The Root Route '/' contains content for layouts where certain elements remain consistent across different subpages a user visits.
   An Index Route uses its parents' (or root route) path to render
   
           const router = createBrowserRouter(createRoutesFromElements(
              <Route path='/' element={ <Root/> }>       {/* root route or parent */}
                // nested routes here will render along with this <Root/> component
                     eg. <Route path="mypath" element={ <MyComponent/> } />  {/* nested route */}
              </Route>
            ));
   
5. RENDER NESTED ROUTE
   To render nested routes the parent must be told where to render the nested element
   FIRST, IMPORT  Outlet from react-router-dom
   SECOND, Use Outlet in parent route to indicate where child route is rendered
   
6. URL PARAMETERS IN REACT COMPONENTS
         Add URL parameters to a Route path with a colon `:` this is a dynamic path
   
         <Route path='/' element={ <MyComponent/> }>
              <Route path=':myType' element={ <MyTypedComponent /> }/>
                     {/* this nested route has a dynamic path which*/}
                     {/* Renders with paths like `/type1` or `/type2` */}
         </Route>
   To get the value of a URL parameter `:param` call useParam() ==> object</br>
   Destructure object for param property:</br>
         `const { param } = useParams()`</br>
   Syntax for a Route that renders a component with multiple URL parameters</br>
         `<Route path='/path/:for/:route' element={ <SomeComponent /> } />`</br>
   Destructuring syntax for a dynamic path URL parameter eg. /:foo/:bar from the object returned by a call to useParams()
         `const { foo, bar } = useParams()`</br>
         
7.REACT ROUTER FEATURES ON A SEARCH BARS</br>
   ***NOTE: QUERY PARAMETERS ARE FOUND AFTER QUESTION MARK IN URL</br>
   `?` ***  URL --> `.../search?name=fido`    QUERY PARAMETER --> `?name=fido`</br>
   First, User inputs a query in search bar. Second, that parameter OR input </br>
   upadates the URL -> Third, User is THEN redirected to pages of that query</br>
   `To update the URL WITH THE A USERS QUERY ---> USE THE useNAVIGATION() HOOK`</br>
         `Imperatively.`</br>
         
   #### 1ST: Call useNavigation() in Component:</br>
   
         const Component = () => {
              const navFunction = useNavigate();
              //...
            }
    #### 2ND: Transform query object ==> URLSearchParams object with `createSearchparams()`</br>
    
          const searchQ = {
               sort: 'ASC'
          }
         const urlQuery = createSearchParams(searchQ);
                     // will create a query that looks like sort=ASC
                     
    #### 3RD: Use the Navigation function to redirect user to SPECIFIC PATH BASED ON</BR>
    USER'S INPUT ---> `/search?keyName=searchValue`</br>

         navigate({
             pathname: '/somepath',
             search: `?${searchQuery}`  // notice you'll need the leading `?`
           });
    #### 4TH: After searchbar user input --> COMPONENT RENDERED --> REDIRECTION TO PATH</BR>
          --> `/search?keyName=searchValue`</br>
         NOTE* query parameter is not part of path</br>

         Add a component or nested route to Root Route which renders when path matches `/search`
         <Route path='/search' element={ <SearchComponent/> } />

      To render the matching user search query get the search parameter value from ?keyName=searchPValue</br>
         call useSearchParams() hook and destructure searchParam property it returns</br>

         const [ searchParamPropertyValue ] = useSearchParams()

     #### FINALLY, RETRIEVE THE 'name' QUERY PARAMETER WITH searchParams get method and replace the value of petNameToFind with it.</br>
  
         const searchParamValue = searchParams.get('nameOfProperty')
   
`**NOTE** To create a ADDITIONAL PAGES OTHER THAN THE MAIN for users to navigate to based on URL</br>`
- Add a nested route to the Root Route that renders a component when the URL the user wants</br>
      to navigate to matches the path associated with that component. </br>
                        <Route path="/path/for/route" element={ <someComponent/>}/></br>
- To test if the nest Route works enter the URL associated with that path in URL address field</br>

8. To conditionaly REDIRECT a user use REACT ROUTER'S Navigate COMPONENT </br>
      In a components return statement use the Navigate component.</br>
         The <Component /> associated with the path in the 'to' attribute will render
   
                Component(){
                  return (
                     <Navigate to='/' />

const navigate = useNavigate(); </br>
Component(){ 

      return (  
            navigate('/somepath');  // navigates to /somepath  
            navigate('-2');  // navigates two paths previous
      ) }

---------------------------------------------------------------------------------------------------------------------------------
