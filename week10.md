# Week Ten - SPRINT WEEK

## Monday 24/03/2025

### During Session
- The first day of sprint me and Jasmine continued on our work from last week. We had originally planned to only spend Monday solving issues, and the rest of the week debugging, but we ran into a lot of issues on Monday. We spent this day figuring out how to configure a login system using Authentication and Authorization in Blazor. We had worked on this the previous week as well, and got quite far with it, but we still ran into the issue where users weren't being passed through authentication. We were able to authorize page views accordingly, but no user at all could access these pages. Most of the day was spent looking into this as it was crucial that (e.g.,) a candidate can not look at a staff dashboard.
- Eventually password hashing worked and could compare the key of the hashed password in the database to the users inputted password. But the page view authorization still didn't work for any logged in user.
- We figured out that the issue likely lied in how the Cookies were handled in the program.cs in the builder services, which stores the authorized state of the user. We tried adding some builder services for staff and candidate, as well as some functions like app.UseAuthentication(); but it still wouldn't run properly.
- We referenced this Microsoft documentation to try and understand why it wasn't working and how to go about building it: https://learn.microsoft.com/en-us/aspnet/core/blazor/security/?view=aspnetcore-9.0&tabs=visual-studio
- This video was also followed: https://www.youtube.com/watch?v=GKvEuA80FAE&ab_channel=CodingDroplets
- This was the whiteboard used for planning out our day for the first day of Sprint Week where our tasks were divided and documented the tracking: (proof_and_screenshots\sprintweekboard.png)

### To Do
Figure out why the authorization isn't working
Do some research on cookies and find the best way to handle them for authorization

### Issues
Authorization not allowing us to see any pages. We were working off our own branch so this didn't halt the progress of our other members, but we were halted on our end with not being able to access any login-required pages.

## Tuesday 25/03/2025

### During Session
- To start this session off, we decided to take a break from authorization as we weren't getting far with it and it caused us to just be confused. So, we instead started with an Admin adding a new Staff member to the database. We decided an Admin should only be able to add a Staff member because it is highly unlikely that a Staff member should be able to add one of their peers, for example. This was quite easy as it was just the same as adding a Candidate, except changing the values and adding in StaffId (their staff number) to the input values. We created the page for this and added in what should be where it authorizes the Admin to only view and edit on this page.
- We then did page logout, because I decided to email Arian about the page authorization and see if he could help us at all. While I waited for his email reply (proof_and_screenshots\arianconsult.png). To do this, we had to find a way to clear the users cookies after they logged out. We have it set up so after 30 minutes, they are timed out, and cookies are removed from the user so they will have to login again. This was general safety practice (e.g.,) if someone were to leave their laptop open in public. We did so by adding a MaxAge(30) to the cookie builder, which clears the cookies after the maximum age of 30 minutes.
- We then took another try at authorization, but got nowhere with it again. We kept getting this error: "No authenticationScheme was specified, and there was no DefaultChallengeScheme found."
    - We looked on a few Stackoverflow links to try and fix this bug, as we figured it probably was due to our double instantiation of cookies for different types of users. So originally, we had it that Staff and Candidate were on two instances of Builder Services for cookies, but this led to that error. The links we looked at were:
    https://stackoverflow.com/questions/75683753/no-authenticationscheme-was-specified-and-there-was-no-defaultchallengescheme 
    https://learn.microsoft.com/en-us/answers/questions/1164459/exception-scheme-already-exists-when-trying-to-imp
- Arian then replied but we were quite busy doing the logout and adding staff as we didn't want to stop development due to this, so me and him planned to call tomorrow and see if he could advise on how to go about our issue. He said he knew the problem we were having, so I told Jasmine I would take on all the login, authorization, and authentication from here on out as I was the one having communication with Arian.


### To Do
Completed all for this session

### Issues
Authorization still not working
Cookies only clear after 30 minutes, but we wanted them to fully delete on log out. After some research we found out this could be quite difficult to do as you have to overwrite the current cookie with a negative time value (e.g., MaxAge(-1D)) to wipe it. We left it as the 30 minute clear and logout for now, deciding if we have more time to implement that after I consult with Arian.

## Wednesday 26/03/2025

### During Session

- called arian the entire day trying to fix our blazor auth
- wrote sql query for lianas encouraging messages

### To Do
Completed all for this session

### Issues
No conflicts this session

## Thursday 27/03/2025

### During Session
- cookie agreement

### To Do
Completed all for this session

### Issues
No conflicts this session

## Friday 28/03/2025

### During Session
- crud pages for staff and candidate
- light house testing

### To Do
Completed all for this session

### Issues
No conflicts this session

