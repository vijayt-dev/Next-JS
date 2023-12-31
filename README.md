# Next JS

## Intro

In official React Documentation, suggest never to use plain React, Instead it recommends to build new apps by picking one of the react frameworks.

They recommend the first framework that they recommend is:

The compaines shift towards using next JS such as Netflix, Tik Tok, Twitch, Hulu, Notion etc..


## What is Next JS?

- Next.js is a framework for building web applications.
- In Next.js, you can build user interfaces using React components. Then, Next.js provides additional structure, features, and optimizations for your application.


## What does Next.js have that React doesn't?

- Next.js simplifies the development process.
- On top of that it optimized your web apps.
- Next.js is an extension of React.
- That streamlines the development process by automating several functions.
- Allowing developers to focus on twhat they do best.


## Benefits of Next JS

### Rendering

It all begins with the rendering process

- The react JS renders user interface on the client side while next JS performs server-side rendering.
- Next JS offers flexibility in rendering options you can choose to render the UI on the client side or the server side according to your needs.

#### Client-side rendering

It happens on the client's device or the browser when a user requests a web page the server sends a basic HTML document and JavaScript code the browser then downloads and executes the JavaScript code


#### Server-side rendering

- Rendering the web page on the server. Before transmitting it to the client's device.
 
- When a user request the page the server processes the request and renders the components on the server side the  server then sends back the fully rendered HTML to the client's browser enabling immediate display
 
### SEO

- SEO crawlers face difficulties indexing pages dynamically rendered on the client side as a result the SEO performance of such pages may suffer.

- Search engines may not fully comprehend their content and rank them appropriately.

- This issue is resolved by sending pre-redered code directly to the client. This enables:
	- Easy crawling
	- Indexing 

#### Why should I prioritize SEO?

SEO is crucial for optimizing a website's visibility and ranking in search engine results

#### Benefits of SEO

- Increased organic traffic
- Enhanced user experience
- Credibility & trustworthiness
- Competitive advantage

### Routing

- Next.js uses file-based routing system.
- The routing is handled by the file system.
- Each folder in the /app directory becomes a route and the folder name becomes theroutes path.
- Ex: http://localhost:3000/about
- No need for external packages or complex configurations

### API Routes

- Enabling the creation of serverless functions to handles API requests.
- Serverless APIs in Next.js are a way of creating API endpoints without the need for a traditional server.
- It allows us to build and deploy APIs
	- Without managing server infrastructure.
	- Worrying about scaling their server as traffic increases
- You can create an API endpoint by simply creating a file called route.js in a specific folder within the app directory


### Automatic Code Splitting

- Code splitting is a technique that breaks down large bundles of JavaScript code into smaller, more manageable chunks that can be loaded as needed.
- This reduces the initial load time of a website and optimizes the user's experience while browsing.
- It uses automatic code splitting by default to split pages into separate chunks.

### It's still just React

- Next.js is not an entirely new technology.
- It is still fundamentally built on top of React.
- Allowing developers to concentrate on the core React code.
- Moving from a typical react, express, webpack to next JS resulted in removing 20, 000+ lines of code and 30+ dependencies while improving hard module reloading from 1.3 seconds to 131ms which is 10x less.

## Create project, run:

```bash
npx create-next-app@latest
```

```bash
npx create-next-app@latest ./
```

This will ensure to create your next application within the current repository.

Import aliases are shortcuts that allow you to refer to a module or a file using a custom name instead of its full path.

## Server & Client Components

There are two environments where your application code can be rendered the client and the server.

In Next JS within the app folder are react server components which means that next js leverages server-side rendering to enhance the initial page loading speed resulting in improved SEO.

A client-side one you need to add the use client directive to the top of your page to turn into a client side component

## Data Fetching

1. Server Side Rendering (SSR)
2. Static Site Generation (SSG)
3. Incremental Static Generation (ISR)

### Server Side Rendering (SSR)

It means Dynamic server rendered data it is fetched fresh on each request with SSR each request to the server triggers a new rendering cycle and data fetch ensuring that the content is always up to date here.

