# REACT-ROUTER
#### For front-end or client side routing.
![image](https://github.com/user-attachments/assets/35ed8189-c85e-4486-add6-e48e3b5903c0)


#### First, Understanding URL's
- URL is a request for resources </br>
- URL components specify the resource is desired.

#### THE URL COMPONENTS
1. The scheme (eg. HTTP, HTTPS, mailto, etc), the rotocol used to get resources.
2. The domain (eg. infotoggle.com), the website with the resources.
3. The path (eg. /docs/guides), the page displayed to the user.
4. The query string (eg. ?search=node), after a ‘?’ are parameter values to search or filter.

#### REACT HOOKS RETURN --> 1. AN OBJECT AND 2. A FUNCTION

- REACT APPLICATIONS use REACT ROUTER for front end ROUTING.</br>
- A Router is needed to work with React Router</br>

## What is Routing?
- APP'S provide user's different PAGES using different URL'S/components.
- Routing NAVIGATES BETWEEN PAGES without a PAGE RELOAD, seamless.</br>

### To Use React Router Install It
##### Install react-router-dom </br>

      npm install --save react-router-dom@6

## Provide a Router 
##### App's views are called Routes or React components, They are rendered.</br>

1st, Define a router with createBrowserRouter (1)
2nd, Make Router available to the App with `RouterProvider`(2)</br>
      - The router determines which routes are rendered at differen URL's</br>
      - Pathes are passed down as props(3)</br>

    import { RouterProvider, createBrowserRouter } from 'react-router-dom';
    const router = createBrowserRouter(      (1)
                /*APP's routes defined here */ );

    export default function App () {
      return (   
        (2) <RouterProvider router={ router (3)} /> 
      );
    }

## ROUTING WITH `<Route>`
#### Once Router is set up. Define the Routes to Render
###### *Routes are also called views, URL paths or components*
######  *React Router's <Route> defines routes as either: JSX or objects.*</br>

   import { RouterProvider, createBrowserRouter, createRoutesFromElements, Route } from `react-router-dom`

To initialize Router </br>
###### *Convert from `route Element --> route object --> router Initialized`*</br>
1st, `.createRoutesFromElements(route element)` converts JSX route elements into route objects </br>
      - <Route> objects defines how the App responds to different URL's.</br>
2nd, `.createBrowserRouter(route object)` accepts <Route> objects and converts to a router object.</br>
3rd, <RouteProvider route={Router} /> <Router> is passed to Route Provider</br>

<Route> Component's Include:
###### 1. A URL path = the path which causes the Route to render
###### 2. An Element prop = the component to render
`.createRoutesFromElements` 
      - configures <Route> to render a component when the URL matches its path `/about`
      - Here render <About> component when URL matches `/about`

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

##### SOME COMPONENTS NEED TO BE RENDERED ON EACH PAGE VIEW LIKE A NAV BAR
   `1st Create a Root-level component`</BR>
   `2nd Nest all other routes within the root-level component.`</br>

      const router = createBrowserRouter(createRoutesFromElements(
        <Route path='/' element={ <Root/> }>  (1)
          // (2) nested routes here will render along with this <Root/> component
        </Route>
      ));
##### When Navigating to one of the nested routes
      What gets Rendered ---> the nested route and all <Root />'s components

#### Ex. Define Routes: Use createBrowserRouter, createRoutesFromELements and Root's <Route>

      const router = createBrowserRouter(createRoutesFromElements(
        <Route path="/" element={ <Root/> }>  {/* Root's route */}
          <Route path="mypath" element={ <MyComponent/> } />  {/* nested route */}
          <Route path="myotherpath" element={ <MyOtherComponent/> } />  {/* nested route */}
        </Route>
      ));

## LINKING TO ROUTES (Navigating within an app/webpage site pages )
Navigating between pages of an app causes pages to reload. </br>
React Router has 2 anchors to prevent reloading (the anchor's default to refresh is disabled)</br>
2 Anchor Tags Syntax: Has a `to` prop (the redirect) and `wrapped HTML` 

     /* First, Components are imported ... */
     import {Link, NavLink } from 'react-router-dom';
     1 .<Link to="/about">About</Link> (to = href)
     2. <NavLink to="/about">About</NavLink>

`/` - ablsolute path - meaning it navigates from the root directory.

#### How is `NavLink` Different? -->  `<NavLink to="path">Click Me</NavLink>`

When `to` prop path matches URL path it automatically gives the link an `.active`class .</br>

##### This impacts Styling: </br>
We can define CSS styles for this .active class name to highlight the viewed content.</br>
Functions can be passed to className to customize styling of the NavLink</br>
*Example

    <NavLink 
      to="about" 
      className={ ({ isActive }) => isActive? 'nav-link nav-link-active' : 'nav-link'}
      //Different styling applied when active 'activeNavLink class' or not active
    > About </NavLink>

- Here NavLink className property accepts a function with a destructured object = isActive.</br>  
***Above className prop applies style dependent on if NavLink is active or not active.</br> 

## DYNAMIC ROUTES
###### * `Static Route paths` match a single path `/about`* </br>
###### * `Dynamic Route paths` match a pattern `/about/:someTitle` * </br>
- React Router uses `URL parameters` for Dynamic Routes </br>
- URL parameter --> `/:URLParameter`</br>

      const route = createBrowserRouter(createRoutesFromElement(
        <Route path='/articles/:titlePlaceholder' element={ <Article /> }/>
      ))
Here path = `/articles/:titlePlaceholder` the URL parameter = :titlePlaceholder</br>
- So NAVIGATING to pages similar to `/articles/:titlePlaceholder`, LIKE:</br>
            - `/articles/react, or /articles/html-or-css` <br>
- RENDERS --> The `<Article>` component</br>

Creating a Dynamic Route, 
- Render a <Route> component with path prop = `dynamic segment` (:URLParameter or placeHolder)

      <Route path='path/:dynamicSegment' element={ <MyComponent/> }/>
#### Rendering Dynamic routes requires the URL Parametes

## usParams
- To access URL Parameter values use React Router's `useParams()`</br>
 -useParams() --> returns an object of mapped URL Parameters names: their values</br>

      --> Visiting /articles/objects renders Article
      import { Link, useParams } from 'react-router-dom';

      export default function Article() {
  
        let { title } = useParams();      // useParams() returns an object
         // Destructuring extracts the value 
         // of URL parameter and stores it in title 
        return (
          <article>
            <h1>{title}</h1>   //Article is rendered and title value displayed
          </article>
       );
      }
## NESTED ROUTES
A route (Child) within a route (Parent).
The child Route path is relative to the parent Route's path.

      /* imports ... */
      const router = createBrowserRouter(createRoutesFromElement(
        <Route path='/about' element={ <About/> }> **If path matches /about `<About>` Rendered
              <Route path='secret' element={ <Secret/> }>  />  
                 **about is exclude from this path b/c it's relative to parent
                 **If path matches /about/secret `<Secret >` and `<About >` Rendered
        </Route> 
      ));

## `<Navigate> COMPONENT` (or Redirect)
- Link & NavLink require user interaction
- <Navigate> when rendered automatically redirects to the location of `to` prop.</br>
- All declarative redirections.</br>

      import { Navigate } from 'react-router-dom';
      const UserProfile = ({ loggedIn }) => {
        if (!loggedIn) {
          return (  <Navigate to='/' /> )
        }
        return (
          // ... user profile content here
        )  
      }
##### Navigate is rendered sending user to `/` page if loggedIn true .</br>

## `useNavigate() HOOK`
- A hook used to imperatively navigate between pages in a React app </br>
- `const navigate = useNavigate();` Returns a navigate function</br>
- navigate can use either a path string or an integer value to trigger a redirect </br>
      - navigate('/somepathSTRINGValue');  // navigates to /somepath </br>
      - navigate('-2');  // navigates two paths previous</br>

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
                  <button onClick={() => navigate(-2)}>
                   Go Back
                  </button>
          </form>
        )
      }

