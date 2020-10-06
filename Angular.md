# What is Angular ?
Angular is a structural open-source JavaScript framework used to build dynamic web apps. It lets you use HTMl as a template language and supports various platforms like web, mobile, desktop native. The library provides number of features that make it trivial to implement the requirements of modern applications such as data binding, routing and animations. Technically, we can use Angular for non-trivial applications that involves data. Angular works well for applications that needs to run in multiple environments. 

# Difference between Angular JS and Angular+ versions :
Angular JS follows MVC (Model-View-Controller) architecture which consists of the following parameters :
- Controller : represents how user interactions are handled and binds both the model and the view.
- Views : represents the presentation layer and the actual UI.
- Model : abstract representation of your data.

It synchronizes the data between model and the view. Whatever changes are made in the UI template are automatically propagated to the model and view and vice-versa.

Angular+ on the other hand follows component-based architecture. Every angular application has a root component. Each component has an associated class which handles all the business logic and template represents the view layer. All the components used are primarily composed of TypeScript (TS).

Angular JS use scopes and controllers which are replaced by components and directives in its higher version. 

# How to Install Angular 6 
You can start an Angular 6 app using Angular CLI (Command Line Interface). To install ot, you'll need to install node package manager aka npm.

> ### Angular CLI : It is a list of commands that helps us create and start our project.  

To work with Angular CLI, we need to install it first by using :
> npm install -g @angular/cli  

To create a new project, we can run the following commands in CLI :
> ng new PROJECT_NAME  
> cd PROJECT_NAME   
> ng serve  

Here, _ng serve_ will compile and execute your program showing the desired output of your project in the browser --- 
> http://localhost:4200 

4200 is the default port used by any Angular app whenever a new project is created. 

# Angular 6 Project Structure 
> e2e  
node_modules  
src --> app  
... bunch of files included 

When you view your first Angular project/folder, all the files should look like this.

The main folder is src/app where you'll be spending most of your time, also components and services are stored in this folder only.

In the src folder, index.html and sty;e.css file is already included which specifies the root component : 
``` html
<app-root> 
``` 
./dist/ folder is created whenever you build your project by using the command :
> ng build  

# Angular 6 Module File 
Every file in Angular+ version is saved by .ts extension. It stands for TypeScript which is a superset of JavaScript. TS provides strong type-checking on JavaScript.

``` typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
``` 

Whenever we generate any component and service using CLI, it will automatically update app.module.ts file adding details to @NgModule decorator.  
All Components are added in _declarations_ array, whereas all Services are added in _services_ array.

CLI will take care of most of the parts in Angular project as it will update module.ts file every time a new component or service is generated.

# Angular Components 
In Angular, Components is the basic building block of your Angular App. When we used CLI to generate our project, it created a single component with 4 files :
> app.component.html  
app.component.css  
app.component.spec.ts  
app.component.ts  

- HTML file is associated with the HTML component
- CSS file is associated with the rulesets for that component
- SPEC.TS file for testing purpose
- .TS file where actual business logic is build up

``` typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  title = 'app';
}
``` 
@Component decorator is a property/value pair which defines an important stuffs associated with that component.  
Selector: 'app-root' is a unique identifier.  
templateUrl and styleUrls are used to locate HTML and CSS file associated with that component.   
Now, we have the logic section of the component file where all dependency injections and methods are defined. 

You can generate a new component by using the following command in CLI :
> ng generate component COMPONENT_NAME  or   
ng gc COMPONENT_NAME  

# Angular Templating 
In Angular, template represents the view which end-user can see on their web page. These are written with HTML, CSS and directives used in AngularJS.

Another very important element is router-outlet. It specifies which component should load by default when the app is loaded, and also utilize router-outlet.
``` html
<div id="container">
  <app-root></app-root>

  <div id="content">
    <router-outlet></router-outlet>
  </div>
</div>
``` 
We can also use _routerLink_ in an HTML tag to direct the user to different routes. 

# Angular Routing 
Angular Routes will allow navigation from one view to another whenever user perform application tasks. 
``` typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { UsersComponent } from './users/users.component';
import { DetailsComponent } from './details/details.component';
import { PostsComponent } from './posts/posts.component';

const routes: Routes = [
  {
    path: '',
    component: UsersComponent
  },
  {
    path: 'details/:id',
    component: DetailsComponent
  },
  {
    path: 'posts',
    component: PostsComponent
  },
];
``` 
Whatever components are their in our app, all should be imported and then define them as an object in Routes array. When router navigates to other page, Router performs the following steps as follows :
- it applies browser URL redirect
- it figures out which router state corresponds to the URL
- it runs the guards that are defined in the router state 
- it resolves the required data for the router state 
- it activates the Angular components to display the page
- it manages navigation and repeats the steps above when a new page is requested.

Whenever project is loaded on the default URL : http://localhost:4200, our application bootstraps the AppComponent first. to make any other page to load first, just place AppComponent to the child component and add router-outlet inside the AppComponent.

