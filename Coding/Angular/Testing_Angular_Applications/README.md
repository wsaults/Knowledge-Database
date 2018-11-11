# Testing Angular Applications
> Copyright 2018 Manning Publications

## Chapter 1. Introduction to testing Angular applications

- Angular was built for testing web and mobile web apps!

### 1.1 Angular testing overview

- The two primary types of tests are unit and End-to-End (E2E).

The first half of this book covers testing:
- Components, Directives, Pipes, Services, and Routing.
- We will explore tools like Jasmine, Karma, and the Angular CLI.

Components are chunks of code that can be to encapsulate certain functionality that can be then reused throughout the application. Components are types of directives except they include a view or HTML template.

Directives are used to manipulate elements that exist in teh DOM or could also add or remove elements to the DOM. Examples of directives that come included with Angular are ngFor, ngIf, and ngShow.

Pipes are used to transform data.

Services are used to fetch data and inject that data into our components.

Routes allow users to navigate from one view to the next.

The second part of this book will dive into end-to-end testing using Protractor.

### 1.2 Getting friendly with TypeScript

TypeScript is a Microsoft product created in 2012 by Ander Hejlsberg who is also the creater of C#. The goal was to improve on JavaScript to support large-scale applications.

> !: JavaScript was created in 1995 in 10 days by Brenden Eich.

TypeScript adds:
- Annotations
- Static typing
- OO features (like interfaces and encapsulation)

#### TypeScript Class Example
```
export class Cat {
  private _name: string = '';

  constructor(name? : string) {
    this._name = name;
  }

  get name() : string {
    return this._name:
  }

  set name(name : string) {
    this._name = name;
  }

  toString() : string {
    return `This cat's name is ${this._name}!`;
  }
}
```
> Note: The '?' makes parameters optional.

### Types of tests
#### 1.3.3 Unit Tests

Unit tests should be:
- Fast
- Reliable
- Repeatable

#### Example of Simple Unit Test using Jasmine
```
describe('super basic test', () => {
  it('true is true', () => {
    expect(true).toEqual(true); // a simple smoke test.
  });
});
```

> Note: A smoke test is used to see if all the parts of your testing environment are set up correctly and you are just attempting to get a test to pass. A test this simple should not be in production.

#### Better example of a Unit Test
```
import { Cat } from './cat';

describe('Test Cat getters and setters.', () => {
  it('The cat name should be Gracie', () => {
    const cat = new Cat();
    cat.name = 'Gracie';
    expect(cat.name).toEqual('Gracie');
  });
});
```

#### End-to-end tests

> Note: the purpose of E2E tests is to simulate the behavior of an end user.

- Test that a modal appears correctly after a form is submitted.
- Test that elments such as buttons or text appears on page load.

> Note: E2Es can be the source of false positive failing tests due to timing out issues.

#### Example of Simple End-to-End
```
import { browser } from 'protractor';

describe('Contacts App title test', () => {
  it('Title should be correct', () => {
    const appUrl = 'https://contacts-app-starter.firebaseapp.com/';
    const expectedTitle = 'Contacts App Starter';
    browser.get(appUrl);
    browser.getTitle().then((actualTitle) => {
      expect(actualTitle).toEqual(expectedTitle);
    });
  });
});
```

## Chapter 2. Creating your first tests

- Write basic unit tests using Jasmine
- beforeEach, afterEach, it, describe
- Testing classes

### 2.1 Writing tests using Jasmine

> Note: Jasmine is a behavior-driven development framework (BDD).

- describe: used to group together a series of tests.
```
describe('message describing the test suite', callback);
```
- it: used when we want to create a specific test.
```
it('message describing the test', callback);
```
- expect: where you want to write the code for the test to work.
```
Matcher function examples:
toBe(), toContain(), toThrow, toEqual(), toBeTruthy(), toBeNull()...
```
> Documentation: [jasmine](https://jasmine.github.io/)


### 2.2 Testing classes

```
import SomeClass from './someClass';
```
> It's not necessary to include the .ts when importing a class.

```
let something: SomeClass = null;
```
> It is preferable to use let instead of var to solve various scoping issues. Let was introduced in ES6.

```
// This is known as the Setup part of the test.
beforeEach(() => {
  something = new SomeClass();
});
```
> It is common to reset a variable before every test to ensure that each is run independantly and that previous manipulated variables do not interfere with any other tests.

```
it('should have a valid constructor', () => {
  expect(something).not.toBeNull(); // '.toBeTruthy();' would be the same as '.not.toBeNull();'
});
```
> Note: using 'should' in your tests are optional.

```
afterEach(() => {
  something = null;
});
```
> Make sure to destroy instance varaibles to avoid memory leaks.

```
// Testing a constructor
it('should set name properly though constructor', () => {
  contact = new ContactClass('Liz');
  expect(contact.name).toEqual('Liz');
});
```

## Chapter 3. Testing Components

#### This chapter covers:
- Testing components
- Knowing the differences between isolated and shallow tests
- Testing classes and functions

> This chapter covers `TestBed`, `ComponentFixture`, `async`, and `fakeAsync`.

### 3.1 Basic component tests

```
it('should not contain contacts if there is no data', () => {
  expect(contactsComponent.contact.length).toBe(0);
});

