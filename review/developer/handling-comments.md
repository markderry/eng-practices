# How to handle reviewer comments

When you've sent a CL out for review, it's likely that your reviewer will respond with several comments on your CL. Here are some useful things to know about handling reviewer comments.

## Don't Take it Personally {#personal}

The goal of review is to maintain the quality of our codebase and our products. When a reviewer provides a critique of your code, think of it as their attempt to help you, the codebase, and Google, rather than as a personal attack on you or your abilities.

Sometimes reviewers feel frustrated and they express that frustration in their comments. This isn't a good practice for reviewers, but as a developer you should be prepared for this. Ask yourself, "What is the constructive thing that the reviewer is trying to communicate to me?" and then operate as though that's what they actually said.

**Never respond in anger to code review comments.** That is a serious breach of professional etiquette that will live forever in the code review tool. If you are too angry or annoyed to respond kindly, then walk away from your computer for a while, or work on something else until you feel calm enough to reply politely.

In general, if a reviewer isn't providing feedback in a way that's constructive and polite, explain this to them in person. If you can't talk to them in person or on a video call, then send them a private email. Explain to them in a kind way what you don't like and what you'd like them to do differently. If they also respond in a non-constructive way to this private discussion, or it doesn't have the intended effect, then escalate to your manager as appropriate.

### Example of Handling Reviewer Comments Politely

Imagine you receive a comment like this: "This code is terrible. Why did you write it this way?" Instead of responding defensively, you could reply: "I understand your concern. I wrote it this way because of X, Y, and Z reasons. Do you have any suggestions on how I can improve it?"

## Fix the Code {#code}

If a reviewer says that they don't understand something in your code, your first response should be to clarify the code itself. If the code can't be clarified, add a code comment that explains why the code is there. If a comment seems pointless, only then should your response be an explanation in the code review tool.

If a reviewer didn't understand some piece of your code, it's likely other future readers of the code won't understand either. Writing a response in the code review tool doesn't help future code readers, but clarifying your code or adding code comments does help them.

### Example of Clarifying Code

Suppose a reviewer comments, "I don't understand why you're checking for null here." Instead of just explaining in the code review tool, you could update the code to make it clearer:

```java
// Check for null to avoid a NullPointerException when accessing the email field
if (email != null) {
    // existing code
}
```

## Think for Yourself {#think}

Writing a CL can take a lot of work. It's often really satisfying to finally send one out for review, feel like it's done, and be pretty sure that no further work is needed. So when a reviewer comes back with comments on things that could be improved, it's easy to reflexively think the comments are wrong, the reviewer is blocking you unnecessarily, or they should just let you submit the CL. However, **no matter how certain you are** at this point, take a moment to step back and consider if the reviewer is providing valuable feedback that will help the codebase and Google. Your first question to yourself should always be, "Is the reviewer correct?"

If you can't answer that question, it's likely the reviewer needs to clarify their comments.

If you *have* considered it and you still think you're right, feel free to respond with an explanation of why your method of doing things is better for the codebase, users, and/or Google. Often, reviewers are actually providing *suggestions* and they want you to think for yourself about what's best. You might actually know something about the users, codebase, or CL that the reviewer doesn't know. So fill them in; give them more context. Usually you can come to some consensus between yourself and the reviewer based on technical facts.

### Example of Thinking for Yourself

If a reviewer suggests a different approach to solving a problem, consider their suggestion carefully. If you still believe your approach is better, explain your reasoning. For example: "I understand your suggestion to use a different algorithm, but I chose this one because it has better performance in our specific use case."

## Resolving Conflicts {#conflicts}

Your first step in resolving conflicts should always be to try to come to consensus with your reviewer. If you can't achieve consensus, see [The Standard of Code Review](../reviewer/standard.md), which gives principles to follow in such a situation.

### Example of Resolving Conflicts

If you and your reviewer can't agree on a particular change, try to find a compromise. For example: "I see your point about the potential performance issue. How about we implement your suggestion, but also add a configuration option to switch back to the original approach if needed?"
