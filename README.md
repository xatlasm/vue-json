# vue-json

## Project description

This is a rudimentary todo list app that I am making to learn JavaScript, Node, Vue.js, JSON, and Heroku.

It can be viewed online [here](https://vue-json.herokuapp.com/).

## Features

* Request saved lists (hosted at [MyJSON](https://myjson.com/)) using a provided key
* Add new items to list
* Checkboxes to visually track item state
* Clear delete individual items or entire list
* Save list at MyJSON with key provided for later retrieval

### To Do

* [ ] Save item checked state between sessions

* [ ] Replace/augment key system with local cookies for ease of use
* [ ] Improve appearance with CSS

## Local Install Instructions

0. Install [node.js](https://nodejs.org/en/)

1. Clone repository:

   ```shell
   git clone https://github.com/xatlasm/vue-json.git
   ```

2. Install dependencies:

   ```shell
   npm install
   ```

3. Run node server:

   ```shell
   npm run serve
   ```

4. Open browser to view app on http://localhost:8080/