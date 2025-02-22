# Week Five - SPRINT
## Monday 17/02/2025

### During Session
- I set up the Azure database. This process took a while due to the code needing to be changed a bit and the ERD diagram needing to be reworked. Me and Liana agreed on a few changes for the ERD and started updating it to reflect our system better. Then Jacob helped me with finishing off the database as we were having a lot of issues actually linking the database to Blazor. The database itself was fine and a lot of the work on the database was done by myself, but me and Jacob ended up getting to the bottom of the issue with linking to Blazor and finally got it working. I then set up everyones IP in the firewall so they all had access and helped Liana download the Azure management app and logged her in through my admin credentials so she could also see the management of it.
- I created the results model.

### To Do
There will be no To-Do for this week as everything was done in class during the sprint.

### Issues
No conflicts this session

## Tuesday 18/02/2025

### During Session
- I gathered all the departments from the research I had done a few weeks back and added them to the database along with a description and link to their place on the NEXT website.
- I added all the roles to the database. Jasmine used my research and made the SQL statements which I then quereyed into the database along with their respective department ID and a link to the job posting (which can be nullable if there is no current job posting). We decided we would have to consider web-scraping and refreshing to make sure it gets the most relevant role posting for the recommended role.
- I added the range-based questions to the database. We decided to do range-based questions first as me and Liana had been working on the front-end and back-end for range based questions and were a bit ahead.

### To do
N/A

### Issues
No conflicts during this session.

## Wednesday 19/02/2025

### During Session
- Me and Liana began working and completing the front-end for range based questions and implementing the functionality on answering questions. We split this up so that I did all the HTML and CSS while she did the database connection in the code. I set up the buttons and then I did all the styling for the front-end.
- Me and Jasmine also worked on the general styling of the page. This included us going back through our research and adding some main css to the pages so we then could go off and do our own css for range based/text based.
- We had a lot of issues with the server side and webassembly side of our project this session. Me and Liana consulted Ra'ed about this in his office two times and after we came to a dead end, we were put into contact with Arian who attempted to help us over video call. He suggested we either create a external library and redo all our models, controllers, etc, in this library or switch everything to server side. After three hours we ended up switching everything to the server side as we had to have this ready for our meeting on Thursday.
- Me and Liana switched everything to server side and remade the folders for the webassembly and pages so everyone could start working on that.
- Me and Liana created a test for the range based questions to see what feedback would be recieved from the back-end code that she had been working on.
- I set up Jacob with the azure management portal as he was not there when I did it previously so when I got home I gave him the admin credentials as the server would go offline while I was sleeping.

### To do
Completed all before meeting

### Issues
No conflicts in this session

## Thursday 20/02/2025

### During Session
- Me and Liana got there at 8am to try and fix the issues she was encountering with the back-end development. The questions weren't calling back properly with EventCallBack and we attempted to debug it before the meeting but were unable to fully fix it before then.
- I did some last touches on the css for the range-based questions.
- I got Jasmine to push all of her css to her branch so me and Liana could have it on our screen. I also pushed my css directly into Liana's branch as she didn't have time to correct merge conflicts before the meeting but since mine had no conflicts I pulled it directly into hers.
- Me, Liana, and Jasmine had the meeting with NEXT.
- Being our product manager, I introduced everyone, and then showed our wireframes and asked for feedback on those. We got some feedback about some small design stuff such as needing to incorporate more photos, and to use the NEXT logo instead of the one we had used. After that, I showed the css for the range-based questions. Then I handed it over to Liana to screenshare the back-end as she had been working on that.

### To do
Sprint week ended

### Issues
We were missing a member for the meeting therefor were unable to explain a lot of the backend in the meeting with NEXT since none of us had worked on the text-based backend.