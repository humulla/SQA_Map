# SQA_Example

Product Details: 
A fitness product that allows you to set a route on Google Maps. It then generates a video that will play through, depending on how far you move or cycle in a physical space.

## Frontend Stack

## Backend Stack

## Testing Frameworks

## Continious Integration: Github actions
This was chosen due to the tight integration with Github. On changes to the repo, be it raising a PR or merging to the main branch, we can run our unit tests to check for regression. Unlike other CI providers such as TravisCi, Github Actions is free to use - this allows us to run extensive testing suites without spending a dime. 

We can also get a badge for a successful action that can be displayed in the readme or on other sites.

Below is an example of a possible combined test and deployment script.
The action will be run on a push to the repo and on a raised pull request.
The action will run through all the available jobs in sequential order. 
Under the `deploy` job the `needs` statement allows us to define prerequisites that need to pass before this job can run. Therefore in the below code, the `test` job needs to have completed successfully before running the `deploy` phase.

```ruby
name: CI Tests & Deploy

on:
  [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - name: npm install and test
      run: |
        npm install
        npm test
      env:
        CI: true

  deploy:
    needs: [test]
    runs-on: ubuntu-latest

    steps:
        //Run some sort of deployment intergration here
```


## Brief:
Choose a role for each team member. 
The role each person has gives them the final word on stack items related to their role. (A Developer will make a final choice between Node and Java on the backend but everyone’s ideas are welcome).

Discuss as a group what STACK you would like to use.
Example:
Node on the backend
React on the frontend
React Native for the mobile apps
Jest and React Testing Library for testing
Postgres for database
github and git for version control and collaboration
Github actions for continuous integration
Netlify to deploy front
Heroku to deploy back
Storybook for component testing
etc.

Justify your stack in your presentation or in the README of your github repo

Define some of the process, you can even start the project set up or write some initial code and tests that you can demonstrate to show code review and test settings. Linter rules etc.

Set it up and/or describe as if it was a real project but we won't build it fully, we will just discuss how SQA fits into the overall project building scheme
