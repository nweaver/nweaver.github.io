---
title: Statement on Teaching
---



*I wrote this in Fall of 2025 as my statement of teaching for various
 academic jobs after being laid off from Davis for budgetary reasons
 in Spring 2025.  Unfortunately I think my strident nature, especially
 with regard to faculty use of AI, was part of the reason I did not
 receive any interview requests.  Playing Cassandra is not how one wins a popularity contest*

## Statement on Teaching:  Effective Programming in the Age of AI

### Nicholas Weaver

Computer science is not computer programming but computer programming
is a foundational skill necessary for students in computer science.
Ensuring that our students have the necessary skills to thrive in both
the later classes and beyond must be the primary objective of the
initial lower division sequence and the computer science department.

This requires student-friendly policies, an emphasis on modern
programming languages and development tools, security by design,
comprehensive testing, and significant effort to ensure an effectively
complete ban on “AI” copilot tools and large language models (LLMs).

The last is new, a constraint that must be dealt with if we want to
prevent computer science education from collapsing.  Dealing with this
problem will require new educational infrastructure and significant
enforcement of academic misconduct rules and restrictions on faculty
as well.

**The Nature of LLMs:** LLMs are \[to use the precise philosophical
term\] [bullshit<sup>1</sup>](#1) [machines<sup>2</sup>](#2) designed
to produce statements that have no actual relation to whether they are
true or false.  The output of an LLM is predictive text based on the
input, the prompt, and the compressed training data.  Indeed, since
there is no semantic understanding in modern LLM-based chatbots, they
do not actually use the LLM for tasks such as [river-crossing
problems<sup>3</sup>](#3) or even just [counting the number of ‘b’s in ‘blueberry’<sup>4</sup>](#4):
situations where an incorrect answer is embarrassing to the chatbot
developer.

This means that LLM output must never be used in a student facing
context.  If the output is unchecked we present the students with
unfiltered bullshit.  Checking the output is not sufficient as humans
are notoriously poor at checking automated processes while the
overhead of checking bullshit is often the same or even higher than
creating the underlying content.  It is critical that all educators
who care about ensuring our students receive correct information do
all we can to limit the efforts to push this technology into
student-facing roles.

Many students already intuitively understand that LLMs are bullshit
and CS students in particular should understand this in detail by the
time they graduate.  How do we expect our students to react to being
presented with what is philosophically bullshit?  How valuable will
they believe their education to be?

**LLMs and Programming:** LLMs for coding have their own additional
problems.  The training set for the LLMs is based largely on all the
public computer code available, complete with using unsafe APIs,
unsafe languages, and general bugs.  This makes the output of a coding
LLM fundamentally unreliable.

Coding LLMs can only be safely used where bugs don’t matter (such as
using the LLM to create a prototype that will be thrown out), where
the output is self-checking (such as creating code-based proofs where,
if they compile correctly, are axiomatically correct), or where the
LLM is just used as an improved auto-complete function that better
tracks variable names[<sup>5</sup>](#5).

Unfortunately, however, there is an area where coding LLMs are
remarkably successful: undergraduate programming assignments.  This is
because we don’t demand students produce bug-free code and the
training data (mostly GitHub archives) includes multiple copies of
almost every undergraduate assignment ever created.  A student can
easily use a coding LLM to pass all our programming assignments
without actually learning how to program.

Allowing the use of these systems creates an environment where
potential employers, realizing that a significant fraction of
graduates lack programming skills, treat all our fresh graduates as
unsuitable.  Compounding the problem is that we must not create
incentives where honest students believe they too need to cheat
because other students are using coding LLMs.

At the same time educators can’t simply prohibit modern tools.  Modern
IDEs such as Visual Studio Code are essential tools that students need
to understand and use.  Just as it is negligent to allow students
unfettered access to AI tools it is similarly negligent to not enable
students to use the modern tools but with any AI “co-pilot” disabled.

**Dedicated Coding Systems:** Fortunately we can build systems that
can still enable modern tools, add checks designed to detect LLM
misuse, and which are designed to not appear oppressive to honest
students.  Building this infrastructure is necessary to continue to
teach computer science in the age of AI.

Modern IDEs robustly support remote development where the user
interface is separated from the actual coding environment.  This can
take the form of a container or an `ssh` connection to a remote system.
I previously used containerized development with VSCode for first-year
students with C and C++ with great success.

If students use remote `ssh` connections to a server we control, this
not only enables a consistent environment but also enables us to
provide custom VSCode or JetBrains extensions.  A custom extension can
not only disable the AI copilot but also log all keystrokes in a
secure manner.  The keystroke log can then detect various forms of
misconduct such as cutting and pasting code from a 3rd-party LLM.
Building and deploying such an environment will be my first priority
when I resume teaching.

Such intrusive monitoring must be disclosed.  Not only would it be
unethical to conduct such monitoring without student consent but the
presence of this monitoring is specifically designed to reassure
honest students.  It not only explicitly informs honest students that
any dishonest student is likely to be caught (removing incentives to
cheat) but also makes it clear that detecting misconduct does not rely
on potentially false-positive prone “AI” based AI detectors.

Developing such a tool will require significant work but it is
necessary to preserve the value of a CS degree.  Students, potential
employers and graduate programs all need reassurance that we ensure
that students actually learn how to program.  If we fail to do this,
and fail to ensure that all lower-division classes implement such an
anti-AI program, we risk failing our students.

**Other Emphases:** Other areas also significantly enhance student
success.  This includes a strong emphasis on security and soundness: C
should not be used until the students are also introduced to assembly
while C++ needs to be restricted to the upper division and used only
in a modern form (C++20 with smart pointers and templated
data-structures), techniques which experience shows students are
capable of using.  Similarly students must be instructed using
prepared statements and execve instead of raw SQL and system.

Programming languages need to be selected to enhance student
productivity.  The first class is probably best in Python due to its
basic nature but subsequent classes should be in Go, Kotlin, or
perhaps Rust[<sup>6</sup>](#6): modern languages with strong static
typing, an emphasis on safety, while also possessing strong type
inferencing and other features that both improve programmer
productivity and eliminate entire categories of bugs.  Experience with
Go (as a programmer) and Kotlin (as both a programmer and using it as
a language for instruction) have shown me just how critical these are.

An emphasis on code testing is also critical.  Assignments need to
include not only a requirement to write test code in a testing
framework but the test code should be graded separately by applying
the student’s test code to an opaque official solution with the grade
representing the test coverage achieved, a technique I first used in
Berkeley’s cryptographic engineering assignment for the upper division
computer security class.  Similarly when I teach C now I use a
C++/CMake containerized development environment as Google Test is far
superior to C-only unit-testing frameworks and containerization
enables valgrind regardless of the student’s host OS.

Finally, student policies on late assignments and other issues need to
be accommodating.  My previous experience showed that this improves
student outcomes and reduces student stress.  Taken together these
more traditional aspects of computer science education are all
critically important.

The rise of the LLM has significantly complicated computer science
education.  But we can deal with it effectively through tools and
policies designed to limit the damage possible, including ensuring
that LLMs never generate student facing content and students are
assured that other students will not have the machine doing the
homework.

<A ID="1"></A> \[1\]: Frankfurt, H. G. (2005). On bullshit. Princeton
University Press.

<A ID="2"></A> \[2\]: Hicks, M.T., Humphries, J. & Slater, J. ChatGPT is
bullshit. *Ethics Inf Technol* **26**, 38
(2024). [https://doi.org/10.1007/s10676-024-09775-5](https://doi.org/10.1007/s10676-024-09775-5)

<A ID="3"></A> \[3\]:  [https://the-decoder.com/llms-give-ridiculous-answers-to-a-simple-river-crossing-puzzle/](https://the-decoder.com/llms-give-ridiculous-answers-to-a-simple-river-crossing-puzzle/)

<A ID="4"></A> \[4\]: [https://minimaxir.com/2025/08/llm-blueberry/](https://minimaxir.com/2025/08/llm-blueberry/)

<A ID="5"></A> \[5\]: The latter case needs to be used with care:
There is effectively an ‘uncanny valley’ type problem in humans
checking automated systems.  If the error rate is too low a human gets
complacent and fails to properly check the results.

<A ID="6"></A> \[6\]: Rust should probably be used primarily for
embedded programming: its advantage over Go and Kotlin lies in the
lack of a garbage collector which provides far more deterministic
memory behavior and the ability to escape many of the safety
constraints.