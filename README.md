# Make Me a Qual

Generating practice tests using questions from old Stanford math qualifying exams. Live version available at https://jonathanlove.info/qual/.

To function properly, all the following files need to be in the same folder:
- index.html
- personalqual.html
- qtags.js
- style.css
- images containing exam problems, labeled [alg / ana] + [year] + [S / F] + [M / A] + [question number]; for example, alg2010FM3.png, alg2012SA5.png, ana2012FA1.png.

This repository contains all of the above except for the image files. Old Stanford qualifying exam problems can be found at this page: https://mathematics.stanford.edu/phd-program/phd-qualifying-exams. 

## How it works

The basic structure of the qual generator is as follows.

- A large list of image files, one for each question that can be loaded, with a consistent labeling scheme.
- personalqual.html is a page that is initially empty aside from a header and footer. You can add a query string to the end of the URL, of the form "?qlist=" followed by labels separated by hyphens (for instance "?qlist=alg2013SA1-alg2017FA3"). The file contains javascript code that will take each label in the list and include the image file with the same name.
- index.html handles the question selection process. There are multiple ways of selecting questions, but every method compiles a list of question labels (“qlistvar”). When any of the qual-generating buttons is pressed, the form "makeitform" is called: this opens personalqual.html with a query string containing the entries in qlistvar.

The question selection process includes the ability to select problems by year and by subtopic. This process is handled as follows:
- qtags.js determines the sorting process for questions: subject (analysis/algebra), test year (e.g. 2012 Fall), and tag (subtopics addressed by each question). Questions can have multiple tags, and not every question needs to be tagged; any untagged question will be automatically added to an "unsorted" list. If new questions are added or tags are changed, this file can be edited without having to change anything in index.html or personalqual.html. The script ends with code that compiles a list of questions for each subject, each test year, and each tag.
- index.html loads the lists from qtags.js, and whenever the analysis/algebra radio button is clicked, two list of checkboxes are created: one for test year and one for tag. As checkboxes are selected, the function "updatelist" is called to determine the full set of questions satisfying the checked boxes (saving the list of valid questions as "qoptions")
