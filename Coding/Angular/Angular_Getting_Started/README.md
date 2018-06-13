# Angular Getting Started

A course on Pluralsight

## Introduction

### Intro

> Angular is a JavaScript Framework



Angular has:

- Expressive HTML
- Powerful Data Binding
- Modular By Design
- Built-in Back-End Integration



Why a New Angular? Angular is:

- Build for speed
- Modern
- Simplified API
- Enhances productivity



### Anatomy of an Angular Application

Application = Component + Component + Component

— — — — — — — — — — — — — — — — — — — —

​					Services

Component = Template + Class(Properties & Methods) + Metadata

AKA a component is a `view` + `code` + `information`

Every application has at least one module called the `Root Angular Module`



### Get the Most from This Course

Github starter files: https://github.com/DeborahK/Angular-GettingStarted/tree/master/APM-Start



------



## First Things First

### Selecting a Language

**ECMAScript (ES):** Most browsers support `ES 5` but do not support `ES 2015` so it must be `transpiled`.

**TypeScript:** Superset of Javascript with strong typing that must be transpiled.

> Strong typing means that evertying has a datatype.
>
> Strongly typed definitions are kept in `*.d.ts` files.

Build, test, and deply Angular apps using https://github.com/angular/angular-cli



### Modules

Angular leverages ES 2015 code modules. "A file is a module and a module is a file". Just create a file and it becomes a module.

#### Export

```ts
export class Product {} // note: this ts is compiled to a js file
```

#### Import

```ts
import { Product } from './product'
```



------



## Introduction to Components

### What is a Component?

Component = **Template** + **Class** + **Metadata**

**Template:**

- View layout
- Created with HTML
- Includes binding and directives

**Class:**

- Code supporting the view
- Created with TypeScript
- Properties: data
- Methods: Logic

**Metadata:**

- Extra data for Angular
- Defined with a decorator



A simple component:

```ts
import { Component } from '@angular/core';

// Metadata & Template
@Component({
    selector: 'pm-root',
    template:
    `
	<div>
		<h1>{{pageTitle}}</h1>
		<div>My First Component</div>
	</div>
	`
})

// Class
export class AppComponent {
    pageTitle: string = 'Acme Product Managment';
}
```

> Note: It is convention to name the root component `AppComponent`



### Defining the Metadata with a Decorator

> **Decorator:** A function that adds metadata to a class, its members, or its method arguments.

- Decorators are prefixed with an `@`
- Angular provides built-in decorators. eg: `@Component()`

```ts
@Component({ // Component Decorator
    selector: 'pm-root', // Directive Name used in HTML
    template: // View layout
    `
	<div>
		<h1>{{pageTitle}}</h1> // Binding
		<div>My First Component</div>
	</div>
	`
})
```



### Importing

Lets us use exported members.

```ts
import { Component } from '@angular/core';
```



### Demo: Creating the App Component

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'pm-root', // Convention is to prefix the selector with something pertains to our app. ex: pm for product managment.
  template: 
  `
	<div>
		<h1>{{pageTitle}}</h1>
		<div>My First Component</div>
	</div>
	`
})
export class AppComponent {
  pageTitle: string = 'Acme Product Management';
}
```



### Bootstrapping our App Component

Referencing a component in `html`

```html
<body>
  <pm-root></pm-root>