```js
async function Page({params}) {
	const res = await fetch(`https://jsonplaceholder.typicode.com/users/${params.id}`, {cache: 'no-store'});
	const data = await res.json();
	
}
```

### Static Site Generation (SSG)

By default next js uses SSG  it will fetch data but it will also cache it this method is ideal for content that doesn't change frequently such as blog posts documentation.


```js
async function Page({params}) {
	const res = await fetch(`https://jsonplaceholder.typicode.com/users/${params.id}`);
	const data = await res.json();
	
}
```

### Incremental Static Generation (ISR)

It can have specify certain data to be statically fetched at build time 
while defining a revalidation time interval this means that the datat will be cached but after a specific time frame it's then going to refresh it and get new data.

```js
async function Page({params}) {
	const res = await fetch(`https://jsonplaceholder.typicode.com/users/${params.id}`, {next: { revalidate: 10 }});
	const data = await res.json();
	
}
```

 

## HTTP Methods

Next.js supports the following HTTP methods:

1. **GET**: Retrieves datat or resources from the server.
2. **POST**: Submits data to the server to create a new resource.
3. **PUT**: Updates or replaces an existing resource on the server.
4. **PATCH**: Partially updates an exisiting resource on the server.
5. **DELETE**: Removes a specific resource from the server.
6. **HEAD**: Retrieves the headers of a resource without fetching its body.
7. **OPTIONS**: Retrieves the supported HTTP methods and other communication options for a resource.

## Metadata

We can define Metadata in two ways: 
1. Static Metadata
2. Dynamic Metadata

### Static Metadata

```js
export const metadata = {
	title: "Promptopia",
	description: "Discover & Share AI Prompts"
}
```

### Dynamic Metadata

```js
export async function generateMetadata({params, searchParams}) {
	const product = await getProduct(params.id);
	return { title: product.title }
}
```

##  "use client" directive

"use-client" is a convention to use a Client Component, create a file inside app and add the "use client" directive at the top of the file (before any imports). By default, all components on NextJS 13 inside the App folder are server components.

## Session Provider

```js
"use client";

import { SessionProvider } from "next-auth/react";

const Provider = ({ children }) => {
  return <SessionProvider>{children}</SessionProvider>;
};

export default Provider;

```

- The SessionProvider component is used to wrap your Next.js application.
- It to enable session management and authentication functionality provided by NextAuth.js
-  It sets up a context for storing and accessing session data throughout your application.
- It  access to the session object and its properties, such as session.user to access the currently authenticated user's information. It also provides hooks and utilities for handling authentication-related operations, such as logging in, logging out, and accessing session data in your components.

## Client API


### useSession()

It allows you to access the session information for the currently authenticated user. The session object usually contains user data, such as the user's name, email, and authentication status.

```js
  const { data: session, status } = useSession()
```

useSession() returns an object containing two values: data and status:


### signIn() 

It is used to initiate the sign-in process. It typically triggers authentication with the selected authentication provider.

By default, when calling the signIn() method with no arguments, you will be redirected to the NextAuth.js sign-in page. If you want to skip that and get redirected to your provider's page immediately, call the signIn() method with the provider's id.

For example to sign in with Google:

```js
import { signIn } from "next-auth/react"
export default () => <button onClick={() => signIn('google')}>Sign in</button>
```

### signOut() 

It is used to sign out the currently authenticated user. It terminates the user's session and clears any associated tokens or cookies.

It reloads the page in the browser when complete.

```js
import { signOut } from "next-auth/react"
export default () => <button onClick={() => signOut()}>Sign out</button>
```

### getProviders() 

It is used to retrieve a list of available authentication providers configured in NextAuth.js. It returns an array of provider objects, each representing a different authentication provider (e.g., Google, Facebook, etc.).

It calls /api/auth/providers and returns a list of the currently configured authentication providers.

```js
import { getProviders } from "next-auth/react"

export default async () => {
  const providers = await getProviders()
  console.log("Providers", providers)
}
```

## Add API route

To add NextAuth.js to a project create a folder called [...nextauth] inside create route.js file in pages/api/auth. This contains the dynamic route handler for NextAuth.js which will also contain all of your global NextAuth.js configurations.

```js
import NextAuth from "next-auth"
import GithubProvider from "next-auth/providers/github"

export const authOptions = {
  // Configure one or more authentication providers
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    // ...add more providers here
  ],
}

