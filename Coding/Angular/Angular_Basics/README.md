# Angular Basics



## Setting Up an Angular Application



### Why Angular 2?

- It's modular.
- It's build on a static language (typescript)
- It's backed by Google and has a large community of developers.



> Note: Angular refers to Angular 2 and it's departure from the previous AngularJS.



### The Parts and Pieces of an Agular Application

- Each app has one root module and is the starting point of the application.
- Services employ actions behind the scenes.
- Components combine templates, styles, and logic to make up the heart of the applicaiton.



### Your First Angular Application 

```
npm install
```

```
npm run serve
```

app.module.ts

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component'; 

@NgModule({ // Angular decorator for efficient platform support.
  imports: [BrowserModule], // Tells the application that it will be used for the web browser.
  declarations: [AppComponent], // Registers the app's components
  bootstrap: [AppComponent] // Tells angular to start teh app components at launch
})

export class AppModule {}
```



app.components.ts

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root', // Inserts our component into the index.html
  template: `<h2>Hello World</h2>`,
  styles: [
    `
    h2 {
      font-family: sans-serif;
      font-size: 1.2em;
    }
    `
  ]
})

export class AppComponent {}
```



main.ts

```typescript
// Import global stylesheet
import './styles/main.css';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule); // Bootstrap and attach the module to the webpage.
```



------



## Angular Components



### The Anatomy of a Component

Component = Template + Class + Decorator

**Key Terms:**

- **Component Decorator:** Components are the backbone of an Angular application. The Component Decorator is for defining a component and registering it with Angular. Each component must have a selector and a template to be valid.

```typescript
// app.component.ts

@Component({
  selector: 'app-root', // Inserts our component into the index.html
  templateUrl: 'app.component.html', // Points to the html file
  styleUrls: ['app.component.css'] // Points to the css file
})

export class AppComponent {
  emoji: string[]; // Declares an array of strings.

  constructor() {
    this.emoji = ['🎉', '😍', '😜', '👍']; // Initilzes the array of strings.
  }
}
```

The array can also be defined more simply like this...

```typescript
export class AppComponent {
  emoji: string[] = ['🎉', '😍', '😜', '👍'];
}
```

And even more simply like this...

```typescript
emoji = ['🎉', '😍', '😜', '👍'];
```



Then interpolate the emoji array into the template. This is refered to as data binding.

```typescript
// app.component.html

<h2>Hello World {{emoji}}</h2>
```



### Data-binding

The ability to pass data between the component class and the template.

**Types of Data Binding:**

- **One-Way:** Class to Template
- **One-Way:** Template to Class
- **Two-Way:** Between Class and Template

```html
// One-Way: Class to Template
<h1>{{expression}}</h1>
<input [target]="expression" />
```

```html
// One-Way: Template to Class
<button (event)="expression"></button>
```

```html
// Two-Way: Between Class and Template
<input [(target)]="expression" />
```



### Nesting Components

```ts
// AppModule

import { EntryListComponent, EntryComponent } from './entries'; // Importing all components via the entry/index.ts barrel file

@NgModule({
  declarations: [
    EntryComponent, // List the child components first
    EntryListComponent
  ], // Registers the app's components
})
```

```ts
// entries/index.ts
// Known as a barrel

export * from './entry-list/entry-list.component';
export * from './entry/entry.component';
```

```html
// entry-list.component.html

Hello from entry-list.component.html

<app-entry></app-entry>
```



### Component Templates and Styles

``` ts
// entry.component.ts

export class EntryComponent {
  title: string = 'My first photo';
  photo: string = 'http://placehold.it/800x500?text=Angular Basics';
  description: string = 'A description of my first photo.';
}
```

``` html
// entry.component.html

<h2>{{title}}</h2>
<figure>
  <img src="{{photo}}">
  <figcaption>{{description}}</figcaption>
</figure>
```

``` css
// entry.component.css

figure {
  margin: 0;
  border: 1px solid #000;
  position: relative;
}

figcaption {
  background-color: rgba(0, 0, 0, 0.5);
  color: #fff;
  font-size: 1.2em;
  padding: 10px;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
}

img {
  display: block;
  width: 100%;
  height: auto;
}

:host { // Targets the element that hosts this component.
  padding: 1em;
  display: block;
}
```



### Structural Directives

Directives allow you to:

- Control Visiblity
- Apply Styling
- Loop Over Items
- Extend Application with Custom Scripts

> Note: Structural directives allow you to hide and reveal content inside a content using NgIf and NgFor

``` ts
// entry.component.ts

export class EntryComponent {
  title: string = 'My first photo';
  photo: string = 'http://placehold.it/800x500?text=Angular Basics';
  description: string = 'A description of my first photo.';
  comments: any[] = [
    {name: "John", comment: "A comment"},
    {name: "Jim", comment: "A comment"},
    {name: "Jane", comment: "A comment"},
    {name: "Jen", comment: "A comment"},
  ];
}
```