it('should contain contacts if there is data', () => {
  const newContact: Contact = {
    id: 1,
    name: 'Jason Pipemaker'
  };
  const contactsList: Array<Contact> = [newContact];
  contactsComponent.contacts = contactsList;

  expect(contactsComponent.contacts.length).toBe(1);
});
```
> The tests above are known as *Isolated Tests* because they do not rely on any Angular dependencies.

### 3.2 Real-world component testing

*Shallow Tests:* Tests a component one level deep, thus ignoring any child element that it may contain. Using shallow tests allows you to test only the parent component in isolation.

### 3.2.1 Importing the dependencies

- import { DebugElement } from '@angular/core'; `DebugElement` can be used to inspect an element during testing. It adds additional methods and properties to the native `HTMLElement`.

- import { async, ComponentFixture, fakeAsync, TestBed, tick } from '@angular/core/testing'; 
  - `async` lets you wrap a test so that the `async` function will complete once all asynchronous calls have been completed.
  - `ComponentFixture` creates a fixture that can be used for debugging.
  - `TestBed` Extensive API used to set-up and configure our tests. https://angular.io/api/core/testing/TestBed
  - `fakeAsync` runs async tasks as though they were synchronous.
  - `tick`simulates the passage of time.
- `By` for selecting DOM elements. ex: `fixture.debugElement.query(By.css('.highlight-row'))`
  - `all`, `css`, `directives`
- `NoopAnimationsModule` to mock animations, allowing tests to run quickly without waiting for them to finish
- `BrowserDynamicTestingModule` helps bootsrap the browser for testing.
- `RouterTestingModule` to test out routing.

### 3.2.2 Setting up the tests

> Note: 
  - *test fake:* an object used in a test that substitutes for the real thing.
  - *mock:* a fake that simulates the real object and keeps track of when it's called and what arguments it receives.
  - *stub:* a simple fake with no logic that always returns the same value.

#### Table 3.3: TestingModuleMetadata optional fields
*declarations*: This is where you list any components that the component you are testing may need.

*imports*: Should be set to an array of moduels that the component you are testing requires.

*providers*: Lets you override the providers Angular uses for dependency injection. Like a fake ContactService.

*schemas*: You can use custom schemas.

*fixture.detectChanges*: Triggers a change-detection cycle for the component. Call it ater initializing a component or changing a data-bound property value. Those changes will be rendered in the DOM.

> Note: In general, you shouldn't test private methods; it a method is important enough to be tested, you should consider making it public.

#### Chapter Recap

- Shallow tests versus isolated tests. Isolated tests don’t rely on the built-in Angular classes and methods. They can be tested as if there are normal JavaScript classes. Sometimes our tests will require the actual rendering of components one level deep without requiring the rendering of child components. These types of tests are known as shallow tests.
- Using the async function, you can wrap a test function in an asynchronous test zone. The test inside the async function will complete automatically after all asynchronous calls within the asynchronous test zone have been completed.
- Use the ComponentFixture class to debug an element.
- TestBed is a class that is used to set-up and configure our tests. We use it anytime we want to write unit test that test out components, directives, and services.
- DebugElement can be used to dive deeper into an element. You can think of it as the nativeElement with additional methods and properties that can be useful to debug elements.
- The nativeElement object is an Angular wrapper around the built-in DOM native element.

## Chapter 4. Testing Directives

### This chapter covers:
- Using the types of directives available in Angular
- Testing attribute and structural directives
- Using TestMetaData to configure TestBed