</body>
```



Defining our Angular Module

```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [], // For future services...
  bootstrap: [AppComponent]
})
export class AppModule { }
```

> Note:  F12 opens the dev tools in the browser



------



## Templates, Interpolation, and Directives



### Building a Template

Linked Template: `templateUrl: './product-list.component.html' `



### Using a Component as a Directive

**Steps:**

1. Create a component and set it's selector: `selector: 'pm-products'`

2. Add the selector as a tag to a template file: `<pm-products></pm-products>`

3. Import the module and declare it in app.module.ts: 

   ```ts
   declarations: [
       AppComponent,
       ProductListComponent
     ],
   ```



### Binding with Interpolation

>  Binding coordinates communication between the component's class and it's template and often involves passing data.

Interpolation using a template expression 

ex: `{{pageTitle}}` 

is an example of one-way binding.

More examples:

```html
{{'Title: ' + pageTitle}}
{{2 * 20 + 1}}
{{'Title: ' + getTitle()}}
<h1 innerText={{pageTitle}}></h1>
```



### Adding Logic with Directives `ngIf`

A Directive is a custom HTML element or attribute used to power up and extend our HTML.

`*ngIf` - Removes or recreates the DOM tree based on the expression

ex: `*ngIf='products && products.length'`

`*ngFor` - Iterates over a list of objects.

ex: `*ngIf='let product of products'`

```html
<tr *ngFor='let product of products'>
    <td>{{ product.productName }}</td>
    <td>{{ product.productCode }}</td>
    <td>{{ product.releaseDate }}</td>
    <td>{{ product.price }}</td>
    <td>{{ product.starRating }}</td>
</tr>
```

> Why is it product `of` instead of product `in` products?

**for..of vs for..in**

ES2015 has both a **for…of** loop and **for…in** loop

**for…of:**

- Iterates over iterable objects, such as an array.

**for…in:**

- Iterates over the properties of an object.
- Iterates the **index**


------



## Data Binding and Pipes



### Property Binding

Let's you set the element property using an template expression.

ex: `<img [src]='product.imageUrl'> // This is the prefered method`

Similar binding using interpolation:

ex: `<img src={{product.imageUrl}}>`

`[] is the binding target`

`'' is the binding source`



### Handling Events with Event Binding

`<button (click)='toggleImage()'>`

`() is the target event`

`'' is the template statment`

``` ts
toggleImage(): void {
    this.showImage = !this.showImage;
}
```



### Handling Input with Two-way Binding

`<input [(ngModel)]='listFilter'>`

> Note: you mist import the formsModule to use ngModel

`import { FormsModule } from '@angular/forms';`

```ts
@NgModule({
...
imports: [
	FormsModule
]
...
})
```



### Transforming Data with Pipes

Pipes transform bound propeties before they are displayed.

**Built-in pipes:**

- date
- number, decimal, percent, currency
- json, slice
- etc




**Pipe Examples:**

```html
{{ product.productCode | lowercase }}
<img [src]='product.imageUrl'
	 [title]='product.productName | uppercase'>
{{ product.price | currency | lowercase }}
{{ product.price | currency:'USD':true:'1.2-2' }}
```



------



## More on Components



### Defining Interfaces

**Interface:** A **specification** identifying a related set or properties and methods.

> Note: A class commits to supporting the specifcation by **implementing** the interface.



Interface example:

```ts
export interface IProduct { // 'I' prefix is sometimes used
    productId: number;
    productName: string;
}
```

> Note: The 'I' prefix is used to visually designate it as an interface.



Using an interface:

``` ts
import { IProduct } from './product';

export class ProductListComponent {
    ...
    products: IProduct[] = [...];                     
	...
}
```



### Encapsulating Component Styles

**styles:**

```ts
@Component({
    styles:['thead {color: #337AB7;}']
})
```

**styleUrls:**

``` ts
@Component({
    styleUrls:['./product-list.component.css']
})
```



### Using Lifecycle Hooks

**Component Lifecycle:**

Create `->` Render `->` Create and render children `->` Process changes `->` Destroy



The most commonly used lifecycle hooks:

**OnInit:** Perform component initialization, retrieve data.

**OnChanges:** Perform action after change to input properties.

**OnDestroy:** Perform cleanup



```ts
// Import the hook
import { Component, OnInit } from '@angular/core';

// Implement the desired hook...
export class ProductListComponent implements OnInit {}

ngOnInit(): void {
    // Do something.
}
```



