# React + TypeScript for High School Students: Components, State, and Hooks

> **Level:** Beginner  
> **Tools:** React, TypeScript, TSX, Vite, and a web browser  
> **Goal:** Learn how React and TypeScript work together, compare class and functional components, understand `useState` and other hooks, and build a type-safe Study Planner app.

React is a JavaScript library for building interactive user interfaces. We will write the application in **TypeScript**, which adds type checking to JavaScript. It is used for websites, dashboards, games, and mobile apps. Instead of writing one giant page, React lets us build small, reusable pieces called **components**.

This guide is divided into mini-tutorials. You can complete one mini-tutorial at a time, but they connect to form one complete learning path.

---

## Table of Contents

1. [How to Use This Tutorial](#1-how-to-use-this-tutorial)
2. [What Is React?](#2-what-is-react)
3. [Set Up a React Project](#3-set-up-a-react-project)
4. [Understand the Project Files](#4-understand-the-project-files)
5. [Tutorial 1: TSX](#5-tutorial-1-tsx)
6. [Tutorial 2: Functional Components](#6-tutorial-2-functional-components)
7. [Tutorial 3: Props](#7-tutorial-3-props)
8. [Tutorial 4: Events](#8-tutorial-4-events)
9. [Tutorial 5: State and `useState`](#9-tutorial-5-state-and-usestate)
10. [Tutorial 6: Conditional Rendering](#10-tutorial-6-conditional-rendering)
11. [Tutorial 7: Lists and Keys](#11-tutorial-7-lists-and-keys)
12. [Tutorial 8: Forms](#12-tutorial-8-forms)
13. [Tutorial 9: Class Components](#13-tutorial-9-class-components)
14. [Tutorial 10: `useEffect`](#14-tutorial-10-useeffect)
15. [Tutorial 11: `useRef`](#15-tutorial-11-useref)
16. [Tutorial 12: `useContext`](#16-tutorial-12-usecontext)
17. [Tutorial 13: `useReducer`](#17-tutorial-13-usereducer)
18. [Tutorial 14: `useMemo` and `useCallback`](#18-tutorial-14-usememo-and-usecallback)
19. [Tutorial 15: Custom Hooks](#19-tutorial-15-custom-hooks)
20. [Rules of Hooks](#20-rules-of-hooks)
21. [Final Project: Study Planner](#21-final-project-study-planner)
22. [Testing and Debugging](#22-testing-and-debugging)
23. [Accessibility Basics](#23-accessibility-basics)
24. [Common Mistakes](#24-common-mistakes)
25. [Practice Challenges](#25-practice-challenges)
26. [React Cheatsheet](#26-react-cheatsheet)
27. [Glossary](#27-glossary)
28. [What to Learn Next](#28-what-to-learn-next)

---

# 1. How to Use This Tutorial

For each mini-tutorial:

1. Read the explanation.
2. Type the example instead of copying it.
3. Predict what will happen before running it.
4. Change one value and observe the result.
5. Complete the checkpoint.

You do not need to memorize every line. Focus on understanding these questions:

- What information does this component receive?
- What information does it remember?
- What causes it to update?
- What does it display?

## Learning objectives

By the end, you will be able to:

- explain React using simple language;
- create types and interfaces for application data;
- create functional and class components;
- pass data with props;
- respond to clicks and form input;
- manage changing data with `useState`;
- run side effects with `useEffect`;
- use `useRef`, `useContext`, and `useReducer`;
- explain when `useMemo` and `useCallback` may help;
- create a custom hook;
- build a complete React application.

---

# 2. What Is React?

Imagine building a school website from LEGO bricks. A navigation bar is one brick, a student card is another, and a calendar is another. React components work like those LEGO bricks.

```text
Application
├── Header
├── AssignmentForm
├── AssignmentList
│   ├── AssignmentCard
│   ├── AssignmentCard
│   └── AssignmentCard
└── Footer
```

Each component can have:

- **props:** information given to it by a parent;
- **state:** information it remembers and can change;
- **events:** actions such as clicking or typing;
- **UI:** the elements it displays.

## React updates the screen

In older JavaScript code, a programmer often finds an HTML element and changes it manually:

```ts
document.querySelector("#score")!.textContent = String(score);
```

In React, we describe what the screen should look like for the current data:

```tsx
<p>Score: {score}</p>
```

When `score` changes, React updates the necessary part of the page.

## React is declarative

**Imperative** code gives detailed instructions:

> Find the paragraph, erase its text, calculate the new score, and insert the new text.

**Declarative** code describes the result:

> The paragraph should display the current score.

React is mainly declarative.

## The component tree

React applications form a tree. A component can render child components, and those children can render more children.

```text
App
├── Header
├── Main
│   ├── SearchBar
│   └── Results
└── Footer
```

Data normally travels **down** the tree through props. Child components can ask parents to make changes by calling callback functions passed as props.

## Checkpoint

Explain React to a classmate without using the word "React." A good answer might be:

> It is a tool that builds a page from reusable pieces and updates the page when its data changes.

---

# 3. Set Up a React Project

## What you need

Install:

- a recent LTS version of [Node.js](https://nodejs.org/);
- a code editor such as Visual Studio Code;
- a modern browser such as Chrome, Edge, or Firefox.

Node.js includes **npm**, a tool that downloads packages and runs project commands.

Check the installations in a terminal:

```bash
node --version
npm --version
```

## Create the project with Vite

Run:

```bash
npm create vite@latest react-study-planner -- --template react-ts
cd react-study-planner
npm install
npm run dev
```

The terminal displays a local address, usually:

```text
http://localhost:5173
```

Open that address in your browser.

> Keep the terminal running while you work. Press `Ctrl+C` when you want to stop the development server.

## Why Vite?

Vite is a development tool. It:

- creates the starter project;
- starts a local development server;
- refreshes the browser after saved changes;
- prepares optimized files for publishing.

## Useful commands

| Command | Purpose |
|---|---|
| `npm install` | Download the project's packages |
| `npm run dev` | Start the development server |
| `npm run build` | Create a production build |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Check common code-quality problems |

---

# 4. Understand the Project Files

A new Vite project contains files similar to these:

```text
react-study-planner/
├── public/
├── src/
│   ├── assets/
│   ├── App.css
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
├── eslint.config.js
├── index.html
├── package.json
└── vite.config.ts
```

## Important files

### `index.html`

This is the main HTML page. It contains the element where React places the application:

```html
<div id="root"></div>
```

### `src/main.tsx`

This starts React:

```tsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.tsx";
import "./index.css";

createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

TypeScript understands that `getElementById` might return `null`. The Vite starter uses a non-null assertion because the project controls `index.html` and knows that `#root` exists:

```tsx
createRoot(document.getElementById("root")!).render(<App />);
```

The `!` means, "We know this value is not `null` here." Use it only when you can prove that statement.

`<StrictMode>` helps find mistakes during development. In development, it may run some logic more than once to reveal unsafe code. It does not do this in the production build.

### `src/App.tsx`

This is the starter application component. Most early examples in this guide go here.

### `package.json`

This records project scripts and installed packages. Do not edit it randomly.

## Clean the starter

Replace `src/App.tsx` with:

```tsx
import "./App.css";

function App() {
  return (
    <main>
      <h1>React Study Planner</h1>
      <p>My first React application</p>
    </main>
  );
}

export default App;
```

Replace `src/App.css` with:

```css
#root {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem;
}
```

You now have a clean starting point.

---

# 5. Tutorial 1: TSX

JSX is a syntax that lets us write HTML-like code inside JavaScript. A `.tsx` file combines JSX with TypeScript, so this tutorial will call it **TSX**.

```tsx
const heading = <h1>Study Planner</h1>;
```

The browser does not directly understand TypeScript or TSX. Vite transforms the code into JavaScript.

## TypeScript in five minutes

TypeScript lets us describe what kind of value a variable may contain:

```ts
const studentName: string = "Maya";
const grade: number = 10;
const isEnrolled: boolean = true;
const subjects: string[] = ["Math", "Art"];
```

TypeScript reports an error before the app runs if a value has the wrong type:

```ts
let score: number = 10;
score = "ten"; // Error: a string cannot be assigned to a number.
```

Usually, TypeScript can **infer** a type from the starting value:

```ts
const schoolName = "Lincoln High"; // TypeScript infers string.
const assignmentCount = 4; // TypeScript infers number.
```

Use an `interface` to describe an object:

```ts
interface Student {
  id: string;
  name: string;
  grade: number;
}

const student: Student = {
  id: "student-1",
  name: "Maya",
  grade: 10,
};
```

A union type limits a value to specific choices:

```ts
type SchoolDay = "Monday" | "Tuesday" | "Wednesday" | "Thursday" | "Friday";

const testDay: SchoolDay = "Friday";
```

Types do not change what the browser does. They help your editor and the TypeScript compiler catch mistakes while you build.

## Put JavaScript expressions inside TSX

Use curly braces for JavaScript expressions:

```tsx
function App() {
  const studentName = "Maya";
  const assignmentCount = 4;

  return (
    <main>
      <h1>Welcome, {studentName}!</h1>
      <p>You have {assignmentCount} assignments.</p>
      <p>Tomorrow you will have {assignmentCount - 1}.</p>
    </main>
  );
}
```

An **expression** produces a value. Variables, calculations, and function calls can be expressions.

This does not work directly inside JSX because `if` is a statement:

```tsx
<p>{if (ready) "Ready"}</p>
```

We will learn valid conditional rendering later.

## JSX rules

### Rule 1: Return one parent element

This is invalid:

```tsx
return (
  <h1>Planner</h1>
  <p>Welcome!</p>
);
```

Wrap the elements:

```tsx
return (
  <main>
    <h1>Planner</h1>
    <p>Welcome!</p>
  </main>
);
```

If you do not need an extra HTML element, use a **fragment**:

```tsx
return (
  <>
    <h1>Planner</h1>
    <p>Welcome!</p>
  </>
);
```

### Rule 2: Close every tag

```tsx
<img src="/book.png" alt="A stack of books" />
<input type="text" />
```

### Rule 3: Use `className`

JavaScript already uses the word `class`, so JSX uses `className`:

```tsx
<p className="important">Exam tomorrow</p>
```

### Rule 4: Use camelCase for many attributes

```tsx
<button onClick={handleClick}>Save</button>
```

## JSX is not a string

Do not place JSX in quotation marks:

```tsx
const wrong = "<h1>Hello</h1>";
const correct = <h1>Hello</h1>;
```

The first value is plain text. The second is a React element.

## Try it

Create variables for your name, favorite subject, and current grade. Display them in a student profile using JSX.

## Checkpoint

Why does JSX use `{studentName}` instead of `"studentName"`?

**Answer:** Curly braces read the JavaScript variable. Quotation marks display the literal word `studentName`.

---

# 6. Tutorial 2: Functional Components

A functional component is a JavaScript function that returns JSX.

```tsx
function Greeting() {
  return <h2>Hello, student!</h2>;
}
```

Use it like an HTML element:

```tsx
function App() {
  return (
    <main>
      <h1>Study Planner</h1>
      <Greeting />
    </main>
  );
}
```

## Component naming rule

Component names begin with a capital letter:

```tsx
function AssignmentCard() {
  return <article>Math worksheet</article>;
}
```

React treats lowercase names like built-in HTML tags:

```tsx
<article>Built-in HTML element</article>
<AssignmentCard /> {/* Custom React component */}
```

## Put a component in its own file

Create `src/components/StudentProfile.tsx`:

```tsx
function StudentProfile() {
  return (
    <section>
      <h2>Jordan Lee</h2>
      <p>Favorite subject: Computer Science</p>
    </section>
  );
}

export default StudentProfile;
```

Import and use it in `App.tsx`:

```tsx
import StudentProfile from "./components/StudentProfile.tsx";

function App() {
  return (
    <main>
      <h1>Student Dashboard</h1>
      <StudentProfile />
    </main>
  );
}

export default App;
```

## Keep components focused

A component should usually have one clear job:

- `Header` displays the heading;
- `AssignmentForm` collects assignment information;
- `AssignmentList` displays assignments;
- `AssignmentCard` displays one assignment.

If a component becomes difficult to explain in one sentence, it may be doing too much.

## Try it

Create these components:

```text
App
├── Header
├── StudentProfile
└── Footer
```

## Checkpoint

Fix this component:

```tsx
function schoolname() {
  <h1>Lincoln High School</h1>;
}
```

**Answer:**

```tsx
function SchoolName() {
  return <h1>Lincoln High School</h1>;
}
```

It needed a capitalized name and a `return`.

---

# 7. Tutorial 3: Props

Props are information passed from a parent component to a child component. Think of props as function arguments.

```tsx
interface GreetingProps {
  name: string;
}

function Greeting({ name }: GreetingProps) {
  return <h2>Hello, {name}!</h2>;
}

function App() {
  return (
    <main>
      <Greeting name="Ava" />
      <Greeting name="Noah" />
    </main>
  );
}
```

The same component displays different information because it receives different props.

An `interface` describes the required shape of the props. TypeScript now reports an error if a parent forgets `name` or passes a number instead of a string.

## Multiple props

```tsx
interface AssignmentCardProps {
  subject: string;
  title: string;
  dueDate: string;
}

function AssignmentCard({
  subject,
  title,
  dueDate,
}: AssignmentCardProps) {
  return (
    <article>
      <h2>{title}</h2>
      <p>Subject: {subject}</p>
      <p>Due: {dueDate}</p>
    </article>
  );
}

function App() {
  return (
    <AssignmentCard
      subject="Biology"
      title="Cell Diagram"
      dueDate="Friday"
    />
  );
}
```

## Strings versus JavaScript values

Pass a string with quotation marks:

```tsx
<AssignmentCard subject="Biology" />
```

Pass a number, Boolean, array, object, or variable with curly braces:

```tsx
<Progress completed={3} total={5} />
```

## Props are read-only

A child should not change its props:

```tsx
interface ScoreProps {
  points: number;
}

function Score({ points }: ScoreProps) {
  // Do not write: points = points + 1
  return <p>Points: {points}</p>;
}
```

If data must change, its owner should update state and pass the new value down.

## The `children` prop

Content placed between component tags becomes `children`:

```tsx
import type { ReactNode } from "react";

interface PanelProps {
  title: string;
  children: ReactNode;
}

function Panel({ title, children }: PanelProps) {
  return (
    <section className="panel">
      <h2>{title}</h2>
      {children}
    </section>
  );
}

function App() {
  return (
    <Panel title="Reminder">
      <p>Bring your calculator tomorrow.</p>
    </Panel>
  );
}
```

## Props versus state

| Props | State |
|---|---|
| Passed in by a parent | Owned by a component |
| Read-only for the receiver | Updated with a setter or reducer |
| Customize a component | Remember changing information |

## Try it

Create a `CourseCard` component with `name`, `teacher`, and `room` props. Display three different courses.

---

# 8. Tutorial 4: Events

Events occur when a user interacts with the page.

```tsx
function EncouragementButton() {
  function handleClick() {
    alert("You can do it!");
  }

  return <button onClick={handleClick}>Encourage me</button>;
}
```

Notice this important difference:

```tsx
<button onClick={handleClick}>Correct</button>
<button onClick={handleClick()}>Usually incorrect</button>
```

- `handleClick` gives React the function to run later.
- `handleClick()` runs the function immediately while rendering.

## Event information

React passes an event object to the handler:

```tsx
function SearchBox() {
  function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
    console.log(event.target.value);
  }

  return <input onChange={handleChange} placeholder="Search assignments" />;
}
```

## Pass information to an event handler

Use an arrow function:

```tsx
function SubjectButtons() {
  function showSubject(subject: string) {
    alert(`You selected ${subject}`);
  }

  return (
    <div>
      <button onClick={() => showSubject("Math")}>Math</button>
      <button onClick={() => showSubject("History")}>History</button>
    </div>
  );
}
```

## Common React events

| Event | When it occurs |
|---|---|
| `onClick` | An element is clicked |
| `onChange` | An input value changes |
| `onSubmit` | A form is submitted |
| `onFocus` | An element receives focus |
| `onBlur` | An element loses focus |
| `onKeyDown` | A keyboard key is pressed |

## Checkpoint

Why is this incorrect?

```tsx
<button onClick={alert("Saved!")}>Save</button>
```

**Answer:** `alert` runs immediately. Wrap it in a function:

```tsx
<button onClick={() => alert("Saved!")}>Save</button>
```

---

# 9. Tutorial 5: State and `useState`

State is information that a component remembers between renders. Examples include:

- a score;
- text in a form;
- whether a menu is open;
- a list of assignments;
- the selected theme.

## Your first state

```tsx
import { useState } from "react";

function ScoreCounter() {
  const [score, setScore] = useState(0);

  return (
    <section>
      <p>Score: {score}</p>
      <button onClick={() => setScore(score + 1)}>Add point</button>
    </section>
  );
}
```

Break down this line:

```tsx
const [score, setScore] = useState(0);
```

| Part | Meaning |
|---|---|
| `score` | Current state value |
| `setScore` | Function that requests an update |
| `useState(0)` | Creates state with an initial value of `0` |

When the button is clicked:

1. `setScore(score + 1)` requests a new value.
2. React renders the component again.
3. `score` contains the new value.
4. The screen updates.

## State updates are scheduled

The setter does not instantly change the variable in the currently running code:

```tsx
function handleClick() {
  setScore(score + 1);
  console.log(score); // Still the old value in this handler
}
```

Think of `setScore` as sending React a request: "Use this value in the next render."

## Update from the previous value

When the next value depends on the previous value, use an updater function:

```tsx
function addThreePoints() {
  setScore((currentScore) => currentScore + 1);
  setScore((currentScore) => currentScore + 1);
  setScore((currentScore) => currentScore + 1);
}
```

Each updater receives the latest queued value.

## Boolean state

```tsx
import { useState } from "react";

function Answer() {
  const [isVisible, setIsVisible] = useState(false);

  return (
    <section>
      <button onClick={() => setIsVisible((visible) => !visible)}>
        {isVisible ? "Hide answer" : "Show answer"}
      </button>
      {isVisible && <p>The answer is 42.</p>}
    </section>
  );
}
```

## Text state

```tsx
import { useState } from "react";

function NameEditor() {
  const [name, setName] = useState("");

  return (
    <label>
      Name:
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
      />
      <span>Hello, {name || "student"}!</span>
    </label>
  );
}
```

This input is **controlled** because React state controls its displayed value.

## Object state

Never directly change an object in state:

```tsx
const [student, setStudent] = useState({
  name: "Sam",
  grade: 10,
});

// Incorrect: changes the existing object
student.grade = 11;

// Correct: creates a new object
setStudent({
  ...student,
  grade: 11,
});
```

The spread syntax copies the existing properties. The later `grade` property replaces the old grade.

When using the previous value, prefer:

```tsx
setStudent((currentStudent) => ({
  ...currentStudent,
  grade: currentStudent.grade + 1,
}));
```

## Array state

Create a new array instead of changing the old one:

```tsx
const [subjects, setSubjects] = useState(["Math", "English"]);

function addScience() {
  setSubjects((currentSubjects) => [...currentSubjects, "Science"]);
}

function removeSubject(subjectToRemove) {
  setSubjects((currentSubjects) =>
    currentSubjects.filter((subject) => subject !== subjectToRemove)
  );
}
```

Avoid mutating methods such as `push`, `pop`, and `splice` on state arrays.

## State belongs to a position in the tree

Each rendered component instance has its own state:

```tsx
function App() {
  return (
    <>
      <ScoreCounter />
      <ScoreCounter />
    </>
  );
}
```

The two counters are independent.

## Do not store values you can calculate

Avoid:

```tsx
const [firstName, setFirstName] = useState("Alex");
const [lastName, setLastName] = useState("Kim");
const [fullName, setFullName] = useState("Alex Kim");
```

Calculate during rendering:

```tsx
const fullName = `${firstName} ${lastName}`;
```

This avoids inconsistent state.

## Try it

Build a counter with:

- a `+1` button;
- a `-1` button;
- a reset button;
- a message that says "Goal reached!" at 10 points.

---

# 10. Tutorial 6: Conditional Rendering

Components often display different content in different situations.

## Use `if`

```tsx
interface AssignmentStatusProps {
  isComplete: boolean;
}

function AssignmentStatus({ isComplete }: AssignmentStatusProps) {
  if (isComplete) {
    return <p>Complete!</p>;
  }

  return <p>Not finished</p>;
}
```

## Use the ternary operator

```tsx
function AssignmentStatus({ isComplete }: AssignmentStatusProps) {
  return <p>{isComplete ? "Complete!" : "Not finished"}</p>;
}
```

The pattern is:

```ts
condition ? valueWhenTrue : valueWhenFalse
```

## Use `&&` when there is no false case

```tsx
interface WarningProps {
  assignmentsDue: number;
}

function Warning({ assignmentsDue }: WarningProps) {
  return (
    <section>
      <p>{assignmentsDue} assignments due</p>
      {assignmentsDue > 5 && <strong>Busy week ahead!</strong>}
    </section>
  );
}
```

Be careful with zero:

```tsx
{messageCount > 0 && <p>{messageCount} new messages</p>}
```

Using `{messageCount && ...}` would display `0` when the count is zero.

## Store JSX in a variable

```tsx
import type { ReactNode } from "react";

interface StudyMessageProps {
  minutes: number;
}

function StudyMessage({ minutes }: StudyMessageProps) {
  let message: ReactNode;

  if (minutes >= 60) {
    message = <p>Excellent focus!</p>;
  } else {
    message = <p>Keep going!</p>;
  }

  return <section>{message}</section>;
}
```

---

# 11. Tutorial 7: Lists and Keys

Use `map` to turn an array into React elements:

```tsx
function SubjectList() {
  const subjects = ["Math", "Biology", "Art"];

  return (
    <ul>
      {subjects.map((subject) => (
        <li key={subject}>{subject}</li>
      ))}
    </ul>
  );
}
```

## Why keys matter

A key gives an item a stable identity. React uses keys to understand which item was added, removed, or changed.

```tsx
interface Assignment {
  id: number;
  title: string;
  isComplete?: boolean;
}

const assignments: Assignment[] = [
  { id: 101, title: "Read chapter 4" },
  { id: 102, title: "Complete lab report" },
];

function AssignmentList() {
  return (
    <ul>
      {assignments.map((assignment) => (
        <li key={assignment.id}>{assignment.title}</li>
      ))}
    </ul>
  );
}
```

## Good and bad keys

Good:

```tsx
<li key={assignment.id}>{assignment.title}</li>
```

Risky when items can move, be inserted, or be deleted:

```tsx
<li key={index}>{assignment.title}</li>
```

Incorrect:

```tsx
<li key={Math.random()}>{assignment.title}</li>
```

Random keys change every render and destroy stable identity.

## Filter a list

```tsx
interface IncompleteAssignmentsProps {
  assignments: Assignment[];
}

function IncompleteAssignments({
  assignments,
}: IncompleteAssignmentsProps) {
  const incompleteAssignments = assignments.filter(
    (assignment) => !assignment.isComplete
  );

  return (
    <ul>
      {incompleteAssignments.map((assignment) => (
        <li key={assignment.id}>{assignment.title}</li>
      ))}
    </ul>
  );
}
```

## Empty states

Tell the user when a list is empty:

```tsx
if (assignments.length === 0) {
  return <p>No assignments yet. Add your first one!</p>;
}
```

---

# 12. Tutorial 8: Forms

Forms collect user input. React commonly uses controlled inputs.

```tsx
import { useState, type FormEvent } from "react";

function AssignmentForm() {
  const [title, setTitle] = useState("");

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault();

    const trimmedTitle = title.trim();

    if (!trimmedTitle) {
      return;
    }

    alert(`Adding: ${trimmedTitle}`);
    setTitle("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="assignment-title">Assignment title</label>
      <input
        id="assignment-title"
        value={title}
        onChange={(event) => setTitle(event.target.value)}
      />
      <button type="submit">Add assignment</button>
    </form>
  );
}
```

## What happens during submission?

1. The user types.
2. `onChange` updates `title`.
3. React renders with the new `title`.
4. The user submits the form.
5. `event.preventDefault()` stops the browser from reloading the page.
6. The handler validates and uses the value.
7. The setter clears the input.

## A form with multiple fields

```tsx
import {
  useState,
  type ChangeEvent,
  type FormEvent,
} from "react";

function CourseForm() {
  const [formData, setFormData] = useState({
    course: "",
    teacher: "",
  });

  function handleChange(event: ChangeEvent<HTMLInputElement>) {
    const { name, value } = event.target;

    setFormData((currentData) => ({
      ...currentData,
      [name]: value,
    }));
  }

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault();
    console.log(formData);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="course">Course</label>
      <input
        id="course"
        name="course"
        value={formData.course}
        onChange={handleChange}
      />

      <label htmlFor="teacher">Teacher</label>
      <input
        id="teacher"
        name="teacher"
        value={formData.teacher}
        onChange={handleChange}
      />

      <button type="submit">Save course</button>
    </form>
  );
}
```

The computed property `[name]` updates the matching field.

## Show a validation message

```tsx
const [error, setError] = useState("");

function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
  event.preventDefault();

  if (!title.trim()) {
    setError("Enter an assignment title.");
    return;
  }

  setError("");
  // Save the assignment.
}
```

Display it:

```tsx
{error && <p role="alert">{error}</p>}
```

---

# 13. Tutorial 9: Class Components

Before hooks were added to React, class components were the main way to use state and lifecycle methods. Modern React code normally uses functional components, but class components still appear in older projects and are useful to understand.

## A basic class component

```tsx
import { Component } from "react";

class Greeting extends Component {
  render() {
    return <h2>Hello from a class component!</h2>;
  }
}

export default Greeting;
```

A class component:

- extends React's `Component` class;
- must have a `render` method;
- returns JSX from `render`.

## Props in a class component

```tsx
import { Component } from "react";

interface GreetingProps {
  name: string;
}

class Greeting extends Component<GreetingProps> {
  render() {
    return <h2>Hello, {this.props.name}!</h2>;
  }
}
```

Use it in the same way:

```tsx
<Greeting name="Taylor" />
```

## State in a class component

```tsx
import { Component } from "react";

interface ScoreCounterState {
  score: number;
}

class ScoreCounter extends Component<object, ScoreCounterState> {
  state = {
    score: 0,
  };

  addPoint = () => {
    this.setState((currentState) => ({
      score: currentState.score + 1,
    }));
  };

  render() {
    return (
      <section>
        <p>Score: {this.state.score}</p>
        <button onClick={this.addPoint}>Add point</button>
      </section>
    );
  }
}

export default ScoreCounter;
```

Important class keywords:

| Code | Meaning |
|---|---|
| `this.props` | Props given to the component |
| `this.state` | Current state object |
| `this.setState(...)` | Requests a state update |
| `this.methodName` | A property or method on this component instance |

Do not directly change class state:

```tsx
// Incorrect
this.state.score = this.state.score + 1;
```

Use `this.setState`.

## Lifecycle methods

Lifecycle methods run at important moments:

```tsx
interface ClockState {
  time: Date;
}

class Clock extends Component<object, ClockState> {
  private timerId: ReturnType<typeof setInterval> | undefined;

  state = {
    time: new Date(),
  };

  componentDidMount() {
    this.timerId = setInterval(() => {
      this.setState({ time: new Date() });
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerId);
  }

  render() {
    return <p>{this.state.time.toLocaleTimeString()}</p>;
  }
}
```

- `componentDidMount` runs after the component first appears.
- `componentDidUpdate` runs after an update.
- `componentWillUnmount` runs before the component is removed.

Cleanup matters. Without `clearInterval`, the timer could continue after the component disappears.

## Class versus functional components

The same counter as a function:

```tsx
import { useState } from "react";

function ScoreCounter() {
  const [score, setScore] = useState(0);

  return (
    <section>
      <p>Score: {score}</p>
      <button onClick={() => setScore((value) => value + 1)}>
        Add point
      </button>
    </section>
  );
}
```

| Functional component | Class component |
|---|---|
| Plain JavaScript function | JavaScript class |
| Uses hooks | Uses lifecycle methods and `this.setState` |
| No `this` | Frequently uses `this` |
| Preferred for new code | Common in older code |

## Should you rewrite every class?

No. A working class component does not need to be rewritten only because it is a class. Convert it when there is a clear reason, enough test coverage, and time to verify behavior.

## Conversion exercise

Convert this class to a functional component:

```tsx
interface WelcomeProps {
  name: string;
}

class Welcome extends Component<WelcomeProps> {
  render() {
    return <h2>Welcome, {this.props.name}!</h2>;
  }
}
```

**Answer:**

```tsx
interface WelcomeProps {
  name: string;
}

function Welcome({ name }: WelcomeProps) {
  return <h2>Welcome, {name}!</h2>;
}
```

---

# 14. Tutorial 10: `useEffect`

Rendering should calculate UI. Sometimes a component must synchronize with something outside React, such as:

- a network API;
- the browser tab title;
- a timer;
- browser storage;
- a third-party library.

`useEffect` runs synchronization logic after React updates the screen.

## Update the document title

```tsx
import { useEffect, useState } from "react";

function ScoreCounter() {
  const [score, setScore] = useState(0);

  useEffect(() => {
    document.title = `Score: ${score}`;
  }, [score]);

  return (
    <button onClick={() => setScore((value) => value + 1)}>
      Score: {score}
    </button>
  );
}
```

The dependency array `[score]` means:

> Run after the first render and whenever `score` changes.

## Dependency patterns

```tsx
useEffect(() => {
  // Runs after every render.
});
```

```tsx
useEffect(() => {
  // Runs after the component first appears.
}, []);
```

```tsx
useEffect(() => {
  // Runs after first render and when userId changes.
}, [userId]);
```

Follow the React hooks lint rules. Do not hide missing dependencies just to silence a warning.

## Cleanup

Effects can return a cleanup function:

```tsx
import { useEffect, useState } from "react";

function Clock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const timerId = setInterval(() => {
      setTime(new Date());
    }, 1000);

    return () => {
      clearInterval(timerId);
    };
  }, []);

  return <p>{time.toLocaleTimeString()}</p>;
}
```

Cleanup runs:

- before the effect runs again;
- when the component is removed.

## Fetch data

```tsx
import { useEffect, useState } from "react";

interface User {
  id: number;
  name: string;
}

type LoadStatus = "loading" | "success" | "error";

function UserList() {
  const [users, setUsers] = useState<User[]>([]);
  const [status, setStatus] = useState<LoadStatus>("loading");

  useEffect(() => {
    const controller = new AbortController();

    async function loadUsers() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users",
          { signal: controller.signal }
        );

        if (!response.ok) {
          throw new Error(`Request failed: ${response.status}`);
        }

        const data: User[] = await response.json();
        setUsers(data);
        setStatus("success");
      } catch (error: unknown) {
        const wasAborted =
          error instanceof DOMException && error.name === "AbortError";

        if (!wasAborted) {
          console.error(error);
          setStatus("error");
        }
      }
    }

    loadUsers();

    return () => {
      controller.abort();
    };
  }, []);

  if (status === "loading") {
    return <p>Loading users...</p>;
  }

  if (status === "error") {
    return <p role="alert">Could not load users.</p>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

This example represents loading, success, and error states. It also cancels the request if the component is removed.

## You might not need an effect

Do not use an effect to calculate a value from props or state:

```tsx
// Avoid
const [fullName, setFullName] = useState("");

useEffect(() => {
  setFullName(`${firstName} ${lastName}`);
}, [firstName, lastName]);
```

Calculate it while rendering:

```tsx
const fullName = `${firstName} ${lastName}`;
```

Do not use an effect for a click action:

```tsx
function handleSubmit() {
  // Submit here because this logic happened due to this event.
}
```

## Development behavior in Strict Mode

During development, Strict Mode may perform an extra setup-and-cleanup cycle for effects. This helps expose missing cleanup. Write effects so that this cycle is safe.

---

# 15. Tutorial 11: `useRef`

`useRef` stores a value that survives renders without causing a render when it changes.

## Focus an input

```tsx
import { useRef } from "react";

function SearchBox() {
  const inputRef = useRef<HTMLInputElement>(null);

  function focusInput() {
    inputRef.current?.focus();
  }

  return (
    <div>
      <input ref={inputRef} aria-label="Search assignments" />
      <button onClick={focusInput}>Focus search</button>
    </div>
  );
}
```

React places the input DOM element in `inputRef.current`.

## Store a timer ID

```tsx
const timerRef = useRef<ReturnType<typeof setInterval> | null>(null);

function startTimer() {
  timerRef.current = setInterval(() => {
    console.log("Tick");
  }, 1000);
}

function stopTimer() {
  if (timerRef.current !== null) {
    clearInterval(timerRef.current);
  }
}
```

## State versus ref

| State | Ref |
|---|---|
| Changing it causes a render | Changing it does not cause a render |
| Used for information displayed by UI | Used for DOM nodes or values not needed for display |
| Read through the state variable | Read through `.current` |

If the screen should update when a value changes, use state rather than a ref.

---

# 16. Tutorial 12: `useContext`

Context shares information with many components without passing the same prop through every level.

Common uses include:

- theme;
- current language;
- signed-in user;
- shared application settings.

## Create a context

Create `src/ThemeContext.ts`:

```ts
import { createContext } from "react";

export type Theme = "light" | "dark";

const ThemeContext = createContext<Theme>("light");

export default ThemeContext;
```

## Provide a value

```tsx
import { useState } from "react";
import ThemeContext, { type Theme } from "./ThemeContext";
import Toolbar from "./Toolbar.tsx";

function App() {
  const [theme, setTheme] = useState<Theme>("light");

  return (
    <ThemeContext.Provider value={theme}>
      <button
        onClick={() =>
          setTheme((currentTheme) =>
            currentTheme === "light" ? "dark" : "light"
          )
        }
      >
        Switch theme
      </button>
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

## Read the value

```tsx
import { useContext } from "react";
import ThemeContext from "./ThemeContext";

function Toolbar() {
  const theme = useContext(ThemeContext);

  return <div className={`toolbar toolbar--${theme}`}>Study tools</div>;
}
```

`Toolbar` reads the closest matching provider above it in the component tree.

## Do not use context for everything

Regular props are clear and useful. Use context when information is truly shared across distant parts of a component tree. Too much context can make data flow harder to follow.

---

# 17. Tutorial 13: `useReducer`

`useReducer` manages state through actions. It can be helpful when:

- state has several related changes;
- update rules are becoming complex;
- many event handlers change the same state;
- you want update logic in one testable function.

## A task reducer

```tsx
import { useReducer } from "react";

interface Task {
  id: string;
  title: string;
  isComplete: boolean;
}

type TaskAction =
  | { type: "added"; id: string; title: string }
  | { type: "toggled"; id: string }
  | { type: "deleted"; id: string };

function taskReducer(tasks: Task[], action: TaskAction): Task[] {
  switch (action.type) {
    case "added":
      return [
        ...tasks,
        {
          id: action.id,
          title: action.title,
          isComplete: false,
        },
      ];

    case "toggled":
      return tasks.map((task) =>
        task.id === action.id
          ? { ...task, isComplete: !task.isComplete }
          : task
      );

    case "deleted":
      return tasks.filter((task) => task.id !== action.id);

    default: {
      const unexpectedAction: never = action;
      throw new Error(`Unknown action: ${JSON.stringify(unexpectedAction)}`);
    }
  }
}

function TaskList() {
  const [tasks, dispatch] = useReducer(taskReducer, []);

  function addTask() {
    dispatch({
      type: "added",
      id: crypto.randomUUID(),
      title: "Study React",
    });
  }

  return (
    <section>
      <button onClick={addTask}>Add example task</button>
      <ul>
        {tasks.map((task) => (
          <li key={task.id}>
            <label>
              <input
                type="checkbox"
                checked={task.isComplete}
                onChange={() =>
                  dispatch({ type: "toggled", id: task.id })
                }
              />
              {task.title}
            </label>
            <button
              onClick={() =>
                dispatch({ type: "deleted", id: task.id })
              }
            >
              Delete
            </button>
          </li>
        ))}
      </ul>
    </section>
  );
}
```

## Reducer vocabulary

| Term | Meaning |
|---|---|
| State | Current data |
| Action | Object describing what happened |
| Reducer | Function returning the next state |
| Dispatch | Function that sends an action |

A reducer should be **pure**:

- do not change existing state;
- do not make network requests;
- do not use random values inside the reducer;
- return the same result for the same state and action.

Notice that the ID is created before dispatching, not inside the reducer.

## `useState` or `useReducer`?

Use `useState` for simple, independent values. Consider `useReducer` when several updates belong to the same state and the rules are easier to understand as named actions.

---

# 18. Tutorial 14: `useMemo` and `useCallback`

These hooks are performance tools. Most beginner applications do not need them.

## `useMemo`

`useMemo` can reuse the result of an expensive calculation until its dependencies change:

```tsx
import { useMemo } from "react";

interface Assignment {
  id: string;
  title: string;
}

interface AssignmentListProps {
  assignments: Assignment[];
  searchText: string;
}

function AssignmentList({
  assignments,
  searchText,
}: AssignmentListProps) {
  const visibleAssignments = useMemo(() => {
    return assignments.filter((assignment) =>
      assignment.title.toLowerCase().includes(searchText.toLowerCase())
    );
  }, [assignments, searchText]);

  return (
    <ul>
      {visibleAssignments.map((assignment) => (
        <li key={assignment.id}>{assignment.title}</li>
      ))}
    </ul>
  );
}
```

For a small list, normal filtering is probably simpler:

```tsx
const visibleAssignments = assignments.filter(/* ... */);
```

## `useCallback`

`useCallback` can reuse a function definition until dependencies change:

```tsx
import { useCallback } from "react";

const handleDelete = useCallback((id: string) => {
  setAssignments((currentAssignments) =>
    currentAssignments.filter((assignment) => assignment.id !== id)
  );
}, []);
```

It is most useful when function identity matters, such as when passing a callback to a carefully memoized child.

## Do not optimize without evidence

Before adding these hooks:

1. Confirm there is a noticeable performance problem.
2. Measure it with React Developer Tools Profiler.
3. Find the expensive work or unnecessary renders.
4. Apply the smallest useful optimization.
5. Measure again.

`useMemo` and `useCallback` can make code harder to read. They are not automatically better.

---

# 19. Tutorial 15: Custom Hooks

A custom hook is a function that uses hooks to share stateful logic. Its name begins with `use`.

## Save state in local storage

Create `src/hooks/useLocalStorage.ts`:

```ts
import {
  useEffect,
  useState,
  type Dispatch,
  type SetStateAction,
} from "react";

function readStoredValue<T>(key: string, initialValue: T): T {
  const savedValue = localStorage.getItem(key);

  if (savedValue === null) {
    return initialValue;
  }

  try {
    return JSON.parse(savedValue) as T;
  } catch (error: unknown) {
    console.error(`Could not read local storage key "${key}".`, error);
    return initialValue;
  }
}

export default function useLocalStorage<T>(
  key: string,
  initialValue: T
): [T, Dispatch<SetStateAction<T>>] {
  const [value, setValue] = useState(() =>
    readStoredValue(key, initialValue)
  );

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}
```

Use it like `useState`:

```tsx
import useLocalStorage from "./hooks/useLocalStorage.ts";

function Notes() {
  const [notes, setNotes] = useLocalStorage("study-notes", "");

  return (
    <textarea
      value={notes}
      onChange={(event) => setNotes(event.target.value)}
      aria-label="Study notes"
    />
  );
}
```

## What a custom hook shares

A custom hook shares **logic**, not one state value. If two components call `useLocalStorage`, each call has its own React state.

## Good custom hooks

Good names explain their purpose:

- `useLocalStorage`;
- `useOnlineStatus`;
- `useDocumentTitle`;
- `useAssignments`.

Do not create a custom hook only to hide one simple line.

---

# 20. Rules of Hooks

Hooks rely on being called in the same order during every render.

## Rule 1: Call hooks at the top level

Incorrect:

```tsx
if (isLoggedIn) {
  const [name, setName] = useState("");
}
```

Correct:

```tsx
const [name, setName] = useState("");

if (!isLoggedIn) {
  return <p>Please sign in.</p>;
}
```

Do not call hooks inside:

- conditions;
- loops;
- event handlers;
- nested regular functions;
- `try`/`catch` blocks.

## Rule 2: Call hooks only from React functions

Call hooks from:

- functional components;
- custom hooks.

Do not call them from ordinary JavaScript functions.

## Use the linter

React projects use lint rules to catch hook mistakes. Run:

```bash
npm run lint
```

Do not disable a hook warning unless you fully understand why it is safe.

---

# 21. Final Project: Study Planner

Now we will combine components, props, events, lists, forms, state, effects, refs, and a custom hook.

## Features

The app will let a student:

- add an assignment;
- choose a subject and due date;
- mark an assignment complete;
- delete an assignment;
- search assignments;
- filter by status;
- see completion progress;
- keep assignments after refreshing the page;
- focus the title field after adding an assignment.

## Step 1: Create the files

Inside `src`, create:

```text
src/
├── components/
│   ├── AssignmentForm.tsx
│   ├── AssignmentItem.tsx
│   ├── AssignmentList.tsx
│   ├── AssignmentSummary.tsx
│   └── FilterBar.tsx
├── hooks/
│   └── useLocalStorage.ts
├── types.ts
├── App.css
├── App.tsx
├── index.css
└── main.tsx
```

Use the `useLocalStorage.ts` hook from Tutorial 15.

Create `src/types.ts` for types shared by several components:

```ts
export interface Assignment {
  id: string;
  title: string;
  subject: string;
  dueDate: string;
  isComplete: boolean;
}

export type AssignmentFilter = "all" | "active" | "complete";
```

An `interface` describes an object's shape. The union type allows only the three listed filter values.

## Step 2: Build `AssignmentForm`

Create `src/components/AssignmentForm.tsx`:

```tsx
import {
  useRef,
  useState,
  type ChangeEvent,
  type FormEvent,
} from "react";
import type { Assignment } from "../types";

const emptyForm = {
  title: "",
  subject: "Math",
  dueDate: "",
};

interface AssignmentFormProps {
  onAddAssignment: (assignment: Assignment) => void;
}

function AssignmentForm({ onAddAssignment }: AssignmentFormProps) {
  const [formData, setFormData] = useState(emptyForm);
  const [error, setError] = useState("");
  const titleInputRef = useRef<HTMLInputElement>(null);

  function handleChange(
    event: ChangeEvent<HTMLInputElement | HTMLSelectElement>
  ) {
    const { name, value } = event.target;

    setFormData((currentData) => ({
      ...currentData,
      [name]: value,
    }));
  }

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault();

    const title = formData.title.trim();

    if (!title) {
      setError("Enter an assignment title.");
      titleInputRef.current?.focus();
      return;
    }

    onAddAssignment({
      id: crypto.randomUUID(),
      title,
      subject: formData.subject,
      dueDate: formData.dueDate,
      isComplete: false,
    });

    setFormData(emptyForm);
    setError("");
    titleInputRef.current?.focus();
  }

  return (
    <form className="assignment-form" onSubmit={handleSubmit}>
      <h2>Add an assignment</h2>

      <label htmlFor="title">Title</label>
      <input
        ref={titleInputRef}
        id="title"
        name="title"
        value={formData.title}
        onChange={handleChange}
        placeholder="Example: Finish chapter 5"
      />

      <label htmlFor="subject">Subject</label>
      <select
        id="subject"
        name="subject"
        value={formData.subject}
        onChange={handleChange}
      >
        <option>Math</option>
        <option>Science</option>
        <option>English</option>
        <option>History</option>
        <option>Art</option>
        <option>Other</option>
      </select>

      <label htmlFor="dueDate">Due date</label>
      <input
        id="dueDate"
        name="dueDate"
        type="date"
        value={formData.dueDate}
        onChange={handleChange}
      />

      {error && <p className="error" role="alert">{error}</p>}

      <button type="submit">Add assignment</button>
    </form>
  );
}

export default AssignmentForm;
```

Concepts used:

- `useState` controls the form and error;
- `useRef` focuses the input;
- `onChange` handles typing and selection;
- `onSubmit` handles the complete form;
- the callback prop sends a new assignment to the parent.

## Step 3: Build `AssignmentItem`

Create `src/components/AssignmentItem.tsx`:

```tsx
import type { Assignment } from "../types";

interface AssignmentItemProps {
  assignment: Assignment;
  onToggle: (id: string) => void;
  onDelete: (id: string) => void;
}

function AssignmentItem({
  assignment,
  onToggle,
  onDelete,
}: AssignmentItemProps) {
  return (
    <li className={assignment.isComplete ? "assignment complete" : "assignment"}>
      <div>
        <label>
          <input
            type="checkbox"
            checked={assignment.isComplete}
            onChange={() => onToggle(assignment.id)}
          />
          <span>{assignment.title}</span>
        </label>
        <p>
          {assignment.subject}
          {assignment.dueDate && ` | Due ${assignment.dueDate}`}
        </p>
      </div>

      <button
        className="danger"
        type="button"
        onClick={() => onDelete(assignment.id)}
        aria-label={`Delete ${assignment.title}`}
      >
        Delete
      </button>
    </li>
  );
}

export default AssignmentItem;
```

This component does not own the assignments. It receives one assignment and callback props.

## Step 4: Build `AssignmentList`

Create `src/components/AssignmentList.tsx`:

```tsx
import AssignmentItem from "./AssignmentItem.tsx";
import type { Assignment } from "../types";

interface AssignmentListProps {
  assignments: Assignment[];
  onToggle: (id: string) => void;
  onDelete: (id: string) => void;
}

function AssignmentList({
  assignments,
  onToggle,
  onDelete,
}: AssignmentListProps) {
  if (assignments.length === 0) {
    return <p className="empty-state">No matching assignments.</p>;
  }

  return (
    <ul className="assignment-list">
      {assignments.map((assignment) => (
        <AssignmentItem
          key={assignment.id}
          assignment={assignment}
          onToggle={onToggle}
          onDelete={onDelete}
        />
      ))}
    </ul>
  );
}

export default AssignmentList;
```

The assignment ID is the key because it is stable and unique.

## Step 5: Build `FilterBar`

Create `src/components/FilterBar.tsx`:

```tsx
import type { ChangeEvent } from "react";
import type { AssignmentFilter } from "../types";

interface FilterBarProps {
  searchText: string;
  onSearchChange: (value: string) => void;
  status: AssignmentFilter;
  onStatusChange: (status: AssignmentFilter) => void;
}

function FilterBar({
  searchText,
  onSearchChange,
  status,
  onStatusChange,
}: FilterBarProps) {
  function handleStatusChange(event: ChangeEvent<HTMLSelectElement>) {
    const nextStatus = event.target.value;

    if (
      nextStatus === "all" ||
      nextStatus === "active" ||
      nextStatus === "complete"
    ) {
      onStatusChange(nextStatus);
    }
  }

  return (
    <section className="filters" aria-label="Assignment filters">
      <label htmlFor="search">Search</label>
      <input
        id="search"
        type="search"
        value={searchText}
        onChange={(event) => onSearchChange(event.target.value)}
        placeholder="Search by title or subject"
      />

      <label htmlFor="status">Status</label>
      <select
        id="status"
        value={status}
        onChange={handleStatusChange}
      >
        <option value="all">All</option>
        <option value="active">Not complete</option>
        <option value="complete">Complete</option>
      </select>
    </section>
  );
}

export default FilterBar;
```

## Step 6: Build `AssignmentSummary`

Create `src/components/AssignmentSummary.tsx`:

```tsx
import type { Assignment } from "../types";

interface AssignmentSummaryProps {
  assignments: Assignment[];
}

function AssignmentSummary({ assignments }: AssignmentSummaryProps) {
  const completedCount = assignments.filter(
    (assignment) => assignment.isComplete
  ).length;

  const totalCount = assignments.length;
  const percentComplete =
    totalCount === 0 ? 0 : Math.round((completedCount / totalCount) * 100);

  return (
    <section className="summary" aria-labelledby="progress-heading">
      <h2 id="progress-heading">Progress</h2>
      <p>
        {completedCount} of {totalCount} complete ({percentComplete}%)
      </p>
      <progress value={completedCount} max={totalCount || 1}>
        {percentComplete}%
      </progress>
    </section>
  );
}

export default AssignmentSummary;
```

`completedCount` and `percentComplete` are calculated values, so they do not need their own state.

## Step 7: Connect everything in `App`

Replace `src/App.tsx`:

```tsx
import { useEffect, useState } from "react";
import "./App.css";
import AssignmentForm from "./components/AssignmentForm.tsx";
import AssignmentList from "./components/AssignmentList.tsx";
import AssignmentSummary from "./components/AssignmentSummary.tsx";
import FilterBar from "./components/FilterBar.tsx";
import useLocalStorage from "./hooks/useLocalStorage.ts";
import type { Assignment, AssignmentFilter } from "./types";

function App() {
  const [assignments, setAssignments] = useLocalStorage<Assignment[]>(
    "assignments",
    []
  );
  const [searchText, setSearchText] = useState("");
  const [status, setStatus] = useState<AssignmentFilter>("all");

  useEffect(() => {
    const incompleteCount = assignments.filter(
      (assignment) => !assignment.isComplete
    ).length;

    document.title = `${incompleteCount} assignments left`;
  }, [assignments]);

  function addAssignment(newAssignment: Assignment) {
    setAssignments((currentAssignments) => [
      ...currentAssignments,
      newAssignment,
    ]);
  }

  function toggleAssignment(id: string) {
    setAssignments((currentAssignments) =>
      currentAssignments.map((assignment) =>
        assignment.id === id
          ? { ...assignment, isComplete: !assignment.isComplete }
          : assignment
      )
    );
  }

  function deleteAssignment(id: string) {
    setAssignments((currentAssignments) =>
      currentAssignments.filter((assignment) => assignment.id !== id)
    );
  }

  const normalizedSearch = searchText.trim().toLowerCase();

  const visibleAssignments = assignments.filter((assignment) => {
    const matchesSearch =
      assignment.title.toLowerCase().includes(normalizedSearch) ||
      assignment.subject.toLowerCase().includes(normalizedSearch);

    const matchesStatus =
      status === "all" ||
      (status === "complete" && assignment.isComplete) ||
      (status === "active" && !assignment.isComplete);

    return matchesSearch && matchesStatus;
  });

  return (
    <main>
      <header>
        <p className="eyebrow">Student dashboard</p>
        <h1>Study Planner</h1>
        <p>Plan your work and celebrate your progress.</p>
      </header>

      <AssignmentForm onAddAssignment={addAssignment} />

      <AssignmentSummary assignments={assignments} />

      <section aria-labelledby="assignments-heading">
        <h2 id="assignments-heading">Your assignments</h2>
        <FilterBar
          searchText={searchText}
          onSearchChange={setSearchText}
          status={status}
          onStatusChange={setStatus}
        />
        <AssignmentList
          assignments={visibleAssignments}
          onToggle={toggleAssignment}
          onDelete={deleteAssignment}
        />
      </section>
    </main>
  );
}

export default App;
```

## Step 8: Add styles

Replace `src/index.css`:

```css
:root {
  font-family: Inter, system-ui, sans-serif;
  color: #172033;
  background: #eef2ff;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
}

* {
  box-sizing: border-box;
}

body {
  min-width: 320px;
  min-height: 100vh;
  margin: 0;
}

button,
input,
select {
  font: inherit;
}

button,
input,
select {
  min-height: 44px;
}

button {
  cursor: pointer;
}

button:focus-visible,
input:focus-visible,
select:focus-visible {
  outline: 3px solid #f59e0b;
  outline-offset: 2px;
}
```

Replace `src/App.css`:

```css
#root {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem 1rem 4rem;
}

main {
  display: grid;
  gap: 1.5rem;
}

header,
.assignment-form,
.summary,
main > section {
  padding: 1.5rem;
  border-radius: 1rem;
  background: white;
  box-shadow: 0 8px 24px rgb(30 41 59 / 10%);
}

h1,
h2,
p {
  margin-top: 0;
}

.eyebrow {
  margin-bottom: 0.25rem;
  color: #4338ca;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.assignment-form,
.filters {
  display: grid;
  gap: 0.75rem;
}

input,
select {
  width: 100%;
  padding: 0.65rem 0.75rem;
  border: 1px solid #94a3b8;
  border-radius: 0.5rem;
}

button {
  padding: 0.65rem 1rem;
  border: 0;
  border-radius: 0.5rem;
  color: white;
  background: #4338ca;
  font-weight: 700;
}

button:hover {
  background: #3730a3;
}

.danger {
  background: #b91c1c;
}

.danger:hover {
  background: #991b1b;
}

.error {
  color: #b91c1c;
  font-weight: 700;
}

.summary progress {
  width: 100%;
  height: 1rem;
}

.filters {
  grid-template-columns: auto 1fr auto minmax(150px, 0.4fr);
  align-items: center;
  margin-bottom: 1rem;
}

.assignment-list {
  display: grid;
  gap: 0.75rem;
  padding: 0;
  list-style: none;
}

.assignment {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #cbd5e1;
  border-radius: 0.75rem;
}

.assignment label {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-weight: 700;
}

.assignment input[type="checkbox"] {
  width: 1.25rem;
  min-height: 1.25rem;
}

.assignment p {
  margin: 0.5rem 0 0 2rem;
  color: #475569;
}

.assignment.complete span {
  color: #64748b;
  text-decoration: line-through;
}

.empty-state {
  padding: 2rem;
  text-align: center;
}

@media (max-width: 650px) {
  .filters {
    grid-template-columns: 1fr;
  }

  .assignment {
    align-items: stretch;
    flex-direction: column;
  }
}
```

## Step 9: Test the app manually

Check each behavior:

- [ ] Submitting an empty title shows an error.
- [ ] Adding an assignment displays it.
- [ ] The form clears after a successful submission.
- [ ] The title input receives focus after submission.
- [ ] A checkbox changes the completed style.
- [ ] Delete removes only the chosen assignment.
- [ ] Search matches titles and subjects.
- [ ] Each status filter works.
- [ ] The progress count and bar are correct.
- [ ] Refreshing the browser keeps the assignments.
- [ ] The browser tab shows the incomplete count.
- [ ] The layout works on a narrow browser window.
- [ ] All controls work with the keyboard.

## Step 10: Create a production build

Run:

```bash
npm run lint
npm run build
npm run preview
```

Fix lint or build errors before publishing the application.

## Follow the data

The main data flow is:

```text
AssignmentForm
    |
    | calls onAddAssignment(newAssignment)
    v
App updates assignments state
    |
    | passes assignments and callbacks as props
    v
AssignmentList
    |
    v
AssignmentItem
```

This is called **lifting state up**. `App` owns the shared assignment data because several child components need it.

---

# 22. Testing and Debugging

## Read error messages

When an error occurs:

1. Read the first meaningful error message.
2. Note the file and line number.
3. Look at the browser console.
4. Check spelling, imports, braces, and parentheses.
5. Make one change at a time.

## Use browser developer tools

Open Developer Tools with `F12` or `Ctrl+Shift+I`.

Useful tabs:

- **Console:** JavaScript errors and logs;
- **Elements:** rendered HTML and styles;
- **Network:** API requests;
- **Application:** local storage;
- **Accessibility:** accessible names and roles, when available.

## Use React Developer Tools

The React Developer Tools browser extension lets you inspect:

- the component tree;
- props;
- state;
- context;
- component renders with the Profiler.

## Temporary logging

```tsx
console.log({ assignments, searchText, status });
```

Log useful values, then remove debugging logs when finished.

## Test behavior, not implementation details

A strong test asks:

> Can a student add an assignment and see it?

A weaker test asks:

> Was `setAssignments` called?

Users care about visible behavior.

## Suggested automated tests

As a next step, install and learn:

- Vitest;
- React Testing Library;
- `@testing-library/user-event`.

Good first tests:

1. The empty form displays an error.
2. A valid assignment is added.
3. A student can complete an assignment.
4. Search hides nonmatching assignments.
5. Delete removes the selected assignment.

---

# 23. Accessibility Basics

Accessibility makes applications usable by more people, including people who use keyboards, screen readers, zoom, or alternative input devices.

## Use semantic HTML

Prefer meaningful elements:

```tsx
<button onClick={save}>Save</button>
```

Avoid clickable generic elements:

```tsx
<div onClick={save}>Save</div>
```

The button already supports keyboard interaction and communicates its role.

## Label form controls

```tsx
<label htmlFor="email">Email</label>
<input id="email" type="email" />
```

## Add useful alternative text

```tsx
<img src="/student-studying.jpg" alt="Student studying at a desk" />
```

For a decorative image:

```tsx
<img src="/blue-shape.svg" alt="" />
```

## Preserve keyboard focus

Do not remove focus outlines. Make them easy to see. Test the app using:

- `Tab` to move forward;
- `Shift+Tab` to move backward;
- `Enter` or `Space` to activate controls;
- arrow keys where appropriate.

## Do not rely only on color

Use text or icons in addition to color. The Study Planner uses a checkbox and line-through style, not only a color change, to show completion.

## Announce errors

```tsx
<p role="alert">Enter an assignment title.</p>
```

Use ARIA only when normal HTML does not already provide the needed meaning.

---

# 24. Common Mistakes

## Mistake 1: Calling an event handler immediately

```tsx
// Incorrect
<button onClick={saveAssignment()}>Save</button>

// Correct
<button onClick={saveAssignment}>Save</button>
```

## Mistake 2: Mutating state

```tsx
// Incorrect
assignments.push(newAssignment);
setAssignments(assignments);

// Correct
setAssignments((currentAssignments) => [
  ...currentAssignments,
  newAssignment,
]);
```

## Mistake 3: Forgetting a key

```tsx
assignments.map((assignment) => (
  <AssignmentItem key={assignment.id} assignment={assignment} />
));
```

## Mistake 4: Using the array index as a changing list's key

Use a stable ID when items can be added, removed, or reordered.

## Mistake 5: Expecting state to update immediately

State is a snapshot for one render. Use an updater function when the new state depends on the old state.

## Mistake 6: Putting hooks inside conditions

Hooks must run in the same order during every render.

## Mistake 7: Using an effect for calculated data

Calculate values such as totals and filtered arrays during rendering unless measurement shows that memoization is needed.

## Mistake 8: Creating too much state

Each extra state value creates another value that can become inconsistent. Store the minimum information and calculate the rest.

## Mistake 9: Forgetting effect cleanup

Timers, subscriptions, and requests may need cleanup.

## Mistake 10: Confusing props and state

- Props come from a parent.
- State belongs to the component that declares it.

## Mistake 11: Updating a parent while a child renders

Call parent update callbacks from events or effects when appropriate, not directly during child rendering.

## Mistake 12: Ignoring lint warnings

Lint warnings often identify real bugs, especially missing effect dependencies and incorrect hook usage.

---

# 25. Practice Challenges

Try these in order.

## Beginner

1. Build a counter that cannot go below zero.
2. Build a light switch with on/off state.
3. Build a character counter for a text area.
4. Display a list of favorite songs from an array.
5. Add a button that sorts subjects alphabetically.

## Intermediate

1. Add priority (`low`, `medium`, or `high`) to each assignment.
2. Add an "Edit" feature.
3. Sort assignments by due date.
4. Add a button to remove all completed assignments.
5. Show how many assignments are overdue.
6. Add a dark theme with context.

## Advanced beginner

1. Replace the assignment state updates with `useReducer`.
2. Create a `useDocumentTitle` custom hook.
3. Add automated component tests.
4. Load assignments from an API with loading and error states.
5. Add routing for Dashboard, Calendar, and Settings pages.

## Challenge rules

For every feature:

1. Describe the user behavior first.
2. Decide which component should own the state.
3. Draw the props and callbacks.
4. Implement the smallest version.
5. Test with mouse and keyboard.
6. Test an empty value and an unusual value.

---

# 26. React Cheatsheet

## Functional component

```tsx
function Welcome() {
  return <h1>Welcome!</h1>;
}
```

## Component with props

```tsx
interface WelcomeProps {
  name: string;
}

function Welcome({ name }: WelcomeProps) {
  return <h1>Welcome, {name}!</h1>;
}
```

## State

```tsx
const [value, setValue] = useState(initialValue);
```

## Update from previous state

```tsx
setCount((currentCount) => currentCount + 1);
```

## Event

```tsx
<button onClick={handleClick}>Click me</button>
```

## Controlled input

```tsx
<input
  value={name}
  onChange={(event) => setName(event.target.value)}
/>
```

## Conditional rendering

```tsx
{isReady ? <ReadyMessage /> : <WaitingMessage />}
{hasError && <ErrorMessage />}
```

## List

```tsx
items.map((item) => <Item key={item.id} item={item} />);
```

## Add to array state

```tsx
setItems((currentItems) => [...currentItems, newItem]);
```

## Update an item in array state

```tsx
setItems((currentItems) =>
  currentItems.map((item) =>
    item.id === updatedItem.id ? updatedItem : item
  )
);
```

## Remove from array state

```tsx
setItems((currentItems) =>
  currentItems.filter((item) => item.id !== id)
);
```

## Effect with cleanup

```tsx
useEffect(() => {
  const subscription = subscribe();

  return () => {
    subscription.unsubscribe();
  };
}, []);
```

## Ref

```tsx
const inputRef = useRef<HTMLInputElement>(null);
inputRef.current?.focus();
```

## Context

```tsx
const value = useContext(MyContext);
```

## Reducer

```tsx
const [state, dispatch] = useReducer(reducer, initialState);
dispatch({ type: "somethingHappened" });
```

## Custom hook

```tsx
function useExample() {
  const [value, setValue] = useState("");
  return [value, setValue];
}
```

---

# 27. Glossary

| Term | Student-friendly meaning |
|---|---|
| API | A way for programs to communicate |
| Array | An ordered collection of values |
| Callback | A function given to other code to run later |
| Component | A reusable piece of a React interface |
| Component tree | Parent-and-child structure of components |
| Controlled input | Input whose value is stored in React state |
| Declarative | Describing the desired result |
| Dependency array | Values that tell an effect or memo when to update |
| Dispatch | Function that sends an action to a reducer |
| Effect | Synchronization with a system outside React |
| Event | A user or browser action such as a click |
| Fragment | A wrapper that adds no extra HTML element |
| Hook | Function that connects a component to a React feature |
| JSX | HTML-like syntax written inside JavaScript |
| Key | Stable identity for an item in a rendered list |
| Lifecycle | Stages when a component appears, updates, and disappears |
| Local storage | Browser storage that remains after a refresh |
| Mutate | Change an existing object or array directly |
| Props | Read-only information passed from parent to child |
| Reducer | Function that calculates next state from state and an action |
| Render | React calling a component to calculate its UI |
| State | Information a component remembers |
| Strict Mode | Development helper that detects unsafe behavior |
| TSX | JSX syntax inside a TypeScript file |
| TypeScript | JavaScript with compile-time type checking |
| Union type | A type that allows one value from a specific set |

---

# 28. What to Learn Next

After completing this guide, learn:

1. modern JavaScript array methods and object syntax;
2. advanced TypeScript features such as generics and type narrowing;
3. React Router;
4. API design and HTTP;
5. Vitest and React Testing Library;
6. form libraries and schema validation;
7. a framework such as Next.js, when your project needs one;
8. Ionic React and Capacitor for mobile applications.

## Final knowledge check

You should now be able to answer:

1. What is a component?
2. How are props different from state?
3. Why should state not be mutated?
4. When should you use `useEffect`?
5. When should you use `useRef` instead of state?
6. What problem does context solve?
7. When might a reducer be clearer than several state setters?
8. Why must hooks be called at the top level?
9. Why does a list item need a stable key?
10. Why are functional components preferred for most new React code?

If you can answer these questions and build the Study Planner without copying every line, you understand the core ideas of React.
