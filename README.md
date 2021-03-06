# Rspec
## Rspec is a testing framework for Ruby

Writing code to test other code

"R" = Ruby
"Spec" = Specification

Spec: An executable example that tests whether a portion of code exhibits the expected behaviour in a controlled context

## What is Rspec?

* Given ome context
* When some event occurs
* Then I expect some outcome
* Given ... When ... Then ...
* Rspec is written is Ruby
* Uses a domain-specific language (DSL)
* Sometimes not very Ruby-like
* Learn Ruby first

## Rails

* Rails is most common use for Rspec
* Rails not required for Rspec
* First basic Ruby with Rspec

## Wht are software tests important?

### Reasons not to test:
- writing tests requires more time
- time is money

### Reasons to test:
- writing tests finds bugs
- simulates critical thinking
- covers edge cases (extremes)
- exposes poorly written code (code smells)
- confidence when refactoring/improving code
- confidence when adding features
- confidence when upgrading related software
- confidence during code deployment
- saves development time!
- saves headache
- helps to sleep at night :)

### Always test?
- small application may not need testing
- testing is more critical as complexity increases
- most developers start testing as they gain experience

## Thinking in User Stories
* Description of the experience of a user of your software
* Excellent planning tool
* Excellent communication tool with developers
* Excellent communication tool with clients
* Describes a single step in the user experience

### User Story #1
* Given that a user is not logged in
* When the user visits the login page
* Then the user should see form fields for username and password and a submit button

### User Story #2
* Given that a user is not logged in and is viewing the login form
* When the user enters a valid name and password and submits the form
* Then the site should redirect them to th approriate user page
(happy path)

### User Story #3
* Given that user is not logged in and is viewing the login form
* When the user enters a valid username and an invalid password and submits the form
* Then the site should return a not valid generic page and return the login page
(unhappy path)

## User Stories
* Defines feature scope and edge cases
* Defines perfectly-sozed portions of code for testing
* No "spaghetti code"
* 1 : 1 ration of story to spec

## Writing good tests
1. What to Test
  * You only have to test the parts that need to work - ha ha
  * How much test coverage we need
  * depends on complexity too
  * existing code: write test by priorities
  * Happy path => users get what they want
  * Unhappy path => when things dont work out and we need to handle it
  * Edge cases
  * Any bug that gets fixed

2. What not to Test
  * Basic Ruby
  * Basic Ruby on Rails
  * Third party APIs
  * Behaviour being tested already

## More advice
- A bad, partial or broken test can be worse than none
- Keep your test suite fast, you will run it more often
- Run tests often
- Every time you do a commit or push code
- Keep your test passing all the time
- Avoid writing brittle test

## Configuration
|Basic settings | You can set them|What it means|
|---------------|-----------------|-------------|
|"--no-color"| '--color'|The outcome is multicoloured or just one colour|
|'--format progress'| '--format documentation'| |
|'--no-profile'| '--profile'|Fastest and slowest test profile|
|'--no-fail-fast'| '--fail-fast'|whether Rspec runs all the tests and then reports all failures or as soon as they occur|
'--order defined| '--order random|the order that our tests are ran|


- Global: ~/.rspec
- Project: ./.rspec - overwrites the global configs
- Local: ./.rspec-local - not checked into source code managers, overwrites both above setting
- Command line (can be defined from)
- Inside Rspec code you can also specify these

### Basic syntaxt

```
describe "Car" do

# examples

end

```

```
describe "Car" do -> this a Ruby block that comes after it

  it "allows reading for :wheels" do
    #expectations
  end

end

```

```
describe "Car" do -> this a Ruby block that comes after it

  describe '.colors' do
  it "returns an array of color names" do
    c = ['blue', 'black', 'red', 'green']
    expect(Car.colors).to match_array(c)
  end

end

```

```
  expect(   ).to(  )
  expect(   ).not_to(  )

```

## Rspec Hierarchy

```
* spec file             car-spec.rb
  * example group         describe
    * nested group          describe/context
      * example               it
        * expectations          expect().to()
```

## What are test doubles?

* Are an object we use during testing, this stands in during testing, it is substituting the actual thing, like an actor for the actual actor.
* Like a placeholder.
* An object that stands in for another object
* Similar to a stand-in or boudy double for and actor/actress
* We dont always need the real object, we can create a stunt double for testing
* Various names: doubles, mocks, stubs, fakes, spies, dummies
* Not used consistently and sometimes they are described with slightly different behaviours
* Most commonly is doubles or mocks

### Why use them?

* When the real object is difficult to work with, or 'expensive'
* A simler version will serve our purpose just as well
* Responses are unpredictable
* Having fixed, expected responses makes testing easier

e.g. test for a method 'is_the_sun_up?' this returns true if the sun is up and false at nighttime
We dont want a test to fail if we wrote the method at daytime but it fails at nighttime. Instead we can create a double for the object that returns the current time so that it returns the responses we want. We can fake it as noon in one example and test that, and in another example we can double it again and make it midnight this time to test how it works there. => Our test will pas any time at the day but we can also test both scenarios.
Having an expected response for testing is better for our testing than having a real response.

* Examples: sending eamil, interacting with an API

### What do test doubles do?

* Set known return values
* Fake method implementations
* Set expectations about calls to an object

#### Definitions

1. Double/mock: a simple object preprogrammed with expectations and responses as preparation for the calls it will receive
2. Stub: an instruction to an object to return a specific response to a method call
3. Double and allow in Rspec 3

## Skipping and pending test
* Pending (still runs them and expects them to fail)
  * Omit the block
  * Use 'pending' inside the block (must be a failing test)