``` html
// entry.component.html

<h2>{{title}}</h2>
<figure>
  <img src="{{photo}}">
  <figcaption>{{description}}</figcaption>
</figure>
<div class="actions">
  <button type="button" (click)="isLiked = !isLiked" [ngClass]="{liked: isLiked}">❤</button>
  <button type="button" (click)="showComments = !showComments">Comments ({{comments.length}})</button>
</div>
<div class="comments" *ngIf="showComments">
  <div class="comment" *ngFor="let comment of comments">
    <p><strong>{{comment.name}}</strong> {{comment.comment}}</p>
  </div>
</div>
```



## Services in Angular - Sending and Retrieving Data



### Locating and Installing Angular Modules

Run the following in the terminal: `npm install @angular/http@2.4.2 —save —save-exact`

```ts
// Inside vendor.ts
...
import '@angular/http';
```

``` ts
// Inside app.module.ts
...
import { HttpModule } from '@angular/http';
...
imports: [
    BrowserModule,
    HttpModule
  ]
...
```



### Dependency Injection

```ts
// Inside entry-list.component.ts

import { Http } from '@angular/http';

export class EntryListComponent {
  constructor(http: Http) {
      http.get('/app/entries').toPromise()
        .then(response => {debugger;}, error => {debugger});
  }
}
```



### Creating a Service

```ts
// Inside entry.service.ts	

import { Entry } from './entry.model';
import { Injectable } from "@angular/core";
import { Http } from '@angular/http';

@Injectable() // Angular requires a service to be Injectable
export class EntryService {

  constructor(private http: Http) {

  }

  getEntries(): Promise<Entry[]> {
    return this.http.get('/app/entries')
      .toPromise()
      .then(response => response.json().data as Entry[]);
  }
}
```

```ts
// Inside entry.model.ts

export class Entry {
  title: string;
  photo: string;
  description: string;
  comments: any[] = [];
}
```



### Connecting a Service and Component

In terminal use:

 `npm install angular-in-memory-web-api@0.2.4 --save --save-exact`

`npm install file-loader --save-dev --save-exact`



```html
// Inside entry.component.html

<h2>{{entry.title}}</h2>
<figure>
  <img src="{{entry.photo}}">
  <figcaption>{{entry.description}}</figcaption>
</figure>
<div class="actions">
  <button type="button" (click)="isLiked = !isLiked" [ngClass]="{liked: isLiked}">❤</button>
  <button type="button" (click)="showComments = !showComments">Comments ({{entry.comments.length}})</button>
</div>
<div class="comments" *ngIf="showComments">
  <div class="comment" *ngFor="let comment of entry.comments">
    <p><strong>{{comment.name}}</strong> {{comment.comment}}</p>
  </div>
</div>
```

```ts
// Inside entry.component.ts

import { Component, Input } from '@angular/core';
import { Entry } from '../shared/entry.model';

@Component({
  selector: 'app-entry',
  templateUrl: 'entry.component.html',
  styleUrls: ['entry.component.css']
})

export class EntryComponent {
  @Input() entry: Entry;
}
```

```ts
// Inside entry-list.component.ts

import { Component, OnInit } from '@angular/core';
import { EntryService } from '../shared/entry.service';
import { Entry } from '../shared/entry.model';

@Component({
  selector: 'app-entry-list',
  templateUrl: 'entry-list.component.html',
  styleUrls: ['entry-list.component.css']
})

export class EntryListComponent implements OnInit {
  entries: Entry[];

  constructor(private entryService: EntryService) {
      
  }

  ngOnInit() {
    this.entryService
      .getEntries()
      .then(entries => this.entries = entries)
  }
}
```

```html
// Inside entry-list.component.html

<app-entry *ngFor="let entry of entries" [entry]="entry"></app-entry>
```



### Summary

When creating a component you add dependencies by setting them as parameters of the constructor function.



------



## Basic Forms



### Adding NgForms Module

There are two ways to build forms in Angular:

- Template Driven
- Dynamic



In terminal: `npm install @angular/forms@2.4.2 --save --save-exact`

> Note: Import `@angular/forms` similar to `@angular/http`



### Setting Up a Form Group

```ts
// Inside entry.component.html
// Add this to the comments div
<app-entry-comment-form></app-entry-comment-form>
```

```ts
// Inside entry-comment-form.components.ts

import { Component } from '@angular/core';

@Component({
  selector: 'app-entry-comment-form',
  templateUrl: 'entry-comment-form.component.html'
})

export class EntryCommentFormComponent {

}
```

``` html
// Inside entry-comment-form.component.html

<form>
  <div>
    <label for="name">Name</label>
    <input type="text" name="name" />
  </div>
  <div>
    <label for="comment">Comment</label>
    <textarea name="comment"></textarea>
  </div>
  <div>
    <button>Submit</button>
  </div>
</form>
```



### Two-way Data Binding with NgModel

> A way of keeping the data in sync no matter where the value is changed.

> Note: When a `<form>` element is used the Forms Module applies the `NgForm` directive automatically.

``` ts
// Inside entry-comment-form.component.ts

...
export class EntryCommentFormComponent {
  name: string = "";
  comment: string = "";
}
```