### Building Custom Pipes

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {
    transform(value: string, character: string): string {
        // Do work
    }
}
```

Using the pipe...

```html
<td>{{ product.productCode | convertToSpaces:'-' }}</td>
```



### Filtering a List

Angular doesn't offer built in filter pipes because...

"…they perform poorly and prevent aggressive minification."

​											*-angular.io*

Using getter and setters:

``` ts
_listFilter: string;
get listFilter(): string {
    return this._listFilter;
}
set listFilter(value:string) {
    this._listFilter = value;
    this.filteredProducts = this.listFilter ? this.performFilter(this.listFilter) : this.products;
}

...

constructor() {
    this.filteredProducts = this.products;
    this.listFilter = 'cart';
}

performFilter(filterBy: string): IProduct[] {
    filterBy = filterBy.toLocaleLowerCase();
    return this.products.filter((product: IProduct) => product.productName.toLocaleLowerCase().indexOf(filterBy) !== -1);
  }
```

> Note: Angular recommends that filter functionality be handled by the component.



## Building Nested Components

Two types of component nesting:

- As a Directive `<app-component></app-component>`
- As a Routing target: Full page style view



### Passing Data to a Nested Component (@Input)

> Note: Use the @Input() decorator to decorate any property in the component's class.

``` html
// Nesting a component
<td><pm-star [rating]='product.starRating'></pm-star></td>
// The here we set the rating via the @Input decorator
```

``` ts
// The nested component responds to the 'rating' change via ngOnChanges and updates the starWidth.
export class StarComponent implements OnChanges {
  @Input() rating: number;
  starWidth: number;

  ngOnChanges(): void {
    this.starWidth = this.rating * 86/5;
  }
}
```



### Passing Data from a Component Using @Output



``` html
// Inside star.component.html
<div class="crop" 
    [style.width.px]="starWidth"
    [title]="rating"
    (click)="onClick()"> // Firing the onClick function
    ....
```

``` ts
// Inside star.component.ts
onClick(): void {
    this.ratingClicked.emit(`The rating ${this.rating} was clicked.`)
  }
```

``` html
// Inside product-list.component.html
<td><pm-star [rating]='product.starRating'
            (ratingClicked)='onRatingClicked($event)'></pm-star></td>
```

``` ts
// Inside product-list.component.ts
onRatingClicked(message: string): void {
    this.pageTitle = 'Product List: ' + message;
  }
}
```

When the star component is clicked it emits an event that propagates to the container class. The container then displays the string value provided by the star component.



------



## Services and Dependency Injection



### How Does it Work?

Service:** A class with a focused purpose.

Used for features that:

- Are independent from any particular component
- Provide shared data or logic across components
- Encapsulate external interactions



**Dependancy Injection:** A coding pattern in which a class receives the instances of objects it needs (called dependencies) from an external source rather than creating them itself.

> Note :The Angular Injector provides singleton instances of service classes.



### Building a Service

Example service:

``` ts
import { Injectable } form '@angular/core'

@Injectable()
export class ProductService {
    getProducts(): IProduct[] {
    }
}
```

Regstering a provider:

``` ts
// Inside app.components.ts
...
providers: [ProductService]
...
```

Injecting the service:

```ts
// Create a private variable that is available throughout the component.
constructor(private _productService: ProductService) {

}
```

> Note: The "_" denotes a private variable.



------



## Retrieving Data Using HTTP



### Observables and Reactive Extensions

- Heps manage asynchrounous data
- Treats events as a collection
- Uses RxJS (Reactive Extensions)



Observable Operators:

- Methods on observables that compose new observables
- Transform the source observable in some way
- Process each value as it is emitted (eg: map, filter, take, and merge)



Promise vs Observable:

| Promise                        | Observable                                              |
| ------------------------------ | ------------------------------------------------------- |
| Provides a single future value | Emits multiple values over time                         |
| Not lazy                       | Lazy (will not emit values until they are subscrbed to) |
| Not cancellable                | Cancellable (unsubscribe)                               |
|                                | Supports map, filter, reduce and etc...                 |

### Sending an Http Request

![](/Users/willsaults/Documents/Knowledge-Database/Coding/Angular/Angular_Getting_Started/sending-an-http-request.png)

``` ts
// Http request example