* Skipping
  * Use xdescribe or xit

## Fundamentals
### Expectation fundamentals
* In general, one expectation per example
* With more you will only see the first failure

```
expect().to()
expect.not_to()
@name = 'Kevin'
expect(@name).to eq('Kevin)
expect(@visible).to be(true)
expect(@numbers).to match_array([4,5,2,8])

expect(actual).to match(expected)
```
### Matcher
* Matchers are used as arguments to #to()
* Expectations are simple statements
* Matchers provide the variety and complexity
  * Equivalence matchers
  * Truthiness matchers
  * Numeric-comparison matchers
  * Collection matchers
  * Observation matchers

### Deprecated Modifier: should
- Outdated matcher, it was present in Rspec 2
- @count.should eq(3) (problem! count can be anything!)
"Count could be an array, a string, another kind of object that we've defined, and "should" has to be a method available for all of those kinds of objects. We have to make it globally available on every single object that could possibly come up."
- Required adding #should to every Ruby object
- Global 'monkey patching' = bad practice
- should syntax is still available - will give you warnings
- Use #expect exclusively
- Revise old code to use #expect

### Examples with 'should'
- it 'should return an array of colour names' (better: it 'returns an array of color names')
- it 'should allow reading and writing from :make' (better: it 'allows reading and writing for :make')
- it should do something vs it does something, avoid using it!!

## Equivalence Matchers

```
x = 1
x == 1    #true
x == 1.0  #true
x == "1"  #false

x.eql?(1) #true -this is value equality
x.eql?(1.0) #false (it is a float)
x.eql?('1') #false

x = 'Lynda'
x == 'Lynda' #true   - loose eq
x.eql?('Lynda') #true - value eq
x.equal?('Lynda') #false - identity eq

expect(x).to eq(1)  - we want this most of the time!
expect(x).to be == 1
expect(x).to eql(1)  - stricter
expect(x).to equal(1)  - very strict, rare
```

## Truthiness Matchers
- We expect something to be true

```
expect( 1 < 2).to be true
expect(1 > 2).to be false

expect(nil).to be_nil - no variation here, nil can only be nil
```

## Numeric comparison matchers
- We want to write expectation which compare numeric values

```
expect(100).to eq(100)
expect(100).to be == 100   #less common
expect(100).to be > 99 etc.
expect(5).to be_between(3, 5).inclusive
expect(5).not_to be_between(3, 5).exclusive
expect(100).to be_within(5).of(105)
expect(1..10).to cover(3)

```

## Collection Matchers
- arrays
- hashes
- strings

```
array = [1,2,3]
expect(array).to include(3)
expect(array).to include(2,3)
expect(array).to start_with(1)
expect(array).to end_with(3)

expect(array).to match_array([3,2,1])
expect(array).not_to contain_exactly(3,2,1)

string = 'Lynda'

expect(string).to include('Ly') etc. similar to arrays

hash = {:city => 'Dallas', :state => 'TX'}
expect(hash).to include(:city)
expect(hash).to include(:city, :state)
expect(hash).to include(:city => 'Dallas')

```

## Other matchers
- matchers for regex
  - match a string using regex
  - only with strings!!
- object type matchers
  - object is an instance of a class?

```
expect(@bob).to be_instance_of(Subscriber)
expect(@bob).to be_an_instance_of(Subscriber)
expect(@bob).to be_a_kind_of(Customer)
expect(@bob).to be_a(Customer)
expect([1,2,3]).to be_an(Array)
```
- respond to matcher
```
expect(@bob).to respond_to(:first_name) #method
```
- attribute matcher
- satisfy matcher (it takes a block) #last resort!!

## Predicate matchers
- are dinamically defined, not built in
- useful with custom methods
- hash.has_key?
- hash.has_value?

## Observation matchers
- allow us to create expectation about how things change
- objects, values, error, output
- expect {}.to ()

```
array = []
expect { array << 1 }.to change(array, :empty?).from(true).to(false)

```
Calls ```:empty?``` before and after the block

```
expect do
  bob.first_name = 'Robert'
  bob.last_name = 'Smith'
  end.to change(bob, :full_name).from('Bob Smith').to('Robert Smith')
```
```
x = 10
expect { x += 1 }.to change{x}.from(10).to(11)
expect { x += 1 }.to change { x  % 3 }.from(2).to(0)
expect { x += 1 }.to change {x}.by(1)
```

## Observer Errors
```
expect { customer.delete }.to raise_error
expect { customer.delete }.to raise_exception
expect { 1/0 }.to raise_error(ZeroDivisionError)
expect { 1/0 }.to raise_error.with_message('divided by 0')
```

## Observer Output
```
expect {print 'hello'}.to output.to_stdout
expect {print 'hello' }.to output('hello').to_stdout
```

## Compound Expectations

- to use and & or when doing expectations

```
s = 'Lynda'
expect(s).to start_with('L').and end_with('a')
expect(s.length).to be_even.or be < 6
expect(s).to start_with('L') & end_with('a')
expect(s.length).to be_even | be < 6
```

## Composing Matcher
- more complex
- new in Rspec 3
- some matchers can accept other matchers as their argument

```
array = [1,2,3]
expect(array).to all( be < 5 )
expect(@item).to all(be_visible & be_in_stock)
```
### Even more:

- all(matcher)
- include(matcher)
- start_with(matcher)
- end_with(matcher)
- change { }.from(matcher).to(matcher)
- change { }.by(matcher)
- raise_error.with_message(matcher)
