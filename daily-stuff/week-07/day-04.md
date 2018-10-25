# Day 04

What we covered today:

* Flickr Solution
* Transpiling Intro
* Ajax-on-rails with frontend
* Frontend Frameworks:
  * Vue.js - intro
* Guest Speaker: Charlie Gerard - [Programming for Hardware in JavaScript & IoT](https://docs.google.com/presentation/d/1VdH-Ry2tp0dEWCBLFis9djfMRmi-nmUfE22fof7W3P0/edit?usp=sharing)

### Warmup <a id="warmup"></a>

* [​Space Age​](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week07/day04_space_age)

## Codealong <a id="codealong"></a>

* ​[Flickr Search Solution](https://github.com/textchimp/wdi-29/tree/master/week7/flickr-search-spa)
* [Babel Flickr Search](https://github.com/textchimp/wdi-29/tree/master/week7/babel-flickr-search)
* [Rails-dogs-frontend](https://github.com/textchimp/wdi-29/tree/master/week7/rails-dogs-frontend)
* [Ajax-on-rails \(updated\)](https://github.com/textchimp/wdi-29/tree/master/week7/ajax-on-rails)
* ​[Vue Reintro​](https://github.com/textchimp/wdi-29/tree/master/week7/vue-reintro)

## Transpilation Intro <a id="transpilation-intro"></a>

* ​[Babeljs.io](https://babeljs.io/)​
* ​[Babel language pluggin - ATOM](https://atom.io/packages/language-babel)​

#### Set up npm in your project <a id="set-up-npm-in-your-project"></a>

```bash
npm init -y
```

#### Install babel-cli and babel-env <a id="install-babel-cli-and-babel-env"></a>

```bash
npm install --save-dev babel-cli babel-env
```

Note the .babelrc file is created for you.

#### Create a .gitignore so you don't commit your 34 MB node\_modules folder <a id="create-a-gitignore-so-you-dont-commit-your-34-mb-node_modules-folder"></a>

```bash
echo "node_modules/" >> .gitignore
```

#### Add a script to build your project \(in package.json\) <a id="add-a-script-to-build-your-project-in-package-json"></a>

```javascript
"scripts": {  
  "build": "babel src -d js",  
  "watch": "babel --watch src -d js"
},
```

#### Ensure your es6 code is in a `src` directory <a id="ensure-your-es6-code-is-in-a-src-directory"></a>

#### Build! <a id="build"></a>

```bash
npm run build
```

and

```bash
npm run watch
```



## Vue <a id="vue"></a>

#### What is it? <a id="what-is-it"></a>

Vue \(pronounced /vjuː/, like view\) is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable.

The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with modern tooling and supporting libraries.

#### Lets get started <a id="lets-get-started"></a>

Add vue to your js folder:

```bash
  project$ wget unpkg.com/vue -O js/vue.js
```

#### Docs: <a id="docs"></a>

The Vue documentation is really easy to follow. I'm not going to waste everyone's time regurgitating it, so go to the [source](https://vuejs.org/v2/guide/#Getting-Started)!

### Homework <a id="homework"></a>

Pick whichever combination of these tasks would be most helpful to your understanding:

* _Flickr search_: add next/previous to the fullscreen slideshow; make another Flickr API request to the slideshow so you can display more information about each image \(link to user page, link to Flickr page for the photo, tags for the photo\); add geolocation-based search option!
* _Rails Dogs AJAX frontend_: add an edit link to each dog in the list; clicking the link causes an edit form \(prefilled with that dog's info\) to appear, and submit the data to the Rails update route, saving it to the DB
* finish the API frontend homework from Tuesday \(pick an API, make a search form, search results & details page for it\); or pick a new API and make a new AJAX frontend for it