export default NextAuth(authOptions)
```

- All requests to /api/auth/ (signIn, callback, signOut, etc.) will automatically be handled by NextAuth.js.
- The only authentication provider included is GoogleProvider. It is configured with a clientId and clientSecret obtained from environment variables (process.env.GOOGLE_ID and process.env.GOOGLE_CLIENT_SECRET respectively).
- These environment variables likely store the Google OAuth credentials required for authentication.


## Next API Functions

### usePathname

usePathname is a Client Component hook that lets you read the current URL's pathname.

```js
'use client'
 
import { usePathname } from 'next/navigation'
 
export default function ExampleClientComponent() {
  const pathname = usePathname()
  return <p>Current pathname: {pathname}</p>
}
```

### useRouter

The useRouter hook allows you to programmatically change routes inside Client Components.

```js
'use client'
 
import { useRouter } from 'next/navigation'
 
export default function Page() {
  const router = useRouter()
 
  return (
    <button type="button" onClick={() => router.push('/dashboard')}>
      Dashboard
    </button>
  )
}
```

router.push(href: string): Perform a client-side navigation to the provided route.

### useSearchParams

useSearchParams is a Client Component hook that lets you read the current URL's query string.

```js
'use client'
 
import { useSearchParams } from 'next/navigation'
 
export default function SearchBar() {
  const searchParams = useSearchParams()
 
  const search = searchParams.get('search')
 
  // URL -> `/dashboard?search=my-project`
  // `search` -> 'my-project'
  return <>Search: {search}</>
}
```

## MongoDB Database Connection

```js
import mongoose from "mongoose";

let isConnected = false; // track the connection

export const connectToDB = async () => {
  mongoose.set("strictQuery", true);

  if (isConnected) {
    console.log("MongoDB is already connected");
    return;
  }

  try {
    await mongoose.connect(process.env.MONGODB_URI, {
      dbName: "share_prompt",
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });

    isConnected = true;

    console.log("MongoDB connected");
  } catch (error) {
    console.log(error);
  }
};
```

- mongoose.set('strictQuery', true): 
The 'strictQuery' option is a Mongoose-specific option that enforces strict behavior when executing queries. When set to true, Mongoose will throw an error if you attempt to execute a query using undefined or unrecognized query methods. This helps catch potential errors in your code where you might mistakenly use a non-existent query method.
- mongoose.connect(process.env.MONGODB_URI, {
      dbName: "share_prompt",
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });:  
The mongoose.connect() method is called with the MongoDB connection URI and an options object. The useNewUrlParser and useUnifiedTopology options are set to true within the options object to enable the new connection string parser and the new Server Discovery and Monitoring engine, respectively.
By configuring these options appropriately, you ensure that Mongoose utilizes the latest MongoDB driver features and avoids any deprecation warnings or compatibility issues.


## Schemas

```js
import { Schema, model, models } from 'mongoose';

const UserSchema = new Schema({
  email: {
    type: String,
    unique: [true, 'Email already exists!'],
    required: [true, 'Email is required!'],
  },
  username: {
    type: String,
    required: [true, 'Username is required!'],
   // match: [/^(?=.{8,20}$)(?![_.])(?!.*[_.]{2})[a-zA-Z0-9._]+(?<![_.])$/, "Username invalid, it should contain 8-20 alphanumeric letters and be unique!"]
  },
  image: {
    type: String,
  }
});

const User = models.User || model("User", UserSchema);

export default User;
```

- **Schema** is a class provided by Mongoose that helps define the structure of the documents stored in a MongoDB collection.
- Each field in the schema is defined using an object that specifies the field's type and any additional validation rules. For example, the email field is of type String, must be unique (unique: true), and is required (required: true). If a validation rule is not met, an error message will be provided.
- **model** is a function provided by Mongoose that is used to create a model based on a schema. It represents a collection in the MongoDB database and provides an interface for querying and manipulating the documents.
- **models** is an object provided by Mongoose that stores all the registered models. It allows you to check if a model has already been defined to avoid redefining it.
- The User constant is assigned the value of models.User if it exists or a new model is created using model("User", UserSchema). This ensures that if the User model has already been defined, it is reused, preventing duplicate model definitions.


## Mongoose API Functions

### find

The find method is used to query a MongoDB collection and retrieve documents that match.

The find method allows you to specify a query object that defines the conditions to match against the documents in the collection. It returns a Query object that can be further customized or executed.

```js
const Person = mongoose.model('Person', { name: String, age: Number });

