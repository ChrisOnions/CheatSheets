## Promise-

```javascript
const choresDone = true;

// Promise
const willGetSwitch = new Promise((resolve, reject) => {
  // Check for a desireable outcome, if so resolve the promise
  if (choresDone) {
    const reward = {
      name: "Nintendo Switch",
      desired: true,
    };
    resolve(reward);
    // Otherwise reject the promise
  } else {
    const issue = new Error("Child did not finish chores as promised");
    reject(issue);
  }
});
// Another promise to call only if we get the reward
const playGames = (reward) => {
  const message = `I am playing games on my new ${reward.name}`;
  return Promise.resolve(message);
};

willGetSwitch
  .then(playGames)
  .then((resolved) => console.log(resolved))
  .catch((err) => console.error(err));
```

## Promise-all

```javascript
// Promise resolved right away
const p1 = new Promise((resolve, reject) => {
  const time = 0;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    resolve("Resolved right away");
  }
});
console.log("Status of p1:", p1);

// Promise resolved after one second
const p2 = new Promise((resolve, reject) => {
  const time = 1000;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    setTimeout(() => {
      resolve("Resolved after 1 second");
    }, time);
  }
});
console.log("Status of p2:", p2);

// Promise resolved after three seconds
const p3 = new Promise((resolve, reject) => {
  const time = 3000;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    setTimeout(() => {
      resolve("Resolved after 3 seconds");
    }, time);
  }
});
console.log("Status of p3:", p3);

// After all three are resolved, Promise.all() returns the results
Promise.all([p1, p2, p3])
  .then((values) => {
    console.log("\nThe returned array from our Promise.all() call:");
    console.log(values);
  })
  .catch((err) => new Error(err));
```
