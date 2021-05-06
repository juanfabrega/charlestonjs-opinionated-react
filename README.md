---
theme: gaia
_class: lead
paginate: true
marp: true
class: invert
---

# **Opinionated React**
Avoiding the giant SPA-ghetti monster.

---

# About Me

![h:100](https://media-exp1.licdn.com/dms/image/C4E03AQFIb2XR-CZMEg/profile-displayphoto-shrink_400_400/0/1570579524994?e=1625702400&v=beta&t=ULoproPr6C19LUnG2K8nH2ee1OmQ8KBCCh1Hudpmb60)

Juan Fabrega

Software Engineer @ [Palmetto Solar](https://palmetto.com/)

Some things I've worked on:
[Palmetto Component Library](https://ux.palmetto.com/) - *Core Maintainer 2020 - present*
[Rhinostyle Component Library](https://github.com/rhinogram/rhinostyle) - *Core Maintainer 2018 - 2020*

---

# Why
Everything is UX.

![bg right h:500](https://images-na.ssl-images-amazon.com/images/I/41MdP5Tn0wL._SX387_BO1,204,203,200_.jpg)

"It doesn't matter how many times I have to click, as long as each  click is a mindless, unambiguous choice"

---

# Our Goal
Should not be to eliminate thought altogether, but limit time spent on inconsequential thought.

* Which directory does this file belong in? ❌
* Does this data belong in our global store ❌
* Should I create a CSS class or just inline styles? ❌

* Am I testing all possible scenarios correctly for this feature? ✅
* Does this solution provide the best user experience? ✅

---

# Relevance to React

React is an unopinionated framework (ahem, library!)

| Pattern      | Vue         | React
| -----------  | ----------- | -----------
| Routing      | Vue Router  | React Router, React Router 🔫
| Global State | Vuex        | Redux, Mobx, Recoil
| Components   | SFC         | Functional, Class Components
| Local State  | magic       | hooks, setState
| Scoped Styles| OTB Scoping | CSS modules, styled components

---

# Where to start?

**PRE-REQUISITE:** Get management/product buy-in.

1. Is this a brand new codebase?
2. Is it an existing codebase with competing patterns and lacking consistency.
3. Is it an existing codebase which is well architected and consistent?

Doesn't matter. The answer is the same: **BDFL**

---

# BDFL(s)
BDFL: Benevolent Dictator ~~for Life~~


<img align="right" width="400" height="auto" src="https://upload.wikimedia.org/wikipedia/commons/e/e2/Guido-portrait-2014-drc.jpg">

- Evaluates team needs.
- Considers input from team members.
- Makes and enforces unilateral decisions.

Does NOT have to be just one person, but it should not be the entire team. Elect a BDFL democratically but let them rule thereafter.

---

# Process
The **architecture meeting:**

- Identify problem areas
- Identify novel needs
- Solicit team feedback
- Evaluate options
- Make decisions
- Insert work into upcoming sprints(s)!

---

# Docs
Your `README.md` should be more than just basic commands to run the project, ideally you'd include a guide for contributors which will include:

* Core principles
* Core libraries (dependencies) in use.
* Low-level style guide for the most common uses, E.G: file structure, testing, JSX formatting, style implementation, etc.

[EXAMPLE](https://github.com/palmetto/palmetto-components/blob/main/docs/CONTRIBUTING.md)

---

# Culture
Team needs to understand the added value of good codebase UX, so they can themselves help maintain it.

* Code reviews on PRs should include style review, but not based on the reviewers opinion, (see previous slide).
* If BDFL is responsible for reviewing all code, something has gone terribly wrong.


---

# Our Guiding Light
How to make decisions about your tech stack:

1. Pick something and **STICK WITH IT!**
2. Be moderately boring.

---

<!-- _class: lead -->
# **Opinions**
![opinion](https://media4.giphy.com/media/MPuTZQqOmYKPK/giphy.gif?cid=ecf05e47iyb644d3s9bldfanafkskd2vhp0wlcdhfh6atrdr&rid=giphy.gif&ct=g)

---

# Component Types
Classes or functions?

```
export const App = () => (
  <h1>
    I win!
  </h1>
);
```

* Most react developer mindshare is invested in functional components.
* Hooks are old enough to be trusted for __almost__ anything.

---

# Directory Structure
Don't overthink it!

[Read this](https://reactjs.org/docs/faq-structure.html), pick one, and **STICK WITH IT**.

* I'm not a fan of atomic design. 👎
* I like component subfolders. 👍
* I do not like more than one layer of nesting beyond a component subfolder. 👎
* I like views and components separated. 👍

---

# Linting
* Use [AirBnB Eslint Config](https://github.com/airbnb/javascript) and call it a day.

![time bg:right h:200](https://media4.giphy.com/media/10PcMWwtZSYk2k/giphy.gif?cid=ecf05e47rpd0vn9cs0fj7dmqpyf0tl73dm4fjskrz026njfx&rid=giphy.gif&ct=g)

---

# Testing
* **Basic component functionality**: [jest](https://github.com/facebook/jest) + [react-testing-library](https://testing-library.com/docs/react-testing-library/intro/)
* **Visual tests**: [Storybook](https://storybook.js.org/docs/react/get-started/introduction) + [chromatic](https://www.chromatic.com/)
* **Integration/e2e**: I can't recommend specific integration/e2e testing options because these are highly context-dependent.

---

# Routing
Use [React Router](https://reactrouter.com/) and call it a day. 

![time bg:right h:200](https://media4.giphy.com/media/10PcMWwtZSYk2k/giphy.gif?cid=ecf05e47rpd0vn9cs0fj7dmqpyf0tl73dm4fjskrz026njfx&rid=giphy.gif&ct=g)

* If posible avoid too many individual route files. Routing is a great way to give a dev a bird's eye view of an application without too much markup clutter.

---

# Global State Management
Decide WHY you need it and that should inform how it gets used. 

* If you're not sure why you need it, you don't need it.
* If you don't know what to pick, pick [Redux](https://react-redux.js.org/), and [**use redux toolkit!**](https://redux-toolkit.js.org/)

---

# Global State Management - Part 2
If you have lots of nested data structures, [Normalize it!](https://redux.js.org/recipes/structuring-reducers/normalizing-state-shape)

![normalize](https://i.imgflip.com/58jrga.jpg)

---

# Styles

* If your team writes CSS/SASS, stick to CSS/SASS (and adopt something like [BEM](http://getbem.com/)).
* If your team's CSS skill set is lacking, See next slide.

---

# Styles - Part 2
Do I need a library?

* If you don't need custom components and prefer semantic markup, use [TailwindCSS](https://tailwindcss.com/).
* If you prefer custom components, pick any of the top players and theme it as needed.

* **Don't create your own component library.**

---

# Styles - Part 3
What about styled components or css-in-js?

* Use it only if you have a LOT of confidence in your ability to architect this approach consistently across teams.

What about CSS modules?
* They are used as a crutch to avoid thinking about CSS architecture.

---
# Forms
* You probably want to use [Formik](https://formik.org/)
* Personally I've rolled my own form abstractions, but this is not the right approach for everyone.

---

# Data Fetching
* Whatever you go with, abstract it into a service, don't have devs type up request URLs in their components please!
* Try [React Query](https://react-query.tanstack.com/)

![fetch](https://media0.giphy.com/media/5G98t8QjqBLK8/giphy.gif?cid=ecf05e47irwt64znjvfuef052x85wt96bqdl6siuqajjifdw&rid=giphy.gif&ct=g)

---

<!-- _class: lead -->
# **Thank you!**
![opinion](https://media2.giphy.com/media/5xtDarmwsuR9sDRObyU/giphy.gif?cid=ecf05e47mu3qi437injy9ufzrvlvziwj1rcae101em0erzxq&rid=giphy.gif&ct=g)