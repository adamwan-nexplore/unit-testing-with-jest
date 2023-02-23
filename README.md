# Refactor the code a bit & Write some good unit tests

## Terms 

SUT - Subject Under Test

Unit test - usually we are verifying the output of a function 

Entry Point - The input of the test

Exit Point - the effect after applying the data to the SUT

---
## `Write more pure functions`

a. pure functions

    -> return value / error (the most easiest to notice

b. impure functions

    -> change in global state (need to check the implementation to find out the state) -> by stricter scoping

    -> call third party dependencies (very hard to observe)


## Rephrase the statment 

We should reduce the number of impure functions. We should group those together, or at least in a managed way.

Do not dream of eliminate those entirely. We need to store something bu the use of impure functions.

---

Unit tests

-> should test one exit point per test case

-> if it is not fast enough or those parts require extra setup. those should not be regarded as unit tests

<img width="421" alt="Screenshot 2023-02-15 at 5 10 53 PM" src="https://user-images.githubusercontent.com/124669872/218983743-03556412-f4b3-4386-9bea-4908c7fed7d5.png">

---

What we prefer to have test case files - the filename ending with `.spec.ts`

Plugin Recommended for VSCode: `Jest Runner` - it will run the spec files immediately when you save the `.spec.ts` file.

Function recommended to use `toMatchInlineSnapshot()` will store and write down the result of first one. (similar one is `toMatchSnapshot()`)

https://jestjs.io/docs/snapshot-testing

---

U.S.E. Naming to describe the test

- Describing the unit (filename + function name)

- Situation (the input you are going for)

- Expectation (expected observed change to be)

e.g.
```
// describe file
describe('@password.ts', () => {

  // describe function
  describe('#verifyPassword', () => {

    // describe condition
    describe('given a failing rule', () => {
    
      // mark expected output ONLY
      it('returns errors', () => {
        const fakeRule = input => ({ passed: false, reason: ‘fake reason’ });
        const errors = verifyPassword('any value', [fakeRule]);
        expect(errors[0]).toContain('fake reason');
      });
    });
  });
});
```

### scroll fatigue
You might consider not to use `beforeEach` function, as reader needs to scroll up a lot to understand the set up. Instead, to be more intuitively, consider creating a setup function with a proper name for readability.

### testing an error throw
```
test('verify, with no rules, throws exception', () => {
  const verifier = makeVerifier();
  expect(() => verifier
              .verify('any input'))
              .toThrowError(/no rules configured/);
});
```

Nock Recording (Setting the real secret to run aginst the apis, and then capture the response for mock testing)
https://github.com/nock/nock#recording

### Functional approaches

    - Function as Parameter

    - Factory Functions (a.k.a Higher Order Functions )

    - Constructor Functions

### Object Oriented Approaches

    - Class Constructor Injection

    - Object as Parameter (a.k.a ‘duck typing’)

    - Common Interface as Parameter (for this we’ll use TypeScript)”


### Pay extra attention to the terms of mocking the implementation
<img width="1423" alt="Screenshot 2023-02-21 at 9 01 44 AM" src="https://user-images.githubusercontent.com/124669872/220221954-0ca65661-4822-4884-bbfb-517c43a35cb6.png">



Reference
- [The Art of Unit Testing - 3rd Edition (In Javascript)](https://www.manning.com/books/the-art-of-unit-testing-third-edition)
- Refactoring: Improving the Design of Existing Code - 2nd Edition (In Javascript)
- [Xunit Patterns.com](http://xunitpatterns.com/Mocks,%20Fakes,%20Stubs%20and%20Dummies.html)

- Change something