// Find all documents where age is greater than or equal to 18
const adults = await Person.find({ age: { $gte: 18 } });

// Find all documents where the name starts with "John"
const johns = await Person.find({ name: /^John/ });
```

### populate

The populate method is used to populate referenced documents in a MongoDB collection. It allows you to retrieve and replace references to other documents with the actual referenced documents.

```js
const User = mongoose.model('User', { name: String, posts: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Post' }] });
const Post = mongoose.model('Post', { title: String, content: String });

// Find a user and populate the 'posts' field with actual Post documents
const user = await User.findOne({ name: 'John' }).populate('posts');

console.log(user);
```

### save

The save method is used to save or update a document in a MongoDB collection.

```js
const User = mongoose.model('User', { name: String, age: Number });

// Create a new user document
const user = new User({ name: 'John', age: 25 });

// Save the user document to the database
await user.save();
```

If the user document is new and doesn't exist in the database, calling save will insert a new document. If the user document already exists and has been modified, calling save will update the existing document with the new values.

**Update Document**

```js
// Find a user document
const user = await User.findOne({ name: 'John' });

// Update the user's age
user.age = 26;

// Save the updated user document
await user.save();
```

### findById

The findById method is used to find a document in a MongoDB collection by its unique _id field. It allows you to search for a document based on its identifier and retrieve it from the collection.

```js
const User = mongoose.model('User', { name: String, age: Number });
// Find a user by its _id
const user = await User.findById('60c42f6ee32d7f1a9c1ab2b5');

```

### findByIdAndRemove

The findByIdAndRemove method is used to find a document by its unique _id field and remove it from the MongoDB collection. It allows you to delete a document based on its identifier.

Tthe removed document is returned as the result. If no matching document is found, the result is null.

```js
const User = mongoose.model('User', { name: String, age: Number });

// Find a user by its _id and remove it
const removedUser = await User.findByIdAndRemove('60c42f6ee32d7f1a9c1ab2b5');
```

### findOne

Tthe findOne method is used to query a MongoDB collection and retrieve a single document that matches the specified criteria. It allows you to find the first document that satisfies the query conditions.

If a matching document is found, it is returned as the result. If no matching document is found, the result is null.

```js
const User = mongoose.model('User', { name: String, age: Number });

// Find a user document
const user = await User.findOne({ name: 'John' });
```

# Routing

### Creating Routes

Next.js has a file-based routing system in which each page automatically becomes a route based on its file name.
**Folders**: It is used to define routes that includes page.js.
**Files**: Files are used to create UI.

For example, to create your first page, add a page.js file inside the app directory and export a React component:

```js
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```

### Nested Routes

To create a nested route, you can nest folders inside each other. For example, you can add a new` /dashboard/settings` route by nesting two new folders in the app directory.

The /dashboard/settings route is composed of three segments:

- / (Root segment)
- dashboard (Segment)
- settings (Leaf segment)

### Colocation

- You can specify our own files (eg: component, styles) inside folder in the app directory.
- .js, .jsx, or .tsx file extensions can be used for special files.
- Only the page.js or route.js are publically addressable.
	- components/button.jsx
	- lib/constant.js

### Pages

- A page is a user interface (UI) specific to a route. To create a page, export a component from a page.js file. Use nested folders to define a route, and include a page.js file to make the route accessible to the public.
- .js, .jsx, or .tsx file extensions can be used for Pages.
- Pages are Server Components by default but can be set to a Client Component.
- Pages can fetch data. 
- Create your first page by adding a page.js file inside the app directory:

```js
// `app/page.js` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>
}
```

### Layouts

A layout is a user interface (UI) that is used on multiple pages. When you move between pages, layouts keep their current state, stay interactive, and don't reload. Layouts can also be nested.

To create a layout, you can export a React component from a file called layout.js as the default export. The component should have a "children" prop that will be filled with either a child layout (if there is one) or a child page when it's being rendered.

**Example**
```js
// app/dashboard/layout.js
export default function DashboardLayout({
  children, // will be a page or nested layout
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>
 
      {children}
    </section>
  )
}
```

- The main layout at the very top is known as the Root Layout. It is used on all pages of an application. Root layouts should have html and body tags.
- Each part of a route can choose to have its own layout. These layouts will be used for all pages in that part.
- Layouts are Server Components by default but can be set to a Client Component.
- Layouts can fetch data.
- Layouts do not have access to the current route segment(s). To access route segments, you can use useSelectedLayoutSegment or useSelectedLayoutSegments in a Client Component.
- .js, .jsx, or .tsx file extensions can be used for Layouts.
- A layout.js and page.js file can be defined in the same folder. The layout will wrap the page.

### Root Layout

The root layout is defined at the top level of the app directory and applies to all routes.

**Example**

```js
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

- The app directory must include a root layout.
- The root layout must define `<html>` and `<body>` tags since Next.js does not automatically create them.
- The root layout is a Server Component by default and can not be set to a Client Component.
- Only the root layout can contain `<html>` and `<body>` tags

### Metadata

Metadata can be defined by exporting a metadata object or generateMetadata function in a layout.js or page.js file.

**Example**

```js
export const metadata = {
  title: 'Next.js',
}
 
export default function Page() {
  return '...'
}
```

- Don't manually include `<head> ` tags like `<title>` and `<meta>` in the main layouts. Instead, use the Metadata API that takes care of advanced tasks like managing streaming and eliminating duplicate `<head>` elements.

### Linking and Navigating

The Next.js router uses a combination of server-based and client-based navigation. It allows for quick loading and rendering, and ensures that the client's current state is maintained during navigation. This approach avoids unnecessary re-rendering, allows for interruptions, and prevents conflicts between different actions.

There are two ways to navigate between routes:

- `<Link>` Component
- useRouter Hook

### `<Link>` Component

The component called `<Link>` in React is an extension of the HTML `<a>` element. It allows for prefetching and navigation between routes on the client side. In Next.js, it is the main method used for moving between different routes.

To use `<Link>`, import it from next/link, and pass a href prop to the component:

### Linking to Dynamic Segments

When linking to dynamic segments, you can use template literals and interpolation to generate a list of links. 

**Example**

### Checking Active Links

You can use usePathname() to determine if a link is active. For example, to add a class to the active link, you can check if the current pathname matches the href of the link:

```js
'use client'
 
import { usePathname } from 'next/navigation'
import { Link } from 'next/link'
 
export function Navigation({ navLinks }) {
  const pathname = usePathname()
 
  return (
    <>
      {navLinks.map((link) => {
        const isActive = pathname.startsWith(link.href)
 
        return (
          <Link
            className={isActive ? 'text-blue' : 'text-black'}
            href={link.href}
            key={link.name}
          >
            {link.name}
          </Link>
        )
      })}
    </>
  )
}
```

### Scrolling to an id

The default behavior of `<Link>` is to scroll to the top of the route segment that has changed. When there is an id defined in href, it will scroll to the specific id, similarly to a normal `<a>` tag.

To prevent scrolling to the top of the route segment, set scroll={false} and add a hashed id to href:

```js

<Link href="/#hashid" scroll={false}>
  Scroll to specific id.
</Link>

```

### useRouter() Hook

The useRouter hook allows you to programmatically change routes inside Client Components.

To use useRouter, import it from next/navigation, and call the hook inside your Client Component:

```js

'use client'
 
import { useRouter } from 'next/navigation'
 
export default function Page() {
  const router = useRouter()
 
  return (
    <button type="button" onClick={() => router.push('/dashboard')}>
      Dashboard
    </button>
  )
}

```

- Use the `<Link>` component to navigate between routes unless you have a specific requirement for using useRouter.


### Route Groups

A folder can be wrapped in parentheses (folderName) to create route groups.

The purpose of having the folder is purely organizational and it should not be included in the URL path of the route.


### Dynamic Routes

Dynamic routes  allow you to create dynamic pages without having to define each route explicitly. **Example** app/post/[slug]
Dynamic route can be created by wrapping a folder name in square brackets.
Dynamic routes give params props can be accessed by layout, page, route, and generateMetadata functions.

**Example**

```js
// app/post/[slug]/page.js	
export function Post({params}) {
  return (
    <div>
      <h1>Post: {params.id}</h1>
    </div>
  );
}

```

#### Catch-all Segments

The catch-all segment is used to match URLs with any number of segments.
**Example** app/shop/[...slug]/page.js

#### Optional Catch-all Segments

Catch-all Segments can be optional by adding the parameter in double square brackets: **Example**  app/shop/[[...folderName]]/page.js.

In optional catch-all routes the route without the parameter will also get match.

### Loading UI and Streaming

loading.js helps to create loading UI wth the help of React Suspense.
You can show loading state from the server while the route segment loads once rendering is completed the new content added.

#### Streaming with Suspense

##### What is Streaming?

Before going to streaming understand SSR  and its limitation

With SSR, list of steps that need to completed before user can see and interact the page.
- First all data for a given page is fetched on the server.
- Then server reder the HTML page.
- The HTML, CSS, and JavaScript for the page are sent to the client.
- A non-interactive user interface is shown using the generated HTML, and CSS.
- Finally, React hydrates the user interface to make it interactive.

The server can render the HTML for a page only after all the data has been fetched because the steps are sequential and blocking. Similarly, on the client side, React can only hydrate the UI once the code for all components in the page has been downloaded.

However, the page display to the user may be delayed since all server data fetching must be completed prior to rendering.

Streaming enables the fragmentation of a page's HTML into smaller portions and gradually transmits these portions from the server to the client.

Streaming enables each component to be treated as a separate unit, known as a chunk. This allows for the prioritization of components that are more important or independent of data, enabling React to begin hydration earlier. Components with lower priority can be sent in the same server request once their data has been retrieved.

Streaming becomes especially advantageous when you aim to avoid the page from being blocked during rendering due to lengthy data requests.

**Example**

`<Suspense>` works by wrapping a component that performs an asynchronous action (e.g. fetch data), showing fallback UI (e.g. skeleton, spinner) while it's happening, and then swapping in your component once the action completes.

```js
import React, { Suspense } from 'react'
import Loading from './loading'

export default function Dashboard() {
    return (
    <Suspense fallback={<Loading />}>
    <h1>Hello, Dashboard Page!</h1>
    </Suspense>
    )
  }

```

Utilizing Suspense provides the advantages of:

- Streaming Server Rendering: Enabling the gradual rendering of HTML from the server to the client.
- Selective Hydration: Allowing React to prioritize the interactivity of components based on user interaction.


### Error Handling

The usage of the error.js file convention enables you to handle runtime errors in nested routes.
Maintain the functionality of the rest of the app while isolating errors to the relevant segments.
Enhance the capability to recover from an error without requiring a complete page reload.

**Example**

```js

//app/dashboard/error.js
'use client'
 
export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  )
}

```

#### How error.js Works

- The file error.js creates a React Error Boundary that wraps a nested child segment or page.js component automatically.
- The exported React component from error.js serves as the fallback component.
- If an error occurs within the error boundary, it is captured and the fallback component is rendered.
- While the fallback error component is active, layouts above the error boundary retain their state and interactivity, and the error component can provide functionality to recover from the error.

#### Recovering From Errors

If an error is temporary, attempting to resolve the issue by retrying might be effective. In the context of an error component, the reset() function can be utilized to prompt the user to recover from the error. By executing this function, the Error boundary's contents are re-rendered in an attempt to replace the fallback error component with the outcome of the re-render.

### Parallel Routes

Parallel Routing enables the simultaneous or conditional rendering of multiple pages within the same layout.

As each route is streamed in independently, Parallel Routing enables you to define separate error and loading states for each route.

With Parallel Routing, you have the ability to conditionally display a slot depending on specific conditions, such as the authentication state. This feature enables the use of completely separate code on the same URL.

#### Convention

Named slots are utilized to create parallel routes. These slots are defined using the "@folder" convention and passed as props to the layout at the same level.

The URL structure remains unaffected by slots, as they are not considered route segments. Therefore, the file path /@team/members can be accessed at /members.

For example, the following file structure defines two explicit slots: @analytics and @team.

With the given folder structure, the app/layout.js component now receives the @analytics and @team slots props and can render them simultaneously with the children prop.

```js
export default function Layout(props) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  )
}
```

#### Unmatched Routes

The content displayed in a slot will automatically correspond to the current URL by default.

In the case of an unmatched slot, If Next.js is unable to determine the active state of a slot based on the current URL, you can specify a default.js file to be rendered as a fallback.

```js
// app/@authModal/login/default.js
export default function Default() {
  return null
}
```

#### Conditional Routes

Parallel Routes can be used to implement conditional routing. For example, you can render a @dashboard or @login route depending on the authentication state.

**Example: **

```js
import { getUser } from '@/lib/auth'
 
export default function Layout({ params, profile, login }) {
  const isLoggedIn = getUser()
  return isLoggedIn ? profile : login
}

```

### Intercepting Routes

The ability to intercept routes enables you to load a route within the existing layout without losing the context of the current page. This routing approach proves beneficial when you need to "intercept" a specific route and display an alternative route instead.

It intercepts the /feed route and masks it by displaying /photo/123 instead when a photo is clicked within the feed, resulting in a modal overlaying the feed showing the photo.

#### Convention

The (..) convention, similar to the relative path convention ../, can be used to define intercepting routes for segments.

You can use:

- (.) to match segments on the same level
- (..) to match segments one level above
- (..)(..) to match segments two levels above
- (...) to match segments from the root app directory


## Data Fetching

The App Router is a simplified way to fetch data in your Next.js application.
You can fetch data inside layouts, pages, and components. Data fetching is also compatible with Streaming and Suspense.

- Fetch data on the server using Server Components: Server Components are a great way to fetch data on the server. This can improve performance, as the data will be pre-rendered and cached on the server.
- Fetch data in parallel to minimize waterfalls and reduce loading times.
- Next.js will automatically cache and  dedupe requests in a tree. This means that if you fetch the same data in multiple times, Next.js will only fetch the data once.

### Static Data Fetching

It fetch data at build time and cache it for improved loading performance. This means that the data will be fetched once and stored in memory, so it can be quickly retrieved when a user visits a page.

**Example**

```js
import Image from "next/image";
async function getImage() {
  const image = await fetch("https://dog.ceo/api/breeds/image/random");
  const data = await image.json();
  return data;
}
const Static = async () => {
  const {message} = await getImage();
  return (
    <div className="flex min-h-screen flex-col items-center justify-between p-24">
      <h2>Static Image</h2>
      <div>
        <Image src={message} width={500} height={500} />
      </div>
    </div>
  );
};

export default Static;

```

### Static with Revalidating Data Fetching

It will periodically check the data to be updated. If it has, Next.js will fetch the updated data and re-render the page.

**Example**

```js
import Image from "next/image";

async function getImagesStatic2() {
  const image = await fetch("https://dog.ceo/api/breeds/image/random", {
    next: { revalidate: 10 },
  });
  const data = await image.json();
  return data;
}

const Static2 = async () => {
  const {message} = await getImagesStatic2();
  return (
    <div className="flex min-h-screen flex-col items-center justify-between p-24">
      <h2>Static2 Image</h2>
      <div>
        <Image src={message} width={500} height={500} />
      </div>
    </div>
  );
};

export default Static2;

```

### Dynamic Data Fetching

It allows you to fetch data from at request time, rather than at build time. This can be useful for applications that need to display data that is constantly changing.

**Example**

```js

import Image from "next/image";

export async function getImagesDynamic() {
  const image = await fetch("https://dog.ceo/api/breeds/image/random", {cache: "no-cache"});
  const data = await image.json();
  return data;
}

const Dynamic = async () => {
  const { message } = await getImagesDynamic();

  return (
    <div className="flex min-h-screen flex-col items-center justify-between p-24">
      <h2>Dynamic Image</h2>
      <div>
        <Image src={message} width={500} height={500} />
      </div>
    </div>
  );
};

export default Dynamic;


```

### Parallel Data Fetching

It allows you to fetch data from multiple sources in parallel, rather than sequentially. This can improve the performance of your application by reducing the amount of time it takes to load data.

#### Streaming and Suspense

Streaming allows you to progressively render your application's UI from the server to the client, even if some of the data is not yet available. This means that users can start interacting with your application sooner, even if it's not fully loaded.

Suspense is a React feature that allows you to show a fallback UI while an asynchronous operation is pending. This can be used to show a loading spinner while your application fetches data, or to show a placeholder image while your application loads an image from the network.



**Example**

```js
import UserPost from "@/app/components/UserPost";
import getPost from "@/utils/getPost";
import getUser from "@/utils/getUser";
import { Suspense } from "react";

async function getPost(id) {
  const post = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${id}`);
  if (!post.ok) {
    throw new Error("Failed to Fetch Post");
  }
  const data = await post.json();
  return data;
}

