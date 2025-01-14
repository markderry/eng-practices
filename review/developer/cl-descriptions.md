# Writing good CL descriptions

A CL description is a public record of **what** change is being made and **why** it was made. It will become a permanent part of our version control history, and will possibly be read by hundreds of people other than your reviewers over the years.

Future developers will search for your CL based on its description. Someone in the future might be looking for your change because of a faint memory of its relevance but without the specifics handy. If all the important information is in the code and not the description, it's going to be a lot harder for them to locate your CL.

A good CL description helps reviewers understand the context and purpose of the change, making the review process more efficient and effective. It also helps future developers understand the reasoning behind the change, which can be crucial for maintaining and evolving the codebase.

## First Line {#firstline}

*   Short summary of what is being done.
*   Complete sentence, written as though it was an order.
*   Follow by empty line.

The **first line** of a CL description should be a short summary of *specifically* **what** *is being done by the CL*, followed by a blank line. This is what appears in version control history summaries, so it should be informative enough that future code searchers don't have to read your CL or its whole description to understand what your CL actually *did* or how it differs from other CLs. That is, the first line should stand alone, allowing readers to skim through code history much faster.

Try to keep your first line short, focused, and to the point. The clarity and utility to the reader should be the top concern.

By tradition, the first line of a CL description is a complete sentence, written as though it were an order (an imperative sentence). For example, say "**Delete** the FizzBuzz RPC and **replace** it with the new system." instead of "**Deleting** the FizzBuzz RPC and **replacing** it with the new system." You don't have to write the rest of the description as an imperative sentence, though.

### Examples of First Lines

Here are some examples of good first lines for CL descriptions:

- "Fix null pointer exception in User class."
- "Add logging to the authentication module."
- "Refactor the database connection handling code."

These examples are short, focused, and provide a clear summary of what the CL does.

## Body is Informative {#informative}

The rest of the description should be informative. It might include a brief description of the problem that's being solved, and why this is the best approach. If there are any shortcomings to the approach, they should be mentioned. If relevant, include background information such as bug numbers, benchmark results, and links to design documents.

If you include links to external resources consider that they may not be visible to future readers due to access restrictions or retention policies. Where possible include enough context for reviewers and future readers to understand the CL.

Even small CLs deserve a little attention to detail. Put the CL in context.

### Examples of Informative Bodies

Here are some examples of good informative bodies for CL descriptions:

- "This CL fixes a null pointer exception that occurs when the User class is instantiated with a null value for the email field. The fix involves adding a null check before accessing the email field. This approach was chosen because it is simple and effective. Bug number: 12345."
- "This CL adds logging to the authentication module to help diagnose issues with user login. The logging includes the username, timestamp, and the result of the authentication attempt. This will help us identify patterns in failed login attempts and improve the security of our system."
- "This CL refactors the database connection handling code to use a connection pool. This improves the performance of the application by reusing database connections instead of creating a new one for each request. Benchmark results show a 20% improvement in response time."

## Bad CL Descriptions {#bad}

"Fix bug" is an inadequate CL description. What bug? What did you do to fix it? Other similarly bad descriptions include:

- "Fix build."
- "Add patch."
- "Moving code from A to B."
- "Phase 1."
- "Add convenience functions."
- "kill weird URLs."

Some of those are real CL descriptions. Although short, they do not provide enough useful information.

### Examples of Bad CL Descriptions

Here are some examples of bad CL descriptions and why they are inadequate:

- "Fix bug." (What bug? What did you do to fix it?)
- "Add patch." (What does the patch do? Why is it needed?)
- "Phase 1." (Phase 1 of what? What does this phase involve?)

## Good CL Descriptions {#good}

Here are some examples of good descriptions.

### Functionality change

Example:

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

The first few words describe what the CL actually does. The rest of the description talks about the problem being solved, why this is a good solution, and a bit more information about the specific implementation.

### Refactoring

Example:

> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

The first line describes what the CL does and how this is a change from the past. The rest of the description talks about the specific implementation, the context of the CL, that the solution isn't ideal, and possible future direction. It also explains *why* this change is being made.

### Small CL that needs some context

Example:

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

The first sentence describes what's actually being done. The rest of the description explains *why* the change is being made and gives the reviewer a lot of context.

## Generated CL descriptions

Some CLs are generated by tools. Whenever possible, their descriptions should also follow the advice here. That is, their first line should be short, focused, and stand alone, and the CL description body should include informative details that help reviewers and future code searchers understand each CL's effect.

## Review the description before submitting the CL

CLs can undergo significant change during review. It can be worthwhile to review a CL description before submitting the CL, to ensure that the description still reflects what the CL does.

### Example of Reviewing a CL Description

Before submitting a CL, take a moment to review the description and make sure it accurately reflects the changes made. For example, if the CL initially fixed a bug but later included a refactoring, update the description to include both aspects:

> Fix null pointer exception in User class and refactor email validation.
>
> This CL fixes a null pointer exception that occurs when the User class is instantiated with a null value for the email field. The fix involves adding a null check before accessing the email field. Additionally, the email validation logic has been refactored to improve readability and maintainability. Bug number: 12345.

Next: [Small CLs](small-cls.md)