import { HttpClient } from '@angular/common/http';

@Injectable()
export class ProductService {
    private _productUrl = 'www.myWebService.com/api/products';
    
    constructor(private _http: HttpClient) {}
    
    getProducts(): Observable<IProduct[]> {
        return this._http.get<IProduct[]>(this._productUrl);
    }
}
```

> Note: Specifying the get return type will automatically map the response for us.
>
> eg: `return this._http.get<IProduct[]>(this._productUrl);`



### Exception Handling & Subscribe to an Observable

``` ts
// products.service.ts
getProducts(): Observable<IProduct[]> {
    return this._http.get<IProduct[]>(this._productUrl)
      .do(data => console.log('All: ' + JSON.stringify(data)))
      .catch(this.handleError);
  }

  private handleError(err: HttpErrorResponse) {
    console.log(err.message);
    return Observable.throw(err.message);
  }
```

``` ts
// product-list.componets.ts
ngOnInit(): void {
    this._productService.getProducts()
      .subscribe(products => { 
        this.products = products; 
        this.filteredProducts = this.products;
      },
        error => this.errorMessage = <any>error);
  }
```



------



## Navigation and Routing Basics

### Handling Undefined

``` html
<div class='panel panel-primary'>
  <div class='panel-heading'>
    <!-- 
	 The save navigation operator '?' keeps us from seeing an 		 undefined value for the productName
	-->
    {{pageTitle + ': ' + product?.productName}}
  </div>
</div>
```

``` html
<!-- It's better to use the ngIf operator -->
<div class='panel panel-primary' *ngIf='product'>
  <div class='panel-heading'>
    {{pageTitle + ': ' + product.productName}}
  </div>
</div>
```



### How Routing Works

> Note: An Angular application is a Single Page Application.

- Configure a route for each component.
- Define options/actions
- Tie a route to each option/action
- Activate the route based on user action
- Activating a route displays the component's view



``` html
<a routerLink="/products">Products List</a>
```

The browser used the router link to identify the proper component via the path name.

``` ts
// Route definition...
{ path: 'products', component: ProductListComponent }
```

The router then displays the component's template.



### Configuring Routes

> Note: An Angular application has ONE router. Angular provides the `RouterModule` which registers the router service.



``` ts
// In app.module.ts
// Import this...
RouterModule.forRoot([], { useHash: true }) // establishes the routes for the root of the application and opts into using hash style routes.
```

``` ts
// Some route definitions:
[
	{ path: 'products', component: ProductListComponent },
    // This one specifies a parameter.
    { path: 'products/:id', component: ProductDetailComponent },
    { path: 'welcome', component: WelcomeComponent },
    // Defines a default route
    { path: '', redirectTo: 'welcome', pathMatch: 'full' },
    // Wildcard path
    { path: '**', component: PageNotFoundComponent }
]
```

> Note: More specific routes should appear higher in the list.



### Tying Routes to Actions

``` html
<a [routerLink]="['/welcome']">Home</a>
<a [routerLink]="['/products']">Product List</a>
```



### Placing the View

> Note: Use `router-outlet` to inject the view.

``` html
<router-outlet></router-outlet>
```



------



## Navigation and Routing Additional Techniques

### Passing Parameters to a Route

``` ts
{ path: 'products/:id', component: ProductDetailComponent }
```

``` html
<a [routerLink]="['/products', product.productId]">
    {{product.productName}}
