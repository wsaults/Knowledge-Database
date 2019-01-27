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

```typescript
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

```typescript
describe('super basic test', () => {
  it('true is true', () => {
    expect(true).toEqual(true); // a simple smoke test.
  });
});
```

> Note: A smoke test is used to see if all the parts of your testing environment are set up correctly and you are just attempting to get a test to pass. A test this simple should not be in production.

#### Better example of a Unit Test

```typescript
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

```typescript
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

```typescript
describe('message describing the test suite', callback);
```

- it: used when we want to create a specific test.

```typescript
it('message describing the test', callback);
```

- expect: where you want to write the code for the test to work.

```typescript
Matcher function examples:
toBe(), toContain(), toThrow, toEqual(), toBeTruthy(), toBeNull()...
```

> Documentation: [jasmine](https://jasmine.github.io/)


### 2.2 Testing classes

```typescript
import SomeClass from './someClass';
```
> It's not necessary to include the .ts when importing a class.

```typescript
let something: SomeClass = null;
```

> It is preferable to use let instead of var to solve various scoping issues. Let was introduced in ES6.

```typescript
// This is known as the Setup part of the test.
beforeEach(() => {
  something = new SomeClass();
});
```

> It is common to reset a variable before every test to ensure that each is run independantly and that previous manipulated variables do not interfere with any other tests.

```typescript
it('should have a valid constructor', () => {
  expect(something).not.toBeNull(); // '.toBeTruthy();' would be the same as '.not.toBeNull();'
});
```
> Note: using 'should' in your tests are optional.

```typescript
afterEach(() => {
  something = null;
});
```
> Make sure to destroy instance varaibles to avoid memory leaks.

```typescript
// Testing a constructor
it('should set name properly though constructor', () => {
  contact = new ContactClass('Liz');
  expect(contact.name).toEqual('Liz');
});
```

## Chapter 3. Testing Components

#### This chapter covers

- Testing components
- Knowing the differences between isolated and shallow tests
- Testing classes and functions

> This chapter covers `TestBed`, `ComponentFixture`, `async`, and `fakeAsync`.

### 3.1 Basic component tests

```typescript
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

### This chapter covers

- Using the types of directives available in Angular
- Testing attribute and structural directives
- Using TestMetaData to configure TestBed

Directives, like components, are a way to encapsulate parts of your application into reusable chuncks of code.

> The only difference between directives and components is that components contain a view.

There are three types of directives:

- Components
- Structural directives
- Attribute directives

### 4.1.1 Componets vs directives

Decorators are a way to add behavior to a class or method.

### 4.1.2 Attribute directives

Attribute directives are used when you are trying to change the apperance of a DOM element.

### 4.1.3 Strucural directives

Structure directives are used to add or remove elements from the DOM.

```typescript
// Creating your own directive looks something like this...
@Directive({
  selector: '[appFavoriteIcon]'
})
export class FavoriteIconDirective implements OnInit {
  ...
}
```

`fixture.detectChanges()` is used to invoke change detection and render updated data whenever an event occurs, such as a click or a mouseenter.

### 4.2.4 Creating the Favorite Icon directive tests

Getting the color of a debug element.

```typescript
expect(starElement.style.color).toBe('gold');
```

Testing a mouseenter event:

```typescript
it('should display a solid gold star if the user rolls over the star', () => {
      const event = new Event('mouseenter');
      starElement.dispatchEvent(event);
      expect(starElement.style.color).toBe('gold');
      expect(doClassesMatch(starElement.classList, expectedSolidStarList)).toBeTruthy();
});

```

### 4.3.4 Creating the ShowContactsDirective test

Testing the text of an element

```typescript
export function getElement(fixture: ComponentFixture<ComponentRef<any>>): HTMLElement {
  const el: HTMLElement = fixture.nativeElement as HTMLElement;
  return el;
}

it('should be displayed when the input evaluates to true.', () => {
  const element = getElement(fixture);
  expect(element.innerText).toContain('This is shown');
});
```

## Chapter 5 Testing Pipes

