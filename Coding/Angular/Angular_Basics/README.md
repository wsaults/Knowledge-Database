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

**Key Terms:**

- **Component Decorator:** Components are the backbone of an Angular application. The Component Decorator is for defining a component and registering it with Angular. Each component must have a selector and a template to be valid.

