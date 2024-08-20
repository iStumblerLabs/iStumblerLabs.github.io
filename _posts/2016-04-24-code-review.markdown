
# Code Review: You Are Doing it Wrong

<img src="/images/2016/20160424-code-review.webp" alt="Don't Blame Me! I Copied the Code From Jim." width="512"><br>
© Geek and Poke — https://geek-and-poke.com

Code review is the new Agile; a software development best practice that’s become de rigueur in many shops. While having more eyes on code is generally a Good Thing™, I’ve see review practices in place which are worse than a waste of time. Instead of helping to produce high quality code, poor or missing code review guidelines can impede progress, create frustration, sap motivation, and in extreme cases; enable harassment.

While the benefits of code review are fairly well established, there isn’t a lot of guidance on how to do code reviews in a way that both improves the code and is collegial. Here’s how to usefully and productively review code:

## Review Function, Not Form

Comments which focus on the coding style, often in service of ‘readability’ are the first cardinal sin of reviews. Let’s be clear: code style means nothing to the compiler, the end users or even in most cases the maintenance programmers who will eventually take over care and feeding of your code base. As a purely aesthetic concern it has no place in the review process.

If your coding standards are longer than a single example file you have a problem. Someone on the team is more interested in beauty than truth, and is willing to impose a totalitarian regime to enforce what eventually resolves to personal preference. Any standards the team does agree upon should be enforced by automated linting or formatting tools: getting detailed formatting feedback is much more palatable when it’s coming from a program than a person.

When reviewing code, look past your personal preference for style and focus on the functional goals of the code and the implementation choices made by the code writer. You’re looking for bugs, not hairs out of place.

## Reviewers Should Not Have Veto Power

With the possible exception of a brand new developer in their first months of professional work, nobody should have to tolerate veto power over their submissions. In fact, the code review process shouldn’t be prospective at all, despite most of the tools being built this way.

I once had a submission rejected because the reviewer intended to perform the same task in a different, more complicated way, at a later date. The review comment suggested that my method (editing the init scripts of an embedded linux system to start daemons at boot time) was not sufficient for our needs, even as a temporary solution, despite being the preferred method for nearly all UNIX systems for decades.

This veto of my changes prevented me from achieving my goals and a flaccid management response made my job literally impossible. The culpable developer eventually failed to implement the more complex init process management system and it’s dependencies and had to resort to—wait for it—editing the init shell scripts.

Code review is about helping your fellow developers write better code, not about asserting that it’s your way or the bit bucket. Review code after its landed, not before, so the author can move forward and does not have to wait for reviews.

## Rejecting a Submission Should Require Work

After style nitpicking and assertion of veto power are taken out of the picture what’s left to actually do in the code review process? Look for errors and bugs: then write test cases to expose them or patches to fix them.

If a reviewer feels the need to reject a submission they should be prepared to write a test case that fails or provide a diff. Code should then be approved automatically when it passes the test or the diff has been applied. Test cases are valuable, as they can be used by original code writer to validate their change and for QA, which can add it to their automated regression testing and a diff is much easier to apply and clearer than a textual description of changes.

Nitpicking is easy, spotting bugs and writing tests with good code coverage is hard. Requiring a test case or diff is a good way to bolster the quality and reliability of the system and discourages petty objections.

## Technical Harassment is Never Acceptable

Besides my personal experience with the de-facto veto power given to reviewers in the name of consensus; I’ve heard stories about bad actors who used the review process as a way to effectively reduce their co-workers ability to make progress on features, resulting in either poor reviews or extreme frustration. While thankfully rare, these incidences, like other forms of workplace harassment should not be tolerated by management.

We have come a long way in the modern workplace to recognizing and confronting many forms of harassment, which generally makes for a more pleasant and productive working environment for everyone. Technical harassment is sadly not a rare issue, but an important one for managers to recognized and deal with just as quuckly as any other form of unprofessional behavior.

As code writers it’s up to us to decide how we work together to build reliable, maintainable systems. We should focus on how we can help each other to write better code, not now we can criticize and obstruct using technical process.

[Sine ira et studio.](http://xkcd.com/1695/)
