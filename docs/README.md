# Clinicians Who Code

An _opinionated_ guide for clinicians who want to build tech safely, openly, and quickly.

###
#TODO #10 link to mkdocs site

### MarkDown

### Front end

- javascript, HTML, CSS

### Version Control

- Git, GitHub, Git Flow
#TODO #3
- https://plethorachutney.github.io/git-workshop-presentation/
- semantic versioning

### Databases

- Use PostgresQL unless you have a good reason not to
- know about: Neo4j (Graph database) and MongoDB (JSON document database)

### Open Source

# Clinical Software Patterns

design patterns for healthcare
checklists

## Avoid Unnecessary Mappings

A mapping is where you are representing a concept with something which is _not_ that concept. For example, if you wanted to represent the sex of a patient and you chose '1' to represent 'male', and '2' to represent 'female'. I've seen this done, it's not uncommon in software to (for some reason) represent things numerically when they are prefectly clear as strings.

In my view this is an unnecessary mapping, and the only thing it can possibly server to do is confuse and introduce bugs, which will be that little bit harder to identify, because when scanning logs you are relying on being able to remember which number maps to 'male' and which to 'female'.

Just use the string representation of whatever it is. The clearer you can be in your programming, the better for you and for anyone else using your code. It also has benefits for patients who are treated using your code!

## Avoid Unnecessary Abbreviations and Acronyms

## APIs

## Clinical Calculators

Rhidian Bramley's blog https://clinicalwebportal.home.blog/2019/07/23/clinical-calculators/

## Integration

## Workflow

Here are some habits which are good to get into

### Git Workflow Checklist

- `git fetch` so you know you are definitely on the most up to date code
- Check which branch you are on - are you starting from the right place?
- Think about the work you're going to do - does it need a [feature branch](link)
- Write the new code
- Write tests for your code
- Make a commit, with an informative commit message

# working in open source

# People skills

- code review, pair programming
  code workflow

## APIs

https://www.freecodecamp.org/news/rest-api-tutorial-rest-client-rest-service-and-api-calls-explained-with-code-examples/
[2 hour FreeCodeCamp video tutorial on APIs](https://www.youtube.com/watch?v=GZvSYJDk-us)

know about libraries and APIs available
write comments "why" not "what" or "how"
documentation
code clarity, quality, linting
write code for people to read it
testing
continuous integration
deployment
security
charging for your time
talking about your work

## Terminologies

NHS Terminology Server https://ontology.nhs.uk/

## Resources

Interop Summit https://www.youtube.com/channel/UCoGOZfeTmZJkHn_4MjA5FFA/videos

## Community building

- forum
- wiki

# Acknowledgements

- Josh Case (Code Blue)
- Ian McNicoll
- Mark Bailey
- Louise Wilson & Kevin Monk - inspiration to get writing