### `QUERY PARAMETERS`
- Appeaar in URL following ? --> `?parameterName=value`.</br>
- useSearchParams() - Grabs query parameter values</br>
                    - Returns `URLSearchParams object` and a `function` to update it.
                    - `[ searchParams, setSearchParams ] = useSearchParams()`;
                    - Use searchParams get method to retrieve the search parameters value.
                    - searchParams.get('get this search parameters value');
##### Eg. A site we want to Visit: `"/list?order=DESC"`</br>
- To get query param value use `searchParams` :
        - `const sortOrder = searchParams.get('order')`--> DESC</br>
- To update a query parameter use `setSearchParams`:
        - onClick = { () => setSearchParams( { order: 'ASC'} )}</br>
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
      // use createSearchParams it takes an object --> transforms to query string (form order=ASC)
      const searchQueryString = createSearchParams(searchQueryParams);
      //Then call navigate: 
      //Pass in object with
            //1. Pathname: which path to navigate AND
            //2. Search:  the query parameters to append to path 
                  navigate({
                    pathname:'/list',
                    search: `?${searchQueryString}`
                  })


--------------------------------------------------------------------------------------------------------------------------------------
TO CREATE ROUTES:

1. SETUP REACT ROUTES</br>
      install react router --> npm install --save react-router-dom@6</br>
      Import RouterProvider from react-router-dom to enable routing in application</br>
      In App's return statement --> <RouterProvider router= {created routes here}</br>
            const nameOfConstant = { JSX Ojbect }</br>
      
2. CREATE ROUTES
      React Router functions and components convert JSX Objects to route objects
            `RouteProvider, createRoutesFromElements, createBrowserRouter, Route`
      FIRST, initialize variable where routes are stored.
      For content which is always displayed on a webpage create "root" route to the path "/" which renders the Root component.
      Initialize a Route called ==> const routeElement = <Route path='/somepath' element{<MyComponent />} />
      Route element can't be inputed in RouterProvider(need a route object).
   
         First create Route object use createRoutesFromElements(routeElement) --> route object
               const routes = createRoutesFromElements(<Route path='/somepath' element={<MyComponent />} />)
         Second create a router, the route object from createRoutesFromElements input into createBrowserRouter
               const router = createBrowserRouter(
                        createRoutesFromElements(<Route path="/somepath" element={ <MyComponent /> }/>) );

3. CREATE NESTED/INDEX ROUTES   
   The Root Route '/' contains content which is always displayed across different subpages.
   Nested Route uses its parents' (or root route) path to render
   
           const router = createBrowserRouter(createRoutesFromElements(
              <Route path='/' element={ <Root/> }>       /* root route or parent */
                // nested routes here will render along with this <Root/> component
                     eg. <Route path="mypath" element={ <MyComponent/> } />  /* nested route */
              </Route>
            ));
   
4. RENDER NESTED ROUTE
   To render nested routes the parent is told where to render the nested element
   FIRST, IMPORT  Outlet from react-router-dom
   SECOND, Use Outlet in parent route to indicate where child route is rendered
   
5. URL PARAMETERS IN REACT COMPONENTS
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
         
6.REACT ROUTER FEATURES ON A SEARCH BARS</br>
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

7. To conditionaly REDIRECT a user use REACT ROUTER'S Navigate COMPONENT </br>
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