async function getUser(id) {
  const user = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
  if (!user.ok) {
    throw new Error("Failed to Fetch User");
  }
  const data = await user.json();
  return data;
}

const UserPost = async ({ posts }) => {
  const postData = await posts;
  console.log(postData);
  return (
    <div>
      <ul>
        {postData.map((post) => {
          return (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.body}</p>
            </li>
          );
        })}
      </ul>
    </div>
  );
};



export const generateMetadata = async ({ params: { id } }) => {
  const { name, email } = await getUser(id);
  return {
    title: name,
  };
};
const User = async ({ params: { id } }) => {
  console.log(id);
  const user = getUser(id);
  const posts = getPost(id);
  const userData = await user;
  return (
    <div className="flex min-h-screen flex-col items-center justify-between p-24">
      <h2>Name: {userData.name}</h2>
      <Suspense fallback={<p>Loading...</p>}>
        <UserPost posts={posts} />
      </Suspense>
    </div>
  );
};

export default User;
```

### Old Methods

Next.js data fetching methods such as getServerSideProps, getStaticProps, and getInitialProps are not supported in the new App Router.

## Route Handlers

It allows developers to create custom request handlers for a given route using the Web Request and Response APIs.

- They can be used to handle any HTTP method, including GET, POST, PUT, PATCH, DELETE, HEAD, and OPTIONS.
- They can be used to access the request object, which contains information about the incoming request, such as the URL, headers, and body.
- They can be used to respond to the request, by sending a response object, which contains the response status code, headers, and body.
- They are only available inside the app directory.
- Route Handlers are defined in a route.js|ts file inside the app directory

### Static Route Handlers

It means that the handler code will be executed at build time, and the result will be embedded in the generated JavaScript bundle. This can be useful for serving static content, such as images, JSON files, or HTML pages.

**Example**

```js
import { getPosts, setPosts } from "@/utils/data";
import { NextResponse } from "next/server";

