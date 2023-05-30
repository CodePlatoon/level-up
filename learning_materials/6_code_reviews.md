# Code Reviews

## Course Goals

* Describe the process of creating and submitting a pull request
* Explain what to look for when reviewing code

## Pull Requests

Code reviews are a tool to help to ensure a standard of quality for a code base, and are an opportunity for you to solicit feedback for the code you've written. Pull requests are the means we as developers use to submit code for review. In order to ensure that the pull request and code review process goes smoothly, you should adhere to some general guidelines for submitting code for review.

The pull request feedback cycle for first timers is usually longer than developers anticipate, because first pull requests almost always require a lot of feedback. There are some measures that you can take to reduce this feedback cycle.

### Length

Pull requests should be small. Small PRs mean faster turnaround time, less chance of a merge conflict, and less back and forth between the reviewer and submitter. When you are working on a project that involves production code, having smaller merge requests means that more code gets promoted to a production environment, more quickly.

### Title

PR titles should include the relevant ticket number and title, ie: *TODO-001 Display a list of tasks*. If tickets are small, or if the tickets tasks are effectively broken down, then the PRs should reflect that structure.

### Branch name

The branch name should model the ticket name ie: *todo-001-display-a-list-of-tasks*.

### PR description

What the description of the code review should contain varies from team to team, so check with your team to see what the norm is. It is generally better to be more descriptive than less, so as to help the reviewer understand what they should be looking for during the review.

A common template used for PR description is as follows:

#### Overview

What changed? This doesn't need to be overly technical, just plainly and concisely state the change this will introduce once merged.

Include why the change was made if the change was linked to a bug or special request or something not documented elsewhere. You can include the acceptance criteria for your story to satisfy this requirement.

#### Testing

All code submitted for review should be tested so that you ensure that you are only merging functional code into your . You should indicate how the changes were tested if that needs further description. Unit tests should be included in the code to review, but were there other tests not included in the code change? Did you do any manual testing for these changes?

#### Screenshots (optional)

If there is a UI change, screen shots should also be included.

### Commits

We learned about git maintenance in [a previous section](/learning_materials_4_git_project_maintenance.md). Part of git maintenance includes maintaining a clean and clear commit history. Reviewers will look at your commit history and check for the following:

* Commits should be prepended by the ticket number ie: *TODO-001 Display a single task*, *TODO-001 Display multiple tasks*
* Commits should be in the imperative mood (**Fix a typo**, and not *Fixes a typo*, *Fixing a typo*, *Fixed a typo*)
* Commits should be concise
* Commits should follow convention
    * First word should be capitalized
    * Use plain English–don’t include uncommon abbreviations
    * Don’t add a period at the end
* Squash unnecessary commits

### Test coverage

All pull requests should include tests for the features that were added. All tests must be passing. You **never** should commit and push up broken code for a PR, because if it gets merged, that broken code will infect the main branch of your repository.

## Code Reviews

Code reviews should be thorough and prompt. Delivering quality code reviews is a skill that comes with practice and exposure. Being on a team with a developer that has experience with providing quality code reviews is the simplest way to level up your code reviewing skills, but if that is not an option, you can pay attention to these factors when reviewing a pull request:

* Functionality
* Testing
* Style
* Quality

### Functionality

* Does the code description adequately explain the effect that will take place if the code is merged?
* Does the code submitted line up with that expectation / does it work?

### Testing

* Are there unit tests included for each public method?
* Do the tests cover all logical scenarios?
* Does the PR include instructions for how to test?

You will want to make sure that the tests cover the full functionality of the code. Let's look at an example:

```
def calculate_average(numbers):
    """
    Calculates the average of a list of numbers.

    Args:
        numbers (list): A list of numbers.

    Returns:
        float: The average of the numbers.

    Raises:
        ValueError: If the input list is empty.

    """
    if not numbers:
        raise ValueError("Input list cannot be empty.")

    return sum(numbers) / len(numbers)
```

This function takes an argument, numbers, and returns a number. We would need to account for a few scenarios in the unit tests:

1. Does it work? Does the method correctly calculate the average of a list of numbers?

```
assert calculate_average([1, 2, 3, 4, 5]) == 3.0
```

2. What should happen when the list is empty?

```
assertRaises(ValueError, calculate_average, [])
```

3. Is the precision what you are expecting for floating point numbers?

```
assert calculate_average([0.1, 0.2, 0.3]) == 0.2
```

4. What happens when you put in large numbers? Check for performance and accuracy.

```
assert calculate_average([1000000, 2000000, 3000000]) == 2000000.0
```


### Style

* Do the UI changes look good?

### Quality

* Is the PR appropriately documented?
* Does the PR include information like screen shots and acceptance criteria?
* Is the code well-designed?
    * Does the code adhere to language norms?
    * Are the names used for functions, variables, objects, etc clear and concise?
    * Is there any unnecessary complexity? Is it easy to understand?
    * Does it include anything that is not stated in the description or ticket? In other words, are they adding anything that doesn't belong?
    * If there are comments, are they necessary and useful?

#### Not adhering to Language Norms

Make sure that the code follows style guidelines. In the following code, we would want to mention that the case they are using for setting the variable (camelCase) is not idiomatic python (snake_case).

```
dateOfBirth = '1987/04/29'
```

#### Poor Naming

This is not great naming because it is vague and does not speak to the purpose of the function. Are they calculating area? Sum? Product? Also, what do `a`, `b`, and `c` represent?
```
def calculate(a, b, c):
    # method implementation...
```

This is also a bad method name because it is not concise and is redundant.

```
def calculate_area_of_cube_given_length_width_and_height(a, b, c):
    # method implementation...
```

Here is how we can suggest they improve this in the code review

```
def calculate_cube_area(length, width, height):
    # method implementation...
```

#### Unnecessary Complexity

This code works, but it is not implemented smartly. The if statement is unnecessary here.
```
def check_if_number_is_even(number):
    if number % 2 == 0:
        return True
    else:
        return False
```

For this, we can suggest they simplify the method
```
def is_number_even(number):
    return number % 2 == 0
```

#### Implements More Than What is Asked For

Let's say the ticket specifies that a checkbox should be added and this is the code that was provided:

```
<input type="checkbox" checked>
```

They are adding a default value of "checked" for the checkbox, but that was not the requirement.

#### Unhelpful Comments

Here is an example of a comment that is not particularly useful:

```
# Increment the counter by 1
counter += 1
```
