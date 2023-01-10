### Agreements

The guidelines of this contributing document does not have as a function to restrict or force developers to make use of specific flow but as an engaged team we decided to create it and follow according with our own needs. To sum up, the reason this document was created is to be a concise and generic base-flow of the process to develop in a way they become more closer between teams and make it possible to reduce the friction and speed up the flow when exchanging team members or when using, contributing to other team's repositories.

### Tip

> Do not make reviews if any of the processes below has no compliance. If not, notify the developer about their mistakes and apply the changes correctly - a new MR shouldn't be necessary. If you do not understand the code you are reviewing, ask. Just ask it even if you think or are really sure that they are naive or too simple questions. These actions can motivate another coworkers to act by the same way and encourage them to ask always about everything they didn't understood.

###  Development process

- do not initialize a new feature/bug/enhancement while a mainly task was not created to track your activity;
- always create a new branch according with the ID over the task created at github project board assigning the correct issue id;
- versioning your code with git;
- keep up a repository per microservice;
- locking the push directly to the master branch (if really necessary);
- working with MR's and code review (suggested 1 revision at least per MR)
- please keep a changelog (consider to use [changelog-it](https://github.com/falcucci/changelog-it) generator);
- always create clear and good documentation in project architecture, its modules and dependencies. It reduces the time spent in understanding the project when onboarding new people
- do unit tests and integration tests
- configure CI/CD pipelines (gitlab has a built-in or using github actions) to improve the processes
- avoid multiple nesting coding style, it makes the code harder to read

### How to develop a new feature?

As you develop your feature in the new branch it should be always sync to be merged, once that we have to make sure that all tests still working like a charm at our pipelines and when we merge many MRs the change to break up everything it’s high. 

Also, the branch should always have staging as its ref. The flow is simple as you see in the image bellow.

![Untitled-2020-05-25-2244-9](https://user-images.githubusercontent.com/33763843/211507685-4b78da84-74b9-4199-87c7-58a24fc7dfeb.png)

### How to develop an expedite bugfix?

First, identify which environment the bug has been affected. It will decide where to start. So, with that said  we should start the throubleshooting to recognize which version has the bug to immediately start the rollback correctly.

That's an important fact to always remember to build compatible versions with a consumer service or an application, the system always should have a rollback option.

![Untitled-2020-05-25-2244-13](https://user-images.githubusercontent.com/33763843/211508038-d0b1f029-2ecd-4513-a555-b23569519f28.png)

### Changelog process

It requires node.js to run.

now you can install the following library to automate the process:

```bash
npm i -g @falcucci/changelog-it@latest
```

### Hands on

without alias it is pretty simple to run:

```bash
changelog-it --range <TAG>...<REF> --release --gmud 
```

most common command used by:

```bash
changelog-it --range v5.8.31...v5.8.40 --release --gmud
```

##### Aliases, why?

Aliases are generally helpful shortcuts, this one it is amazing to minimize the daily processes avoiding you to forget a big command.

Also we can automate it even better just adding the following alias in your shell.

```bash
alias release-me='curl -LsS https://raw.githubusercontent.com/falcucci/release-me/master/changelog-it.sh | bash -s $1 $2'
```

#### Now, you can run:

```bash
release-me patch "Various spec compliancy fixes and better support for smart pipelines and private methods."
```

Basically, it will:

- create a semantic version based on the params (minor, patch, major);
- publish the tag on github/gitlab;
- start to generate a changelog based on the git refs (by default it must compare the latest tag with the head ref);
- send a message to the slack channels to preview the new release (if possible);
- create a github/gitlab release (required to show the MR`s;

### Configuration

It must have be configured using a `changelog.config.js` file created at the root of your workspace directory.