export const GET = async (req, resp) => {
  try {
    const posts = getPosts();
    return NextResponse.json({ message: "OK", posts }, { status: 200 });
  } catch (error) {
    return NextResponse.json({ message: "ERROR" }, { status: 500 });
  }
};

export const POST = async (req, resp) => {
  try {
    const posts = await req.json();
    setPosts(posts);
    return NextResponse.json({ message: "OK", posts }, { status: 200 });
  } catch (error) {
    return NextResponse.json({ message: "ERROR" }, { status: 500 });
  }
};
```

### Dynamic Route Handlers

When the request happen it evaluated dynamically.

**Example**

```js
import { deletePost, getById, updatePost } from "@/utils/data";
import { NextResponse } from "next/server";

export const GET = async (req, resp) => {
  try {
    const id = req.url.split("blog/")[1];
    const post = getById(id.toString());
    if (!post) {
      return NextResponse.json({ message: "ERROR" }, { status: 404 });
    }
    return NextResponse.json({ message: "OK", post }, { status: 200 });
  } catch (error) {
    return NextResponse.json({ message: "ERROR" }, { status: 500 });
  }
};

export const PUT = async (req) => {
  try {
    const { title } = await req.json();
    const id = req.url.split("blog/")[1];
    updatePost(id, title);
    return NextResponse.json({ message: "OK", post }, { status: 200 });
  } catch (error) {
    return NextResponse.json({ message: "ERROR" }, { status: 500 });
  }
};

export const DELETE = async (req) => {
  try {
    const id = req.url.split("blog/")[1];
    deletePost(id, title);
    return NextResponse.json({ message: "OK", post }, { status: 200 });
  } catch (error) {
    return NextResponse.json({ message: "ERROR" }, { status: 500 });
  }
};

```






