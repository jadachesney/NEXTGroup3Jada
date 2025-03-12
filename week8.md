# Week Eight
## IT Session - Monday 10/03/2025

### During Session
- During this session I completed the landing page for the website. I kept having the issue where my elements weren't resizing properly for mobile users/wasn't dynamically responding. Arian helped me with this, the issue was due to the video as its not a background. We fixed this by making the position absolute and setting top to 0. Then I set the z-index to -1 and for all other content (such as headings etc) the z-index was set to 1. This will possibly need refining once we merge all of our css together due to Jasmine having changed the navbar.

### To Do
Completed

### Issues
No conflicts this session

## Group Meeting 1 - Tuesday 11/03/2025

### During Session
- I started fixing the css for the range-based questions page as Liana had finished the back-end for now. I centered all components as the css I had done previously was quite messed up due to Liana and Jacob changing the page a lot. Then I started looking into ways to make the questionnaire seem more appealing. I decided to use Bootstrap to create an animated progress bar and used the colours off NEXT's website for this. 
- I linked all Range-Question-ID's in the database to the Department-ID's and then set their alignment. This goes off of the questions we made for text based answers, and then I wrote them all out (see photo evidence) so I could set them as true or false in the database. To do this I used a Bit where 1 = true and 0 = false. I then queryed this in using SQL and populated the database with this link table.

### To do
- Functionality for Onclick for progress bar

### Issues
No conflicts in this session

## Group Meeting 2 - Wednesday 12/03/2025

### During Session
- During todays session I focused on the functionality for the progress bar. Bootstrap itself seemed to not support an Onclick function for this, so at first I attempted switching to a Blazor component but that became too messy. So, I switched back to Bootstrap, and incorporated some jQuery/JS to make the Onclick function work. I included this so that when the user clicks next for a question, the progress bar will increase in size and show what question theyre on. The width of it still needs to be changed but the JS worked perfectly after I had to do much research on it (see evidence).

### To do
Done

### Issues
A member of our group has been consistently 1-2 hours late for our meetings. Though this isn't a technical issue, as a group we decided to have a conversation about it to the person and how it was impacting our groupwork/it was disrespecting our time as we put a lot of time aside for these three meetings a week. This has been a consistent issue since the start of the project and hasn't improved.