</a>
```

``` ts
constructor(private _route: ActivatedRoute) { }

  ngOnInit() {
    // The Javascript shortcut '+' converts the string to a numeric id.
    let id = +this._route.snapshot.paramMap.get('id');
    this.pageTitle += `: ${id}`;
    this.product = {
      "productId": id,
      "productName": "Leaf Rake",
    }
  }
```



### Activating a Route with Code

``` ts
constructor(private _router: Router) { }

onBack(): void {
    this._router.navigate(['/products']);
}
```

``` html
<!-- Using onBack() -->
<a class='btn btn-default' (click)='onBack()' style='width:80px'>
    <i class='glyphicon glyphicon-chevron-left'></i> Back
</a>
```



### Protecting Routes with Guards

CanActivate

- Guard navigation to a route

CanDeactivate

- Guard navigation from a route

Resolve

- Pre-fetch data before activating a route

CanLoad

- Prevent asynchrounus routing



#### Using CanActivate

First create the guard service...

`ng g s products/product-guard.service -m app.module`

> Note: using `-m app.module` tells angular to register our service in the app module.

``` ts
// The product guard service

@Injectable()
export class ProductGuardService implements CanActivate {

  constructor(private _router: Router) { }

  // ActivatedRouteSnapshot gives us details about the route.
  canActivate(route: ActivatedRouteSnapshot): boolean {
    let id = +route.url[1].path;
    if (isNaN(id) || id < 1) {
      alert("Invalid product Id");
      this._router.navigate(['/products']);
      return false;
    }
    return true;
  }
}
```

``` ts
// Hook up the guard to a route in the router module.

RouterModule.forRoot([
      { path: 'products/:id', 
        canActivate: [ ProductGuardService ],
        component: ProductDetailComponent },
    ])
```



------



## Angular Modules

A class with an NgModule decorator

Purpose:

- Organize the pieces of our application
- Arrange them into blocks
- Extend our applicaiton with capabilities from external libraries
- Provide a template resolution environment
- Aggregate and re-export



### Bootstrap Array

1. Every application must bootstrap at least one component, the root application component.

2. The bootstrap array should only be used in the root applicaiton module, AppModule.



### Declarations Array

Contains the components, directives, and pipes.

1. Every component, directive, and pipe we create must belone to one and only one Angular module.

2. Only decloare components, directives, and pipes.

3. Never re-declare components, directives, or pipes that belone to another module.

4. All declared components, directives, and pipes are private by default.
They are only accessible to other compoments, directives, and pipes delcared in the same module.

5. The Angular module provides the template resolution environment for its component templates.



### Exports Array

1. Export any component, directive, or pipe if other components need it.
2. Re-export modules to re-export their components, directives, and pipes.
3. We can re-export something without importing it first.
4. Never export a service.



### Import Array

1. Importing a module makes available any exported components, directives, and pipes from that module.
2. Only import what this module needs.
3. Importing a module does NOT provide acces to its imported modules.



### Providers Array

1. Any service provider added to the providers array is registered at the root of the application.
2. Don't add services to the providers array of a shared module.
3. Routing guards must be added to the providers array of an Angular module.



### Feature Modules

Generate a new module:

`ng g m products/product --flat -m app.module`

> Note: use `RouterModule.forChild([])` in the product module.



------



## Angular CLI

Help: `ng --help`

Version: `ng -v`

New Application: `ng new hello-world`

New app with a prefix: `ng new hello-world --prefix hw`

Serve: `ng serve`

> Note: `localhost:4200` is the default angular url.

Serves with a new window: `ng serve -o`

Generate: `ng g c hello-component` 

> Note: See `ng g —help` for a long list of possible generations.

Test: `ng test` 

> Note: `ng test` lanches the karma test runner in watch-mode.

e2e test: `ng e2e`

> Note: uses protractor to execute the e2e specs.

Build: `ng build `

> Note: `ng build` creates the dist folder containing the app bundles.

> Note: use `--prod` to build the project files with hashes, minified, and tree shook.