Example pipe test

```typescript
describe('PhoneNumberPipe Tests', () => {
    let phoneNumber: PhoneNumberPipe = null;

    beforeEach(() => {
       phoneNumber = new PhoneNumberPipe();
    });

    describe('default behavior', () => {
       it('should transform the string or number into the default phone format', () => {
          const testInputPhoneNumber = '7035550123';
          const transformedPhoneNumber = phoneNumber.transform(testInputPhoneNumber);
          const expectedResult = '(703) 555-0123';

          expect(transformedPhoneNumber).toBe(expectedResult);
       });
    });

    afterEach(() => {
       phoneNumber = null;
    });
});
```

Example pipe test using an argument

```typescript
describe('phone number format tests', () => {
    it('should format the phone number using the dots format', () => {
      const testInputPhoneNumber = '7035550123';
      const format = 'dots';
      const transformedPhoneNumber = phoneNumber.transform(testInputPhoneNumber, format);
      const expectedResult = '703.555.0123';

      expect(transformedPhoneNumber).toBe(expectedResult);
    });
});
```

## Chapter 6 Testing Services

Create BrowserStorageMock

```typescript
class BrowserStorageMock {
    getItem = (property: string) => ({ key: 'testProp', value: 'testValue '});
    setItem = ({ key: key, value: value }) => {};
}
```

Configure the TestBed dependency injection to use BrowserStorageMock instead of the real service

```typescript
beforeEach(() => {
    TestBed.configureTestingModule({
        providers: [PreferencesService, {
            provide: BrowserStorage, useClass: BrowserStorageMock
        }]
    });
});
```