``` html
// Inside entry-comment-form.component.html

<form>
  <div>
    <label for="name">Name</label>
    <input type="text" name="name" [(ngModel)]="name" />
  </div>
  <div>
    <label for="comment">Comment</label>
    <textarea name="comment" [(ngModel)]="comment"></textarea>
  </div>
  <div>
    <button>Submit</button>
  </div>
</form>
```



### Submitting Form Data

``` html
// Inside entry.component.html

<app-entry-comment-form (onCommentAdded)="onCommentAdded($event)"></app-entry-comment-form>
```

``` ts
// Inside entry-comment-form.component.ts

...
@Output() onCommentAdded = new EventEmitter<{name: string; comment: string;}>();

  onSubmit() {
    let comment = { name: this.name, comment: this.comment };
    this.onCommentAdded.emit(comment);
  }
...
```

``` html
// Inside entry-comment-form.component.html

<form (submit)="onSubmit()">
```



### Resetting the Form

``` html
// Inside entry-comment-form.component.html

<form (submit)="onSubmit()" #commentForm="ngForm">
```

``` ts
// Inside entry-comment-form.component.ts

import { Component, EventEmitter, Output, ViewChild } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
  selector: 'app-entry-comment-form',
  templateUrl: 'entry-comment-form.component.html'
})

export class EntryCommentFormComponent {
  name: string = "";
  comment: string = "";
  @Output() onCommentAdded = new EventEmitter<{name: string; comment: string;}>();
  @ViewChild('commentForm') commentForm: NgForm;

  onSubmit(commentForm: NgForm) {
    let comment = { name: this.name, comment: this.comment };
    this.onCommentAdded.emit(comment);
    this.commentForm.resetForm();
  }
}
```



### Posting Data Using a Service

``` html
// Inside entry.component.html
<app-entry-comment-form (onCommentAdded)="onCommentAdded($event)" [entryId]="entry.id"></app-entry-comment-form>
```

``` ts
// Inside entry.service.ts
import { Entry } from './entry.model';
import { Injectable } from "@angular/core";
import { Http } from '@angular/http';

@Injectable() // Angular requires a service to be Injectable
export class EntryService {

  constructor(private http: Http) {

  }

  addComment(entryId: number, comment: { name: string; comment: string; }) {
    return this.http.post(`/app/entries/${entryId}/comments`, comment)
      .toPromise();
  }

  getEntries(): Promise<Entry[]> {
    return this.http.get('/app/entries')
      .toPromise()
      .then(response => response.json().data as Entry[]);
  }
}
```

``` ts
// Inside entry-comment-form.components.ts
import { Component, EventEmitter, Input, Output, ViewChild } from '@angular/core';
import { NgForm } from '@angular/forms';
import { EntryService } from '../shared/entry.service';

@Component({
  selector: 'app-entry-comment-form',
  templateUrl: 'entry-comment-form.component.html'
})

export class EntryCommentFormComponent {
  name: string = "";
  comment: string = "";
  @Input() entryId: number;
  @Output() onCommentAdded = new EventEmitter<{name: string; comment: string;}>();
  @ViewChild('commentForm') commentForm: NgForm;

  constructor(private entryService: EntryService) {

  }

  onSubmit(commentForm: NgForm) {
    let comment = { name: this.name, comment: this.comment };
    this.entryService.addComment(this.entryId, comment)
      .then(() => {
        this.onCommentAdded.emit(comment);
        this.commentForm.resetForm();
      });
  }
}
```

> Note: The `ViewChild` decorator lets the component inspect the template for local varaibles and assign them to members of a component.

> Note: Angular's Event Emitter does NOT register a global event.

Example of an event binding in HTML:

```html
<button (click)="doThis()">click me</button>
```



------



##Form Validation 



### HTML5 Input Rules

Making a field required: 

``` html
// Add `requried` to the element.
<input type="text" name="name" [(ngModel)]="name" required />
```

Adding a required element length:

``` html
<input type="text" name="name" [(ngModel)]="name" required minlength="3"/>
```



### Form and Input State

`novalidate` lets the browser know that we will be taking care of the validations and to suppress any validation messages.

``` html
<form (submit)="onSubmit()" #commentForm="ngForm" novalidate>
```

``` html
// Inside entry-comment-form.component.html

<input type="text" name="name" [(ngModel)]="name" required minlength="3" #nameField="ngModel" />
    <div class="alert alert-danger" *ngIf="(commentForm.submitted || nameField.dirty || nameField.touched) && nameField.errors">
      <div [hidden]="!nameField.errors.required">Name is required</div>
      <div [hidden]="!nameField.errors.minlength">Name must be a minimum of 3 characters long</div>
    </div>
```

> Note: The `invalid` property on an `NgForm` returns true if the form is invalid.



### Styling Form Input

Styling when an element is valid:

``` html
<input type="text" name="name" [(ngModel)]="name" 
      required minlength="3" #nameField="ngModel" 
      [ngStyle]="{'outline-color': nameField.dirty && nameField.valid ? 'green' : undefined }" />
```

> Note: The `ngStyle` directive lets you add styles inline.

> Note: When binding to the `hidden` attribute we can hide or show an element.

