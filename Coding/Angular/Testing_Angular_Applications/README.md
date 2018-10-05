# Testing Angular Applications
> Copyright 2018 Manning Publications

## 1. Introduction to testing Angular applications

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