Use inject to get the BrowserStorageMock
Add a spy to browserStorage.setItem
Check the spy to make sure it was called from saveProperty()
[Testing dependency injection](https://youtu.be/iy35OhhtYgc?t=105)

```typescript
describe('save preferences', () => {
    it('should save a preference', inject([PreferencesService, BrowserStorage],
        (service: PreferencesService, browserStorage: BrowserStorageMock) => {

            spyOn(browserStorage, 'setItem').and.callThrough();
            service.saveProperty({ key: 'myProperty', value: 'myValue' });
            expect(browserStorage.setItem).toHaveBeenCalledWith('myProperty', 'myValue');
        })
    );       
});
```

Listing 6.8 Unit test for checking that a bad input throws an error.

```typescript
it('saveProperty should require a non-zero length key',
    inject([PreferencesService],  (service: PreferencesService) => {
 
    const fn = () => service.saveProperty({ key: ‘’, value: ‘foo’ });
 
    expect(fn).toThrowError();
  })
);
```

Listing 6.9 Incorrect and correct way to write asynchronous Jasmine tests

```typescript
it('is an asynchronous test', () => {
    setTimeout(() => {
        expect(true).toBe(false);
 });
});

it('is an asynchronous test', (done) => {
    setTimeout(() => {
        expect(true).toBe(false);
     done();
 });
});
```

Listing 6.13 Setting up TestBed before each test

```typescript
import { TestBed, fakeAsync, inject } from '@angular/core/testing';
import { Http, BaseRequestOptions, Response, ResponseOptions, RequestMethod } from '@angular/http';
import { MockBackend, MockConnection } from '@angular/http/testing';
 
import { ContactService } from './contact.service';
 
describe('ContactsService', () => {
    beforeEach(() => {
        TestBed.configureTestingModule({
            providers: [
                ContactService,
                MockBackend,
                BaseRequestOptions,
                {
                    provide: Http,
                    useFactory: (backend, options) => new Http(backend, options),
                    deps: [MockBackend, BaseRequestOptions]
                }
            ]
        });
    });
 
});
```

Listing 6.14 Unit testing ContactsService.getContacts()

```typescript
describe('getContacts', () => {
  let mockBackend;
  let mockContact;
  let mockGetContactsResponse;
 
  beforeEach(inject([MockBackend], (_MockBackend_) => {
    mockBackend = _MockBackend_;
    mockContact = { id: 100, name: 'Erin Dee', email: 'edee@example.com' };
    mockGetContactsResponse = new Response(new ResponseOptions({ body: { data: [ mockContact ] }}));
  }));
 
  afterEach(() => {
    mockBackend.verifyNoPendingRequests();
    mockBackend.resolveAllConnections();
  });
 
  it('should GET a list of contacts',
    fakeAsync(inject([ContactService], (service) => {
 
      mockBackend.connections //
        .subscribe((connection: MockConnection) => {        
          expect(connection.request.method).toEqual(RequestMethod.Get);
          connection.mockRespond(mockGetContactsResponse);
        });
 
      service.getContacts() //
        .subscribe((contacts) => {
          expect(contacts[0]).toEqual(mockContact);
        });
    }))
  );
});
```

## Chapter 7 Testing Router

> The Angular router is part of the Angular framework that converts the web address to a specific view of the Angular application.

### 7.1.1 Configuring the router

```typescript
// Example router configuration
export const routes: Routes = [
 { path: '', component: ContactsComponent },
 { path: 'add', component: NewContactComponent },
 { path: 'contacts', component: ContactsComponent },
 { path: 'contact/:id', component: ContactDetailComponent },
 { path: 'edit/:id', component: ContactEditComponent },
 { path: '**', component: PageNotFoundComponent }
];
```

### 7.2.1 Testing router navigation with RouterTestingModule

When using `fakeAsync`, you have to resolve outstanding asynchronous calls manually with the flush method, and then update the fixture with `detectChanges`.

```typescript
beforeEach(fakeAsync(() => {
  router = TestBed.get(Router);
  location = TestBed.get(Location);
  fixture = TestBed.createComponent(AppComponent);
router.navigateByUrl('/');
advance();
}));

function advance(): void {
flush();
fixture.detectChanges();
}
```

### 7.3.1 Route guards

```typescript
// Listing 7.10 AuthenticationGuard service
@Injectable()
class AuthenticationGuard implements CanActivate {
 constructor(private userAuth: UserAuthentication) {}
 canActivate(): Promise<boolean> {
 return new Promise((resolve) =>
 resolve(this.userAuth.getAuthenticated());
 );
 }
}

@Injectable()
class UserAuthentication {
 private isUserAuthenticated: boolean = false;
 authenticateUser() {
 this.isUserAuthenticated = true;
 }
 getAuthenticated() {
 return this.isUserAuthenticated;
 }
}
```

```typescript
// Listing 7.11 Setting up the AuthenticationGuard test
beforeEach(() => {
  TestBed.configureTestingModule({
 imports: [RouterTestingModule.withRoutes([
      { path: '', component: AppComponent },
      {
        path: 'protected',
        component: TargetComponent,
 canActivate: [AuthenticationGuard],
      }
      ])],
    providers: [AuthenticationGuard, UserAuthentication],
    declarations: [TargetComponent, AppComponent],
  });

  router = TestBed.get(Router);
  location = TestBed.get(Location);
 userAuthService = TestBed.get(UserAuthentication);
});

beforeEach(fakeAsync(() => {
  fixture = TestBed.createComponent(AppComponent);
  router.initialNavigation();
}));
```

```typescript
// Listing 7.12 AuthenticationGuard tests
it('tries to route to a page without authentication', fakeAsync(() => {
 router.navigate(['protected']);
  flush();
  expect(location.path()).toEqual('/');
}));

it('tries to route to a page after authentication', fakeAsync(() => {
 userAuthService.authenticateUser();
  router.navigate(['protected']);
  flush();
  expect(location.path()).toEqual('/protected');
}));
```

> Note: These tests make sure the route guards behave correctly under different application scenarios.

### 7.3.2 Resolving data before loading a route

```typescript
// Listing 7.13 Configured resolver route guard
{
  path: 'contacts',
  component: TargetComponent,
  resolve: {
    userPreferences: UserPreferencesResolver,
    contacts: ContactsResolver
  }
}
```

---

 Part 2 End-to-end testing

---

## Chapter 8

> Note: Integration tests involve validating external dependencies via mocks. End-to-end tests use the real version.

```typescript
// Listing 8.4 Test specification—e2e/first-test.e2e-spec.ts
import { browser } from 'protractor';

describe('your first protractor test', () => {
  it('should load a page and verify the url', () => {
    browser.get('/#/');
    expect(browser.getCurrentUrl())
        .toEqual(browser.baseUrl + '/#/');
  });
});
```

### 8.4 Interacting with elements

> Note: this section introduced `element` and `by`.

The `by` API has methods to find web elements using an identifier. The `element` API consumes the object generated by the `by` API and returns a Protractor `ElementFinder` object that represents the web element.

### 8.4.1 Test scenario: creating a new contact

```typescript
// Listing 8.7 Test specification to create a new contact—e2e/add-contact.e2e-spec.ts
import { browser, by, element } from 'protractor';

describe(adding a new contact with only a name', () => {
  beforeAll(() => {
    browser.get('/#/');
  });

  it('should find the add contact button', () => {
  element(by.id('add-contact')).click();
    expect(browser.getCurrentUrl())
        .toEqual(browser.baseUrl + '/#/add');
  });

  it('should write a name', () => {
  let contactName = element(by.id('contact-name'));
    contactName.sendKeys('Ada');
    expect(contactName.getAttribute('value'))
        .toEqual('Ada');
  });

  it('should click the create button', () => {
  element(by.css('.create-button')).click();
    expect(browser.getCurrentUrl())
        .toEqual(browser.baseUrl + '/#/');
  });
});
```

```typescript
// Listing 8.8 Test to create another contact—e2e/add-second-contact.e2e-spec.ts
import { browser, by, element } from 'protractor';

describe('adding a new contact with name, email,' +
    'and phone number', () => {
  beforeAll(() => {
    browser.get('/#/');
    element(by.id('add-contact')).click();
    element(by.id('contact-name')).sendKeys('Grace');
  });

  it('should type in an email address', () => {
 let email = element(by.id('contact-email'));
 email.sendKeys('grace@hopper.com');
    expect(email.getAttribute('value'))
        .toEqual('grace@hopper.com');
  });

  it('should type in a phone number', () => {
 let tel = element(by.css('input[type="tel"]'));
    tel.sendKeys('1234567890');
    expect(tel.getAttribute('value'))
        .toEqual('1234567890');
  });

  it('should click the create button', () => {
    element(by.css('.create-button')).click();
    expect(browser.getCurrentUrl())
        .toEqual(browser.baseUrl + '/#/');
  });
});
```

### 8.4.2 Test scenario: workflows that don't create a new contact

> Note: using `EC` (Expected Conditions) to test `precenseOf`

```typescript
// Listing 8.9 Test that doesn’t create a new contact—e2e/invalid-contact.e2e-spec.ts
import { browser, by, element, ExpectedConditions as EC } from 'protractor';

describe('adding a new contact with an invalid email', () => {
  beforeEach(() => {
    browser.get('/#/add');
    element(by.id('contact-name')).sendKeys('Bad Email');
  });

  it('shouldn’t create a new contact with baduser.com', () => {
    let email = element(by.id('contact-email'));
    email.sendKeys('baduser.com');
    element(by.buttonText('Create')).click();

    let invalidEmailModal = element(by.tagName(
        'app-invalid-email-modal'));
 expect(invalidEmailModal.isPresent()).toBe(true);

    let modalButton = invalidEmailModal.element(
 by.tagName('button'));
    modalButton.click();

    browser.wait(EC.not(
 EC.presenceOf(invalidEmailModal)), 5000);
 expect(invalidEmailModal.isPresent()).toBe(false);
    expect(browser.getCurrentUrl()).toEqual(
        browser.baseUrl + '/#/add');
    });
});
```

### 8.5 by and element methods

#### by.css

Finding a web element by css
**HTML:**

```html
<input class="contact-email" id="contact-email" type="email">
```

**Protractor:**

```typescript
let e1 = element(by.css('.contact-email'));
let e2 = element(by.css('#contact-email'));
let e3 = element(by.css('input[type="email"]'));
```

---

#### by.id

Finding a web element by id
**HTML:**

```html
<input class="contact-email" id="contact-email" type="email">
```

**Protractor:**

```typescript
let email = element(by.id('contact-email'));
```

---

#### by.buttonText && by.partialButtonText

Finding a button with the matching text
HTML:

```html
<button>Submit Contact</button>
```

Protractor:

```typescript
let fullMatch = element(by.buttonText( 'Submit Contact'));
let partialMatch = element(by. partialButtonText('Submit'));
```

---

#### by.linkText && by.partialLinkText

Finding a link by matching text
HTML:

```html
<a href="/add">Add contact</a>
```

Protractor:

```typescript
let fullMatch = element(by.linkText( 'Add contact'));
let partialMatch = element(by. partialLinkText('contact'));
```

---

#### by.tagname

Finding a web element by tag name
HTML:

```html
<app-contact-detail>…</app-contact-detail>
```

Protractor:

```typescript
let tag = element(by.tagName( 'app-contact-detail'));
```

> Note: You should remember that Protractor’s `by` and Selenium WebDriver’s `by` are different.

#### isPresent && isElementPresent

 Note: When testing Angular structural directives like *ngIf, you need to call isPresent to validate if a web element exists on the screen.

 ```typescript
 expect(element(by.id('contact-email')).isPresent()).toBe(false);
 ```

#### getAttribute

When typing values into input fields, you can validate you entered them properly using the getAttribute method. To get the contents of an input field, you’ll need to get the 'value' attribute. A common mistake is to try to use the getText method to get the text from an input field:

```typescript
browser.get('/#/add');
let email = element(by.id('contact-email')); email.sendKeys('foobar');
expect(email.getAttribute('value')).toBe('foobar');
```

#### sendKeys

Use sendKeys to simulate typing in text—for example, to fill out an input field:

```typescript
browser.get('/#/add');
element(by.id('contact-name')).sendKeys('foobar');
expect(element(by.id('contact-name')).getAttribut('value')).toBe('foobar');
```

#### isDisplayed

You can check if an element is present but hidden from view with isDisplayed. If a web element is hidden but still part of the DOM, Protractor will return that it’s present but not displayed:

```typescript
browser.get('/#/add'); let contactName = element(by.id('contact-name'));
expect(contactName.isDisplayed()).toBe(true);
expect(contactName.isPresent()).toBe(true);
expect(contactName.isDisplayed()).toBe(false);
```

### 8.6 Interacting with a list of elements

> **Note:** A common gotcha is to try to iterate over the collection of web elements with a for loop. You can’t loop through a promise, so instead you’ll use the Protractor API methods for `element.all`.

```typescript
element(by.tagName('tbody')).all(by.tagName('tr'))
```

```typescript
// Listing 8.11 Filter for a contact—e2e/contact-list.e2e-spec.ts
import { browser, by, element } from 'protractor';

describe('the contact list', () => {
  it('with filter: should find existing ' +
     'contact "Craig Service"', () => {
    let tbody = element(by.tagName('tbody'));
 let trs = tbody.all(by.tagName('tr'));
    let craigService = trs.filter(elem => {
 return elem.all(by.tagName('td')).get(1).getText()
          .then(text => {
 return text === 'Craig Service';
      });
    });
 expect(craigService.count()).toBeGreaterThan(0);
    expect(craigService.all(by.tagName('td'))
 .get(2).getText())
        .toBe('craig.services@example.com');
  });
});
```

### 8.6.2 Mapping the contact list to an array

```typescript
// Listing 8.12 Checking that all the contacts appear as expected with map
import { browser, by, element } from 'protractor';
import { promise as wdpromise } from 'selenium-webdriver';

export interface Contact {
  name?: string;
  email?: string;
  tel?: string;
}

describe('the contact list', () => {
  let expectedContactList: Contact[] = [{
      name: 'Adrian Directive',
      email: 'adrian.directive@example.com',
      tel: '+1 (703) 555-0123'
    }, {
      name: 'Rusty Component',
      email: 'rusty.component@example.com',
      tel: '+1 (441) 555-0122'
    }, {
      name: 'Jeff Pipe',
      email: 'jeff.pipe@example.com',
      tel: '+1 (714) 555-0111'
    }, {
      name: 'Craig Service',
      email: 'craig.services@example.com',
      tel: '+1 (514) 555-0132'
  }];

  beforeAll(() => {
    browser.get('/#/');
  });

  it('with map: should create a map object', () => {
    let tbody = element(by.tagName('tbody'));
    let trs = tbody.all(by.tagName('tr'));
 let contactList = trs.map(elem => {
      let contact: Contact = {};
      let promises: any[] = [];
 let tds = element.all(by.tagName('td'));
 promises.push(tds.get(0).getText().then(text => {
        contact.name = text;
      }));
 promises.push(tds.get(1).getText().then(text => {
        contact.email = text;
      }));
 promises.push(tds.get(2).getText().then(text => {
        contact.tel = text;
      }));

 return Promise.all(promises).then(() => {
        return contact;
      });
    });
 expect(contactList).toBeDefined();
 contactList.then((contacts: Contact[]) => {
      expect(contacts.length).toEqual(4);
 expect(contacts).toEqual(expectedContactList);
    });
  });
});
```

### 8.6.3 Reduce

```typescript
// Listing 8.13 Reduce the list of elements to a single string
describe('the contact list', () => {
  beforeAll(() => {
    browser.get('/#/');
  });

  it('with reduce: get a list of contact names', () => {
    let tbody = element(by.tagName('tbody'));
 let trs = tbody.all(by.tagName('tr'));
 let contacts = trs.reduce((acc, curr) => {
 let name = curr.all(by.tagName('td')).get(0);
      return name.getText().then(text => {
 return acc + ', ' + text;
      });
    });
    expect(contactList).toEqual(
        'Adrian Directive, Rusty Component, Jeff Pipe, ' +
        'Craig Service');
  });
});
```

### 8.7 Page objects

```typescript
// Listing 8.14 Contact list page object—e2e/po/contact-list.po.ts
import { browser, by, element, ElementFinder } from 'protractor';

export class ContactListPageObject {
  plusButton: ElementFinder;

  constructor() {
 this.plusButton = element(by.id('add-contact'));
  }

  clickPlusButton() {
    this.plusButton.click();
 return new NewContactPageObject();
  }

  navigateTo() {
    browser.get('/#/');
  }
}
```

```typescript
// Listing 8.15 New contact page object—e2e/po/new-contact.po.ts
import { browser, by, element, ElementFinder } from 'protractor';

export class NewContactPageObject {
  inputName: ElementFinder;
  inputEmail: ElementFinder;
  inputPhone: ElementFinder;

  constructor() {
    this.inputName = element(by.id('contact-name')); 
    this.inputEmail = element(by.id('contact-email'));
    this.inputPhone = element(by.css('input[type="tel"]'));
  }

  setContactInfo(name: string, email: string,
      phoneNumber: string) {
 this.inputName.sendKeys(name);
 if (email) {
      this.inputEmail.sendKeys(email);
    }
 if (phoneNumber) {
      this.inputPhone.sendKeys(phoneNumber);
    }
  }

  clickCreateButton() {
    this.element(by.buttonText('Create')).click();
    return new ContactListPageObject();
  }

 getName() {
    return this.inputName.getAttribute('value');
  }
}
  getPhone() {
    return this.inputPhone.getAttribute('value');
}
  getEmail() {
    return this.inputEmail.getAttribute('value');
}
```

## Chapter 9 Understanding timeouts

### 9.3 Waiting with expected conditions

```typescript
let EC = browser.ExpectedConditions;
browser.wait(EC.visibilityOf($('.popup-title')), 2000,
  'Wait for popup title to be visible.');
```

```typescript
// Chained expected conditions
let EC = browser.ExpectedConditions;
let titleCondition = EC.and(EC.titleContains('foo'),
    EC.not(EC.titleContains('bar'));
browser.wait(titleCondition, 5000, 'Waiting for title to contain foo and not bar');
```

### 9.5 Using browser.wait

```typescript
// Listing 9.5 Using browser.wait with a custom condition
describe('feed dialog', () => {
  beforeEach(() => {
    browser.get('/contact/4');
  });

  it('should enable the follow button with more than two posts', () => {
    let feedButton = element(by.css('button.feed-button'));
    feedButton.click();

    let followButton = element(by.css('button.follow'))
 expect(followButton.isEnabled()).toBeFalsy();
    let moreThanOnePost = () => {
      return element.all(by.css('app-contact-feed mat-list-item')).count()
        .then((count) => {
 return count >= 2;
        })
    };
 browser.wait(moreThanOnePost, 20000, 'Waiting for two posts');

 expect(followButton.isEnabled()).toBeTruthy();
  });
});
```

## Chapter 10

### 10.2.1 Taking Screenshots

```typescript
browser.takeScreenshot()
```

```typescript
// Listing 10.9 test_screenshot/e2e/screenshot.e2e-spec.ts
describe('the contact list', () => {
  beforeAll(() => {
    browser.get('/');
 browser.driver.manage().window().setSize(1024,900);
  });

  it('should be able to login', (done) => {  
    const list = element(by.css('app-contact-list'));
 browser.waitForAngular();

    browser.takeScreenshot().then((data) => {
      fs.writeFileSync('screenshot.png', data, 'base64');
 done();
    })
  });
});
```

### 10.2.2 Taking screenshots on test failure

```config
plugins: [{
  path: './screenshot_on_failure_plugin.ts'
}],
```

```typescript
// Listing 10.10 test_screenshot/screenshot_on_failure_plugin.ts
import {browser} from 'protractor';
import * as fs from 'fs';

export function postTest(passed: boolean, testInfo: any) {
  if(!passed) {
 const fileName = `${testInfo.name.replace(/ /g, '_')}_failure.png`
    return browser.takeScreenshot().then((data) => {
 fs.writeFileSync(fileName, data, 'base64')
    });
  }
}
```

### 10.3.2 Highlight delay

Use `-highlightDelay` to tell Protractor to first highlight the text field with a blue rectangle and then wait the specified delay time.

### 10.4.2 The WebDriver control flow

```typescript
// Listing 10.16 Test using control flow
it('should open the dialog with waitForAngular', () => {
    let feedButton = element(by.css('button.feed-button'));
    let closeButton = element(by.css('button[mat-dialog-close]'));
    let dialogTitle = element(by.css('app-contact-feed h2.mat-dialog-title'));

 feedButton.click();
    expect(dialogTitle.getText())
        .toContain('Latest posts from Craig Service');
 debugger;

    closeButton.click();  
    browser.wait(EC.stalenessOf(dialogTitle), 3000, 
        'Waiting for dialog to close');
    expect(dialogTitle.isPresent()).toBeFalsy();
 });
```

> **Note:** These two tests do the same thing.

```typescript
// Listing 10.17 Explicitly using WebDriver promises
it('should open the dialog with waitForAngular', (done) => {
    let feedButton = element(by.css('button.feed-button'));
    let closeButton = element(by.css('button[mat-dialog-close]'));
    let dialogTitle = element(by.css('app-contact-feed h2.mat-dialog-title'));
    return feedButton.click().then(() => {  
      return dialogTitle.getText();  
    }).then((dialogText) => {
      expect(dialogText).toContain('Latest posts from Craig Service');
 debugger;
      return closeButton.click();
    }).then(() => {
      return browser.wait(EC.stalenessOf(dialogTitle), 3000,
          'Waiting for dialog to close');
    }).then(() => {
      return dialogTitle.isPresent();
    }).then((dialogTitleIsPresent) => {
      expect(dialogTitleIsPresent).toBeFalsy();
      done();
    });
```