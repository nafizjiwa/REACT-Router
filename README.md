# REACT-ROUTER
#### For front-end or client side routing.
![image](https://github.com/user-attachments/assets/35ed8189-c85e-4486-add6-e48e3b5903c0)


#### First, Understanding URL's
- URL is a request for desired resources explained in their components </br>

#### THE URL COMPONENTS
1. The protocol used to get resources (eg. HTTP, HTTPS, mailto, etc).
2. The domain (eg. infotoggle.com), the website with the resources.
3. The path (eg. /docs/guides), the page displayed to the user.
4. The query string (eg. ?search=node), after a ‘?’ are parameter values to search or filter.
#### REACT APPLICATIONS use REACT ROUTER for ROUTING.</br>

## What is Routing?
- APP'S display different PAGES or different URL'S/components by Routing.</br>

## PROVIDE A ROUTER / SET ROUTER UP 
##### App's views are called Routes or React components, They are rendered.</br>
- The Router determines which routes to render at differen URL's</br> 
##### Install react-router-dom </br>
      `npm install --save react-router-dom@6`
      
    import { RouterProvider, createBrowserRouter } from 'react-router-dom';
    const router = createBrowserRouter(      (1) THIS DEFINES A ROUTER
                /*APP's ROUTES DEFINED HERE */      );

    export default function App () {
      return (   (2) THIS MAKES ROUTER AVAILABLE TO APP
         <RouterProvider router={ router } /> 
      );                  (3) PATHS ARE PASSED AS PROPS
    }

## ROUTING WITH `<Route>` / DEFINE THE ROUTERS TO RENDER
###### *Routes are views, URL paths, or components*
###### *React Router's defines routes as either: JSX or objects.*</br>

To initialize Router </br>
###### *Convert from `route Element --> route object --> router Initialized`*</br>
1st `.createRoutesFromElements(JSX route element)` --> route objects </br>
      - <Route> objects defines how the App responds to different URL's.</br>
2nd `.createBrowserRouter(route object)`--> router objectS.</br>
3rd <RouteProvider route={Router} /> ROUTER is passed to Route Provider</br>

<Route path='/about' element={ <About/> } Component's:
###### 1. A URL path = THIS PATH CAUSES THIS ROUTE TO RENDER
###### 2. An Element prop = THE COMPONENT RENDERED FOR THIS PATH
`.createRoutesFromElements` - renders component when URL path matched
- ABOVE: render <About> component when URL matches `/about`

       import About from './About.js';
       import { RouterProvider, createBrowserRouter, createRoutesFromElements, Route } from `react-router-dom`

       const router = createBrowserRouter(createRoutesFromElements(
              <Route path='/about' element={ <About/> } />
       ));

##### FOR COMPONENTS THAT NEED TO BE RENDERED ON EACH PAGE VIEW LIKE A NAV BAR

      const router = createBrowserRouter(createRoutesFromElements(
        <Route path='/' element={ <Root/> }>  (1) CREATE ROOT LEVEL COMPONENT
                            // (2) NESTED ROUTES HERE BEFORE CLOSING TAG
        </Route>
      ));
##### When Navigating to one of the nested routes
      WHAT IS RENDERED? ---> the nested route and <Root />'s components

#### Ex. Define Routes: Use createBrowserRouter, createRoutesFromELements and Root's <Route>

      const router = createBrowserRouter(createRoutesFromElements(
        <Route path="/" element={ <Root/> }>  {/* Root's route */}
          <Route path="mypath" element={ <MyComponent/> } />  {/* nested route */}
          <Route path="myotherpath" element={ <MyOtherComponent/> } />
              `/` ablsolute path - means it navigates from the root directory.
        </Route>
      ));

## LINKING TO ROUTES 
#### Navigating between pages of an app causes pages to reload. </br>
React Router has 2 anchors to prevent reloading</br>
THEIR SYNTAX: They have a `to` prop (for redirect) and `wrapped HTML` 

     import {Link, NavLink } from 'react-router-dom';
     1. <Link to="/path">About</Link> (to = href)
     2. <NavLink to="/path">About</NavLink>

#### `NavLink` is Different?
- It gives the link an `.active`class .</br>

##### This helps Styling: </br>
- Allows highlight to the viewed content.</br>
- Functions can be passed to className to customize styling of the NavLink</br>
            *Example
            
                <NavLink 
                  to="about" 
                  className={ ({ isActive }) => isActive? 'nav-link nav-link-active' : 'nav-link'}
                  //Different styling applied when active 'activeNavLink class' or not active
                > About </NavLink>

## DYNAMIC ROUTES
###### * `Static Route paths` match a single path `/about`* </br>
###### * `Dynamic Route paths` match a pattern `/about/:someTitle   = `/:URLParameter`` * </br>

      const route = createBrowserRouter(createRoutesFromElement(
        <Route path='/articles/:titlePlaceholder' element={ <Article /> }/>
      ))                    FROM ABOVE PATH THE URL PARAMETER IS = :titlePlaceholder`
- So The `<Article>` component is RENDERED FOR ALL PAGES SIMILAR TO:</br>
            - `/articles/react, or /articles/html-or-css or /articles/anythingelse` <br>


## `useParams()` HOOK
#### To Render Dynamic routes requires the URL Parametes
#### REACT HOOKS RETURN --> 1. AN OBJECT AND 2. AN A SETTER FUNCTION </br>
- `useParams()` --> gives access to URL parameter values as an object of names: value pairs</br>

      --> Visiting /articles/objects renders Article
      import { Link, useParams } from 'react-router-dom';

      export default function Article() {
        let { title } = useParams();      // Destructure returned object 
         // to access the URL parameters value and store in title
        return (
            <h1>{title}</h1>   //when Article is rendered title's value displayed
       );
      }
## NESTED ROUTES
Are route (Children) relative with a route (Parent).

      const router = createBrowserRouter(createRoutesFromElement(
        <Route path='/about' element={ <About/> }> ** WHEN PATH matches /about THEN `<About>` Rendered
              <Route path='secret' element={ <Secret/> }>  />  
                 **about is exclude from this path b/c it's relative to parent
                 **If path matches /about/secret `<Secret >` and `<About >` Rendered
        </Route> 
      ));

## `<Navigate>` COMPONENT (or Redirect)
- When <Navigate> is rendered it redirects to the location of `to` prop.</br>
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

## `useNavigate()` HOOK
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

## QUERY PARAMETERS
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
      
2. CREATE ROUTES</br>
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

3. CREATE NESTED/INDEX ROUTES   </br>
   The Root Route '/' contains content which is always displayed across different subpages.
   Nested Route uses its parents' (or root route) path to render
   
           const router = createBrowserRouter(createRoutesFromElements(
              <Route path='/' element={ <Root/> }>       /* root route or parent */
                // nested routes here will render along with this <Root/> component
                     eg. <Route path="mypath" element={ <MyComponent/> } />  /* nested route */
              </Route>
            ));
   
4. RENDER NESTED ROUTE</br>
   Once Nested routes are created we must render them</br>
   To render nested routes the parent element is told where to render the nested element</br>
   FIRST, import { Outlet } from 'react-router-dom'</br>
   SECOND, Use Outlet to indicate where in the parent component we want the child component rendered.</br>
   
               <Route path='/' element={ <Parent/> }>    //In Parent component use <Outline/>  
                     <Route path="childPathName" element={ <Child/> } /> 
               </Route>
       
         
5. URL PARAMETERS IN REACT COMPONENTS</br>
   To add URL parameters to a Route path use a colon `:` --> :A_Dynamic_Path</br>
   
         <Route path='/' element={ <MyComponent/> }>
              <Route path=':myType' element={ <MyTypedComponent /> }/>
                     {/* Nested Route renders paths matching `/type1` or `/type2` */}
         </Route>
   
   To get the value of a URL parameter `:param` call useParam() ==> returns object and Destructure object </br>
         `const { param } = useParams()`</br>
   A Route with multiple URL parameters</br>
         `<Route path='/path/:foo/:bar' element={ <SomeComponent /> } />`</br>
   The useParams() returns object on the Dynamic Route and then destructuring the object:</br>
         `const { foo, bar } = useParams()`</br>
         
6.REACT ROUTER FEATURES ON A SEARCH BARS</br>
   ***NOTE: QUERY PARAMETERS ARE FOUND AFTER QUESTION MARK IN URL</br>
   ***For the URL --> `.../search?name=fido`   The QUERY PARAMETER --> `?name=fido`</br>
   First, User inputs a query in the search bar. </br>
   Second, that search query or parameter upadates the URL </br>
   Third, User is THEN redirected to pages of for that query</br>
   `To update the URL WITH THE USERS QUERY ---> USE THE useNAVIGATION() HOOK`</br>
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
   #### 4TH: After users input on searchbar --> COMPONENT RENDERED --> REDIRECTION TO PATH</BR>
          --> `.../search?keyName=searchValue`</br>
         NOTE* query parameter is not part of path</br>

         Add a component or nested route to Root Route which renders when path matches `/search`
         <Route path='/search' element={ <SearchComponent/> } />

      To render the matching user search query get the search parameter value from ?keyName=searchPValue</br>
         call useSearchParams() hook and destructure searchParam property it returns</br>

         const [ searchParamPropertyValue ] = useSearchParams()

   #### FINALLY, RETRIEVE THE 'name' QUERY PARAMETER WITH searchParams get method and replace the value of petNameToFind with it.</br>
  
         const searchParamValue = searchParams.get('nameOfProperty')

7. To REDIRECT a user use REACT ROUTER'S Navigate COMPONENT or useNavigate() hook</br>
      A.    return (
               <Navigate to='/' /> declarative
               )
      B.   const navigate = useNavigate(); imperative</br>

---------------------------------------------------------------------------------------------------------------------------------
