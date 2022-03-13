# Jasmine Testing Intro

Jasmine is a behaviour-driven development framework for testing JS code. It does not depend on any other JS framework.

Testing is done in 3 parts: grouping, a test case, and our expectation.

```js
// grouping
describe('Test Example', () => {
    // test case
    it('returns true', () => {
        // expectation
        expect(false).toBe(true); 
    });
});
```

`Describe()` takes two parameters: the name of the testing function, and its body. The name can be anything we want and we can use string interpolation to make sure it matches a component in the program. Multiple describes can be nested to group test cases.

`BeforeEach()` will run code before each test after it. It can be nested within any `describe()`

An `f` can be placed on any method such as `fit` and `fdescribe` to make Jasmine focus and only execute that test. An `x` can also be placed to skip certain tests.

Spies are used to check on dependencies such as APIs without calling them directly.

API calls are usually mocked. A mock can be created from scratch and is more reusable than spies.

Matches make comparisons and are chain after `expect()`.

* `toBe()` checks that something is equivalent, as in strictly equal, to the parameter.
* `toEqual()` does a deep comparison between elements.
* `toBeDefined()` checks that something exists.

## Test suite example with all of the above

User class:

```js
class User {
    firstName;
    lastName;
    middleName;
    id;
    userService;
    
    constructor(data, userService){
        this.firstName = data.firstName || '';
        this.lastName = data.lastName || '';
        this.middleName = data.middleName || '';
        this.id = data.id;
        this.userService = userService;
    }
        
    get fullName() {
        if(this.middleName.length > 0) {
            return `${this.firstName} ${this.middleName[0]}. ${this.lastName}`;
        }
        
        return `${this.firstName} ${this.lastName}`;
    }
    
    async getMyFullUserData() {
        return this.userService.getUserById(this.id);
    }
    
    sayMyName() {
        alert(this.fullName);
    }
    
    getCodeName() {
        const isATestingGod = confirm('Are you a testing god?');
        
        if(isATestingGod) {
            return 'TESTING GOD!'
        } else {
            return `Scrub skipping tests in his best friend's ride!`;
        }
    }
} 
 
```

API call:

```js
class UserService {
    getUserById(id) {
        return fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
    }
}
```

Test suite:

```js
describe(`${User.name} Class`, () => {
    let model;
        let mockUserService;
    
    beforeEach(() => {
        mockUserService = {
            lastId: null,
            user: {},
            getUserById(id) {
                this.lastId = id;
                
                return this.user;
            }
        };
        const data = { firstName: 'Dylan', middleName: 'Christopher', lastName: 'Israel', id: 1 };
        model = new User(data, mockUserService);
    });

    beforeEach(() => {
        model = new User();
    });
    
    describe('default values', () => {
        it('first name defaults to empty', () => {
            // assert
            expect(model.firstName).toBe('');
        });
    
        it('last name defaults to empty', () => {
            // assert
            expect(model.lastName).toBe('');
        });
    
        it('middle name defaults to empty', () => {
            // assert
            expect(model.middleName).toBe('');
        }); 
    });

    describe('full name', () => {
        beforeEach(() => {
            model = new User({ firstName: 'Dylan', lastName: 'Israel' }); 
        });
        
        it('middle initial when middleName is defined with first and last', () => {
            // arrange
            model.middleName = 'Christopher';
            
            // act
            const result = model.fullName;
            
            // assert
            expect(result).toBe(`${model.firstName} ${model.middleName[0]}. ${model.lastName}`);
        });
       
        it('when no middle name return just first and last', () => {
            // arrange
           model.middleName = '';
           
           // act
           const result = model.fullName;
           
           // assert
           expect(result).toBe(`${model.firstName} ${model.lastName}`);
        });
    });

    // spies the window API object for the alert method and expects it to have been called with that name
    describe('say my name', () => {
        it('alerts the full name of user', () => {
            // arrange
            model.firstName = "Dylan";
            model.lastName = "Israel";
            spyOn(window, 'alert');
            
            // act
            model.sayMyName();
            
            // assert
            expect(window.alert).toHaveBeenCalledWith('Dylan Israel');
        });
    });
    
    // mock checking on API call
    describe('getMyFullUserData', () => {
        it('gets user data by id', async () => {
            // arrange
            mockUserService.lastId = null;
            mockUserService.user = new User(
                {firstName: 'Dollan', middleName: 'Coding God', lastName: 'Noneya', id: 2 }
                )
            // act
            const result = await model.getMyFullUserData();
            
            // assert
            expect(mockUserService.lastId).toBe(1);
        });
    });
});
```
